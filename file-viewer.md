# File Viewer Component

## Overview

The File Viewer component provides a comprehensive and accessible modal-based interface for viewing images and PDF documents built with Genesis Design System tokens. It supports two distinct modes (image gallery and PDF viewer), advanced features including zoom controls, pan functionality, navigation between files, thumbnail sidebar, and download capabilities. The component is designed for both single and multi-file viewing scenarios with complete keyboard navigation and accessibility support.

## Component API

### FileViewer Props

| Prop          | Type                                    | Default     | Description                                                        |
| ------------- | --------------------------------------- | ----------- | ------------------------------------------------------------------ |
| files         | `string[]`                              | Required    | Array of file URLs (images or single PDF) to display in the viewer |
| onFileSelect  | `(file: string, index: number) => void` | `undefined` | Callback function when a file is selected with file URL and index  |
| onDownload    | `(file: string) => void`                | `undefined` | Callback function when download is initiated with the file URL     |
| headerTitle   | `string`                                | `undefined` | Title displayed in the modal header                                |
| mode          | `"image" \| "pdf"`                      | `"image"`   | Viewing mode: image gallery or PDF document viewer                 |
| className     | `string`                                | `undefined` | Additional CSS classes for customization                           |
| buttonTitle   | `string`                                | `undefined` | Text for the trigger button to open the modal                      |
| triggerButton | `ReactNode`                             | `undefined` | Custom trigger button element to open the modal                    |
| footerIcons   | `ReactNode`                             | `undefined` | Custom footer icons/buttons replacing the default download button  |

### Import Statement

```typescript
import { FileViewer } from "gends";
```

## Viewer Modes

### Image Gallery Mode

The default mode for viewing multiple images with navigation controls, zoom functionality, and thumbnail sidebar.

**Key Features:**

- **Thumbnail Sidebar**: 172px width with scrollable thumbnails (124×124px each)
- **Main Viewer**: 778px width with zoom and pan controls
- **Navigation Controls**: Previous/next buttons with counter display
- **Zoom Controls**: Slider-based zoom (0-100%) with pan functionality when zoomed
- **Selection Indicator**: Primary color ring (4px) around selected thumbnail

```tsx
// Basic image gallery
<FileViewer
  files={[
    "https://example.com/image1.jpg",
    "https://example.com/image2.jpg",
    "https://example.com/image3.jpg"
  ]}
  headerTitle="Image Gallery"
  onFileSelect={(file, index) => console.log(`Selected: ${file} at index ${index}`)}
  onDownload={(file) => console.log(`Downloading: ${file}`)}
/>

// Single image viewer
<FileViewer
  files={["https://example.com/single-image.jpg"]}
  headerTitle="Single Image Viewer"
  mode="image"
/>
```

### PDF Document Mode

Specialized mode for viewing PDF documents with page-by-page navigation and zoom capabilities.

**Key Features:**

- **PDF Processing**: Automatic PDF-to-image conversion for display
- **Page Thumbnails**: 124×155px thumbnails with page numbers
- **Scrollable Viewer**: Vertical scroll through all PDF pages
- **Zoom Integration**: Synchronized zoom across all pages
- **Page Tracking**: Intersection observer for current page detection
- **File Size Display**: Shows PDF file size in MB

```tsx
// PDF document viewer
<FileViewer
  files={["https://example.com/document.pdf"]}
  headerTitle="PDF Viewer"
  mode="pdf"
  buttonTitle="Open PDF Document"
  onDownload={(file) => handlePdfDownload(file)}
/>

// PDF with custom trigger
<FileViewer
  files={["https://example.com/report.pdf"]}
  headerTitle="Annual Report"
  mode="pdf"
  triggerButton={<Button variant="primary">View Report</Button>}
/>
```

## Advanced Features

### Zoom and Pan Controls

**Zoom Control System:**

- **Slider Range**: 0-100% zoom level (0% = fit-to-container, 100% = maximum zoom)
- **Zoom Buttons**: Increment/decrement by 5% steps
- **Pan Functionality**: Mouse drag to pan when zoomed (zoom > 0%)
- **Cursor States**: Grab cursor when zoomed, grabbing when panning
- **Auto Reset**: Pan position resets when zoom returns to 0%

```tsx
// Zoom controls are automatically included
<FileViewer
  files={imageUrls}
  headerTitle="Zoomable Gallery"
  // Zoom controls appear in bottom-right corner
  // - Minus button (disabled at 0%)
  // - Zoom slider (0-100%)
  // - Plus button (disabled at 100%)
/>
```

### Navigation and Selection

**Keyboard Navigation:**

- **Arrow Keys**: Up/Down in thumbnail sidebar to navigate files
- **Enter/Space**: Select focused thumbnail
- **Tab Navigation**: Focus management across interactive elements
- **Screen Reader**: Comprehensive ARIA attributes and announcements

**Mouse Navigation:**

- **Thumbnail Click**: Select any file from sidebar
- **Navigation Buttons**: Previous/next buttons (image mode only)
- **Wheel/Touch**: Scroll in PDF mode to navigate pages

```tsx
// Navigation with callbacks
<FileViewer
  files={multipleImages}
  headerTitle="Navigable Gallery"
  onFileSelect={(file, index) => {
    // Track file selection
    analytics.track("file_selected", { index, fileName: file });
  }}
  // Navigation shows: "3/10" counter between prev/next buttons
/>
```

### Custom Trigger Buttons

**Default Trigger**: Modal component generates a button with `buttonTitle` text

**Custom Trigger**: Full control over the modal trigger element

```tsx
// Custom trigger button
<FileViewer
  files={imageUrls}
  headerTitle="Custom Gallery"
  triggerButton={
    <div className="flex items-center gap-2 p-3 border rounded">
      <ImageIcon />
      <span>Open Gallery</span>
      <Badge>{imageUrls.length}</Badge>
    </div>
  }
/>

// Icon-only trigger
<FileViewer
  files={pdfFiles}
  mode="pdf"
  triggerButton={<IconButton icon={<FileIcon />} />}
/>
```

### Custom Footer Actions

Replace or extend the default download button with custom action buttons.

```tsx
// Custom footer with multiple actions
<FileViewer
  files={imageUrls}
  headerTitle="Gallery with Actions"
  footerIcons={
    <div className="flex gap-2">
      <IconButton icon={<ShareIcon />} onClick={handleShare} />
      <IconButton icon={<EditIcon />} onClick={handleEdit} />
      <IconButton icon={<DeleteIcon />} onClick={handleDelete} />
      <IconButton icon={<DownloadIcon />} onClick={handleDownload} />
    </div>
  }
/>

// Custom download behavior
<FileViewer
  files={protectedImages}
  headerTitle="Protected Gallery"
  footerIcons={
    <Button
      onClick={() => requestDownloadPermission()}
      variant="tertiary"
      size="sm"
    >
      Request Download
    </Button>
  }
/>
```

## Real-World Usage Examples

### Product Image Gallery

```tsx
const ProductImageViewer = ({ product }) => {
  const handleImageSelect = (imageUrl, index) => {
    // Track which product image was viewed
    analytics.track("product_image_viewed", {
      productId: product.id,
      imageIndex: index,
      imageUrl,
    });
  };

  const handleImageDownload = imageUrl => {
    // High-resolution download
    const highResUrl = imageUrl.replace("w_400", "w_1920");
    downloadFile(highResUrl, `${product.name}-image-${Date.now()}.jpg`);
  };

  return (
    <FileViewer
      files={product.images}
      headerTitle={`${product.name} - Images`}
      mode="image"
      triggerButton={
        <Button variant="secondary" size="sm">
          View Images ({product.images.length})
        </Button>
      }
      onFileSelect={handleImageSelect}
      onDownload={handleImageDownload}
    />
  );
};
```

### Document Management System

```tsx
const DocumentViewer = ({ document }) => {
  const [isLoading, setIsLoading] = useState(false);

  const handleDocumentDownload = async fileUrl => {
    setIsLoading(true);
    try {
      // Log download activity
      await logDocumentAccess(document.id, "download");

      // Trigger secure download
      window.open(`/api/documents/${document.id}/download`, "_blank");
    } catch (error) {
      showErrorToast("Download failed");
    } finally {
      setIsLoading(false);
    }
  };

  return (
    <FileViewer
      files={[document.pdfUrl]}
      headerTitle={`${document.title} - ${document.type}`}
      mode="pdf"
      buttonTitle="View Document"
      onDownload={handleDocumentDownload}
      footerIcons={
        <div className="flex gap-2">
          <IconButton
            icon={<PrintIcon />}
            onClick={() => window.print()}
            disabled={!document.allowPrint}
          />
          <IconButton
            icon={<DownloadIcon />}
            onClick={handleDocumentDownload}
            loading={isLoading}
            disabled={!document.allowDownload}
          />
        </div>
      }
    />
  );
};
```

### Media Upload Preview

```tsx
const MediaUploadPreview = ({ uploadedFiles, onRemove }) => {
  const [selectedFile, setSelectedFile] = useState(null);

  const fileUrls = uploadedFiles.map(file =>
    file.type.startsWith("image/") ? URL.createObjectURL(file) : file.pdfUrl
  );

  const handleFileSelect = (fileUrl, index) => {
    setSelectedFile(uploadedFiles[index]);
  };

  const handleRemoveFile = () => {
    if (selectedFile) {
      onRemove(selectedFile);
    }
  };

  return (
    <FileViewer
      files={fileUrls}
      headerTitle="Uploaded Files Preview"
      mode={uploadedFiles[0]?.type === "application/pdf" ? "pdf" : "image"}
      triggerButton={
        <Button variant="outline" size="sm">
          Preview Files ({uploadedFiles.length})
        </Button>
      }
      onFileSelect={handleFileSelect}
      footerIcons={
        <div className="flex gap-2">
          <IconButton icon={<DeleteIcon />} onClick={handleRemoveFile} disabled={!selectedFile} />
          <IconButton
            icon={<DownloadIcon />}
            onClick={() => selectedFile && downloadFile(selectedFile)}
          />
        </div>
      }
    />
  );
};
```

## Accessibility Features

### Keyboard Navigation

**Focus Management:**

- **Initial Focus**: Set to selected thumbnail when modal opens
- **Tab Order**: Logical flow through thumbnails → navigation → zoom controls → actions
- **Arrow Keys**: Navigate between thumbnails in sidebar
- **Enter/Space**: Activate focused thumbnail or control
- **Escape**: Close modal (inherited from Modal component)

### Screen Reader Support

**ARIA Attributes:**

- **Thumbnails**: `role="button"`, `aria-label` with file info, `aria-selected` state
- **Navigation**: Counter with `aria-live="polite"` for selection announcements
- **Zoom Controls**: `role="group"` with `aria-label="Zoom controls"`
- **Current State**: Dynamic announcements for zoom level and file selection

**Content Descriptions:**

- **Image Mode**: "Image 1 of 5", "Selected image 3"
- **PDF Mode**: "Page 1", "PDF page 3 of 10"
- **Zoom Level**: "Zoom level 25%", "Maximum zoom reached"

### Visual Accessibility

**Focus Indicators:**

- **Thumbnails**: 4px primary color ring on focus/selection
- **Controls**: Standard focus outlines with sufficient contrast
- **Interactive States**: Clear hover and active states

**Color and Contrast:**

- **Selection Ring**: Primary color (`var(--gd-primary-50)`) with 4px width
- **Background**: Neutral gray (`var(--gd-neutral-grey-20)`) for image container
- **Text**: High contrast text colors from Genesis token system

## Design System Integration

### Genesis Design Tokens Used

**Colors:**

- `var(--gd-primary-50)`: Selection ring and primary accents
- `var(--gd-neutral-grey-20)`: Image viewer background
- `var(--gd-neutral-grey-80)`: Primary text color
- `var(--gd-text-subdued-1)`: Secondary text and metadata

**Spacing:**

- `gd-8`: Gap between PDF thumbnails and page numbers
- `gd-12`: Gap between main viewer elements, padding for PDF container
- `gd-16`: Gap between thumbnail items (image mode), main viewer padding
- `gd-24`: Sidebar padding for thumbnail container

**Typography:**

- `text-en-desktop-body-s`: File metadata, counter, and secondary text
- `text-en-desktop-body-m`: Loading and error messages
- `font-400`: Regular weight for page numbers and metadata

**Border Radius:**

- `rounded-gd-8`: Thumbnails and main viewer container

### Component Dependencies

**Required Components:**

- **Modal**: Provides the base modal functionality and layout
- **Scrollbar**: Custom scrollbar for sidebar and PDF viewer
- **IconButton**: Navigation, zoom, and action buttons
- **Slider**: Zoom level control slider

**External Dependencies:**

- **pdfjs-dist**: PDF processing and image conversion
- **React**: Core component framework with hooks

## Performance Considerations

### PDF Processing

**Image Conversion:**

- **On-Demand**: PDF pages converted to images when modal opens
- **Quality Settings**: Optimized for display with configurable DPI
- **Memory Management**: Automatic cleanup of generated image URLs
- **Error Handling**: Graceful fallback for unsupported PDF files

### Image Loading

**Optimization:**

- **Lazy Loading**: Images loaded as needed in thumbnail sidebar
- **Drag Prevention**: `draggable={false}` on all images
- **Load Events**: Dimension calculation and orientation detection
- **Error Boundaries**: Fallback UI for failed image loads

### Zoom and Pan Performance

**Smooth Interactions:**

- **CSS Transforms**: Hardware-accelerated zoom and pan
- **Transition Control**: Smooth transitions except during active panning
- **Event Throttling**: Optimized mouse move handlers
- **Memory Cleanup**: Automatic cleanup of event listeners

## Browser Support

**Modern Browser Features:**

- **IntersectionObserver**: PDF page tracking (with fallback)
- **ResizeObserver**: Responsive image sizing
- **CSS Transforms**: Zoom and pan functionality
- **File API**: PDF processing and image handling

**Accessibility Support:**

- **Screen Readers**: NVDA, JAWS, VoiceOver compatibility
- **Keyboard Navigation**: Full keyboard accessibility
- **High Contrast**: Respects system color preferences
- **Reduced Motion**: Honors `prefers-reduced-motion` settings

## Best Practices

### File Management

**Image Files:**

- **Format Support**: JPEG, PNG, WebP, GIF
- **Size Optimization**: Recommend compressed images for web display
- **Resolution**: Provide sufficient resolution for zoom functionality
- **Alt Text**: Include descriptive alt attributes

**PDF Files:**

- **File Size**: Consider performance impact of large PDFs
- **Security**: Ensure PDFs are from trusted sources
- **Compression**: Use optimized PDFs for web delivery
- **Permissions**: Respect PDF security settings

### User Experience

**Performance:**

- **Loading States**: Show loading indicators for PDF processing
- **Error Handling**: Provide clear error messages for failed loads
- **Progressive Enhancement**: Ensure basic functionality without JavaScript
- **Mobile Optimization**: Consider touch gestures and viewport constraints

**Interaction Design:**

- **Clear Navigation**: Provide obvious next/previous controls
- **Zoom Feedback**: Show zoom level and pan capabilities
- **File Context**: Display file information and metadata
- **Download Options**: Make download functionality discoverable

### Integration Patterns

**Form Integration:**

```tsx
// File upload with preview
const FileUploadField = ({ field, form }) => {
  return (
    <div>
      <FileUploader onUpload={field.onChange} />
      {field.value?.length > 0 && (
        <FileViewer
          files={field.value}
          headerTitle="Uploaded Files"
          triggerButton={<Button variant="outline">Preview</Button>}
        />
      )}
    </div>
  );
};
```

**Data Loading:**

```tsx
// Async file loading
const AsyncFileViewer = ({ documentId }) => {
  const [files, setFiles] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    loadDocumentFiles(documentId)
      .then(setFiles)
      .finally(() => setLoading(false));
  }, [documentId]);

  if (loading) return <Skeleton />;

  return (
    <FileViewer
      files={files}
      headerTitle="Document Files"
      mode={files[0]?.endsWith(".pdf") ? "pdf" : "image"}
    />
  );
};
```

## Troubleshooting

### Common Issues

**PDF Not Loading:**

- Verify PDF URL is accessible and CORS-enabled
- Check if PDF is password-protected or corrupted
- Ensure PDF.js library is properly loaded

**Images Not Displaying:**

- Confirm image URLs are valid and accessible
- Check for CORS restrictions on image domains
- Verify image format compatibility

**Zoom Not Working:**

- Ensure images have loaded completely
- Check if zoom controls are enabled
- Verify container dimensions are calculated

**Performance Issues:**

- Reduce PDF file size or image dimensions
- Implement lazy loading for large galleries
- Consider pagination for extensive file collections

### Migration Notes

**From Previous Versions:**

- Update import paths if component location changed
- Review prop names for any breaking changes
- Test keyboard navigation and accessibility features
- Verify PDF processing functionality

Remember: The File Viewer component provides a comprehensive solution for displaying images and PDFs with advanced features like zoom, pan, and navigation. Always test with real file types and sizes that match your production environment.
