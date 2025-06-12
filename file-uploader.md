# File Uploader Component

## Overview

The File Uploader component provides a comprehensive and accessible file upload interface built with Genesis Design System tokens. It supports multiple upload methods including drag-and-drop, file selection, and URL submission, with extensive customization options for layout, validation, file status tracking, and user experience optimization. The component is designed for both single and multi-file upload scenarios with complete accessibility support.

## Component API

### FileUpload Props

| Prop                | Type                         | Default                                    | Description                                          |
| ------------------- | ---------------------------- | ------------------------------------------ | ---------------------------------------------------- |
| files               | `FileWithStatus[]`           | `[]`                                       | Array of files with their upload status information  |
| onFileChange        | `(files: File[]) => void`    | -                                          | Callback when files are added or removed             |
| onUrlSubmit         | `(url: string) => void`      | -                                          | Optional callback for URL submissions                |
| onRetry             | `() => void`                 | -                                          | Optional callback for retry attempts                 |
| layout              | `"vertical" \| "horizontal"` | `"vertical"`                               | Layout orientation of the uploader interface         |
| uploadMode          | `"single" \| "multi"`        | `"multi"`                                  | Single file or multiple files upload mode            |
| titleText           | `string`                     | `"Drag and drop your file here"`           | Primary text displayed in the dropzone               |
| otherText           | `string`                     | `"Supported Format: XLS, XLSX, CSV (5MB)"` | Secondary descriptive text in the dropzone           |
| maxSize             | `number`                     | `5 * 1024 * 1024`                          | Maximum file size in bytes (5MB default)             |
| maxFilesHeight      | `string`                     | `"151px"`                                  | Maximum height of the files list container           |
| allowedFileTypes    | `string[]`                   | `[".xls", ".xlsx", ".csv"]`                | Array of allowed file extensions                     |
| maxFileCount        | `number`                     | -                                          | Maximum number of files for multi-upload mode        |
| errors              | `string \| string[]`         | -                                          | External error message(s) to display                 |
| disabled            | `boolean`                    | `false`                                    | Whether the component is disabled                    |
| showHeader          | `boolean`                    | `false`                                    | Whether to show the header section                   |
| showHelpIcon        | `boolean`                    | `false`                                    | Whether to show the help icon in the header          |
| showMandatory       | `boolean`                    | `false`                                    | Whether to show the mandatory asterisk in the header |
| showFileCount       | `boolean`                    | `false`                                    | Whether to show the file count in the header         |
| headerText          | `string`                     | -                                          | Text to display in the header                        |
| fileCountText       | `string`                     | -                                          | Text to display for file count in the header         |
| supportText         | `string`                     | -                                          | Support text displayed below the uploader            |
| isSingleUploadSmall | `boolean`                    | `false`                                    | Whether the single upload uses compact size variant  |

### FileWithStatus Interface

```tsx
interface FileWithStatus {
  /** The actual File object */
  file: File;
  /** Current upload status */
  validationStatus: "uploading" | "uploaded" | "failed";
  /** Upload progress percentage (0-100) */
  progress?: number;
  /** Validation error message */
  validationText?: string;
}
```

### Extended Features

The component extends standard dropzone functionality and supports:

- React Dropzone integration for drag-and-drop
- File validation with custom rules
- Progress tracking for uploads
- Status indicators with visual feedback
- Icon-based file type recognition
- URL submission with popover interface

## Import

```tsx
import { FileUpload } from "gends";

```

## Layout Variants

### Vertical Layout (Default)

The vertical layout provides a prominent, centered upload interface ideal for primary upload flows.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  layout="vertical"
  uploadMode="multi"
  titleText="Drag and drop your file here"
  otherText="Supported Format: XLS, XLSX, CSV (5MB)"
/>
```

**Characteristics:**

- **Structure**: Cloud icon, title text, description, and action buttons stacked vertically
- **Dropzone**: Large rectangular area with dashed border
- **Visual Hierarchy**: Prominent cloud upload icon with clear text hierarchy
- **Use Cases**: Primary upload flows, form sections, document management

### Horizontal Layout

The horizontal layout provides a compact, inline upload interface for constrained spaces.

```tsx
<FileUpload files={files} onFileChange={handleFileChange} layout="horizontal" uploadMode="multi" />
```

**Characteristics:**

- **Structure**: Upload button, descriptive text, and URL link arranged horizontally
- **Dropzone**: Compact rectangular area with centered content
- **Space Efficiency**: Reduced vertical space requirement
- **Use Cases**: Inline forms, compact interfaces, secondary upload options

## Upload Mode Variants

### Multi-File Upload

Allows uploading multiple files simultaneously with comprehensive file management.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  uploadMode="multi"
  maxFileCount={5}
  maxSize={10 * 1024 * 1024}
/>
```

**Features:**

- **File Selection**: Multiple files can be dropped or selected simultaneously
- **File Management**: Individual file removal and status tracking
- **Progress Tracking**: Per-file upload progress and status indicators
- **Validation**: Individual file validation with error reporting

### Single File Upload

Designed for scenarios requiring exactly one file upload.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  uploadMode="single"
  titleText="Select a document"
  otherText="PDF, DOC, or DOCX files only"
/>
```

**Features:**

- **File Replacement**: New file selection replaces the existing file
- **Simplified Interface**: Streamlined UI for single-file scenarios
- **Focused Validation**: Single file validation and error handling

### Compact Single Upload

A smaller variant of single upload for space-constrained interfaces.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  uploadMode="single"
  isSingleUploadSmall={true}
/>
```

**Features:**

- **Reduced Height**: Compact vertical footprint
- **Simplified Controls**: Essential upload functionality only
- **Space Efficient**: Ideal for inline or sidebar placements

## File Status States

### Uploading State

Shows active upload progress with visual feedback.

```tsx
const uploadingFiles = [
  {
    file: new File(["content"], "document.pdf", { type: "application/pdf" }),
    validationStatus: "uploading",
    progress: 45,
  },
];

<FileUpload files={uploadingFiles} onFileChange={handleFileChange} uploadMode="multi" />;
```

**Visual Elements:**

- **Progress Bar**: Animated progress indicator (0-100%)
- **Status Text**: "Uploading..." with percentage
- **Icon**: File type icon with uploading indicator
- **Cancel Option**: Ability to cancel ongoing upload

### Uploaded State

Indicates successful file upload completion.

```tsx
const uploadedFiles = [
  {
    file: new File(["content"], "document.pdf", { type: "application/pdf" }),
    validationStatus: "uploaded",
    progress: 100,
  },
];

<FileUpload files={uploadedFiles} onFileChange={handleFileChange} uploadMode="multi" />;
```

**Visual Elements:**

- **Success Indicator**: Green checkmark icon
- **Completion Status**: "Uploaded" or similar success message
- **File Information**: File name, size, and type
- **Remove Option**: Ability to remove successfully uploaded file

### Failed State

Shows upload failure with retry mechanism.

```tsx
const failedFiles = [
  {
    file: new File(["content"], "document.pdf", { type: "application/pdf" }),
    validationStatus: "failed",
    validationText: "Upload failed due to network error",
  },
];

<FileUpload
  files={failedFiles}
  onFileChange={handleFileChange}
  onRetry={() => console.log("Retrying upload")}
  uploadMode="multi"
/>;
```

**Visual Elements:**

- **Error Indicator**: Red error icon
- **Error Message**: Specific failure reason
- **Retry Button**: Option to retry the failed upload
- **Remove Option**: Ability to remove failed file

## File Validation

### File Type Validation

Control allowed file types using the `allowedFileTypes` prop.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  allowedFileTypes={[".jpg", ".jpeg", ".png", ".gif"]}
  titleText="Upload Images"
  otherText="Supported formats: JPG, PNG, GIF (5MB max)"
/>
```

**Common File Type Groups:**

```tsx
// Documents
allowedFileTypes={[".pdf", ".doc", ".docx", ".txt"]}

// Spreadsheets
allowedFileTypes={[".xls", ".xlsx", ".csv"]}

// Images
allowedFileTypes={[".jpg", ".jpeg", ".png", ".gif", ".svg"]}

// Archives
allowedFileTypes={[".zip", ".rar", ".7z"]}
```

### File Size Validation

Set maximum file size limits with clear user feedback.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  maxSize={10 * 1024 * 1024} // 10MB
  otherText="Maximum file size: 10MB"
/>
```

**Size Calculations:**

```tsx
// Common size limits
const sizes = {
  "1MB": 1 * 1024 * 1024,
  "5MB": 5 * 1024 * 1024,
  "10MB": 10 * 1024 * 1024,
  "50MB": 50 * 1024 * 1024,
  "100MB": 100 * 1024 * 1024,
};
```

### Custom Validation with Zod

Implement complex validation rules using Zod schemas.

```tsx
import { z } from "zod";

const documentSchema = z.object({
  file: z
    .instanceof(File)
    .refine(file => file.size <= 5 * 1024 * 1024, "File must be under 5MB")
    .refine(
      file => ["application/pdf", "application/msword"].includes(file.type),
      "Only PDF and DOC files are allowed"
    )
    .refine(file => !file.name.includes(" "), "File name cannot contain spaces"),
});

<FileUpload
  files={files}
  onFileChange={handleFileChange}
  zodSchema={documentSchema}
  errors="File validation failed"
/>;
```

## Advanced Features

### URL Submission

Enable users to upload files from URLs with integrated popover interface.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  onUrlSubmit={url => {
    console.log("URL submitted:", url);
    // Fetch file from URL and add to files
    fetchFileFromUrl(url).then(file => {
      const fileWithStatus = {
        file,
        validationStatus: "uploading",
        progress: 0,
      };
      setFiles(prev => [...prev, fileWithStatus]);
    });
  }}
  uploadMode="multi"
/>
```

**URL Submission Features:**

- **Popover Interface**: Modal-like URL input with validation
- **URL Validation**: Basic URL format validation
- **Integration**: Seamless integration with file upload flow
- **Error Handling**: URL fetch error management

### Header Configuration

Add descriptive headers with help icons and file count information.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  showHeader={true}
  showHelpIcon={true}
  showMandatory={true}
  showFileCount={true}
  headerText="Upload Required Documents"
  fileCountText="Maximum 5 files allowed"
  supportText="Upload all required documents for processing"
/>
```

**Header Elements:**

- **Header Text**: Primary header description
- **Help Icon**: Contextual help information
- **Mandatory Indicator**: Asterisk for required fields
- **File Count**: Current/maximum file count display

### Custom Height Control

Control the maximum height of the file list container.

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  uploadMode="multi"
  maxFilesHeight="300px"
/>
```

**Height Management:**

- **Scrollable Container**: Automatic scrolling for overflow
- **Responsive Design**: Adapts to container constraints
- **Performance**: Virtualization for large file lists

## Real-World Usage Examples

### Document Management System

```tsx
const DocumentUploader = () => {
  const [files, setFiles] = useState<FileWithStatus[]>([]);
  const [isUploading, setIsUploading] = useState(false);

  const handleFileChange = async (newFiles: File[]) => {
    const filesWithStatus = newFiles.map(file => ({
      file,
      validationStatus: "uploading" as const,
      progress: 0,
    }));

    setFiles(prev => [...prev, ...filesWithStatus]);
    setIsUploading(true);

    // Simulate upload process
    for (const fileWithStatus of filesWithStatus) {
      try {
        await uploadFile(fileWithStatus.file, progress => {
          setFiles(prev =>
            prev.map(f => (f.file === fileWithStatus.file ? { ...f, progress } : f))
          );
        });

        setFiles(prev =>
          prev.map(f =>
            f.file === fileWithStatus.file
              ? { ...f, validationStatus: "uploaded", progress: 100 }
              : f
          )
        );
      } catch (error) {
        setFiles(prev =>
          prev.map(f =>
            f.file === fileWithStatus.file
              ? {
                  ...f,
                  validationStatus: "failed",
                  validationText: "Upload failed",
                }
              : f
          )
        );
      }
    }
    setIsUploading(false);
  };

  return (
    <div className="space-y-4">
      <FileUpload
        files={files}
        onFileChange={handleFileChange}
        uploadMode="multi"
        maxFileCount={10}
        allowedFileTypes={[".pdf", ".doc", ".docx"]}
        maxSize={25 * 1024 * 1024} // 25MB
        showHeader={true}
        headerText="Upload Documents"
        showFileCount={true}
        fileCountText="Up to 10 documents allowed"
        supportText="Accepted formats: PDF, DOC, DOCX (max 25MB each)"
      />
    </div>
  );
};
```

### Image Gallery Upload

```tsx
const ImageGalleryUploader = () => {
  const [images, setImages] = useState<FileWithStatus[]>([]);

  const handleImageChange = (newFiles: File[]) => {
    const imageFiles = newFiles.map(file => ({
      file,
      validationStatus: "uploading" as const,
      progress: 0,
    }));

    setImages(prev => [...prev, ...imageFiles]);

    // Process each image
    imageFiles.forEach(async imageFile => {
      try {
        const compressedFile = await compressImage(imageFile.file);
        await uploadToGallery(compressedFile);

        setImages(prev =>
          prev.map(img =>
            img.file === imageFile.file
              ? { ...img, validationStatus: "uploaded", progress: 100 }
              : img
          )
        );
      } catch (error) {
        setImages(prev =>
          prev.map(img =>
            img.file === imageFile.file
              ? {
                  ...img,
                  validationStatus: "failed",
                  validationText: "Image upload failed",
                }
              : img
          )
        );
      }
    });
  };

  return (
    <FileUpload
      files={images}
      onFileChange={handleImageChange}
      uploadMode="multi"
      allowedFileTypes={[".jpg", ".jpeg", ".png", ".gif", ".webp"]}
      maxSize={10 * 1024 * 1024} // 10MB
      titleText="Upload Images to Gallery"
      otherText="Supported formats: JPG, PNG, GIF, WebP (10MB max)"
      maxFilesHeight="400px"
    />
  );
};
```

### CSV Data Import

```tsx
const CSVImporter = () => {
  const [csvFile, setCsvFile] = useState<FileWithStatus[]>([]);

  const handleCSVUpload = async (files: File[]) => {
    if (files.length === 0) return;

    const file = files[0];
    const fileWithStatus = {
      file,
      validationStatus: "uploading" as const,
      progress: 0,
    };

    setCsvFile([fileWithStatus]);

    try {
      // Validate CSV structure
      const csvContent = await file.text();
      const isValidCSV = validateCSVStructure(csvContent);

      if (!isValidCSV) {
        throw new Error("Invalid CSV structure");
      }

      // Process CSV data
      await processCSVData(csvContent);

      setCsvFile(prev =>
        prev.map(f => ({
          ...f,
          validationStatus: "uploaded",
          progress: 100,
        }))
      );
    } catch (error) {
      setCsvFile(prev =>
        prev.map(f => ({
          ...f,
          validationStatus: "failed",
          validationText: error.message,
        }))
      );
    }
  };

  return (
    <FileUpload
      files={csvFile}
      onFileChange={handleCSVUpload}
      uploadMode="single"
      allowedFileTypes={[".csv"]}
      maxSize={50 * 1024 * 1024} // 50MB
      titleText="Import CSV Data"
      otherText="Select a CSV file with your data (max 50MB)"
      showHeader={true}
      headerText="Data Import"
      supportText="CSV must include headers in the first row"
    />
  );
};
```

### Profile Avatar Upload

```tsx
const AvatarUploader = () => {
  const [avatar, setAvatar] = useState<FileWithStatus[]>([]);

  const handleAvatarUpload = (files: File[]) => {
    const file = files[0];
    const fileWithStatus = {
      file,
      validationStatus: "uploading" as const,
      progress: 0,
    };

    setAvatar([fileWithStatus]);

    // Upload avatar with image processing
    uploadAvatar(file)
      .then(() => {
        setAvatar(prev =>
          prev.map(f => ({
            ...f,
            validationStatus: "uploaded",
            progress: 100,
          }))
        );
      })
      .catch(() => {
        setAvatar(prev =>
          prev.map(f => ({
            ...f,
            validationStatus: "failed",
            validationText: "Avatar upload failed",
          }))
        );
      });
  };

  return (
    <div className="max-w-md">
      <FileUpload
        files={avatar}
        onFileChange={handleAvatarUpload}
        uploadMode="single"
        isSingleUploadSmall={true}
        allowedFileTypes={[".jpg", ".jpeg", ".png"]}
        maxSize={2 * 1024 * 1024} // 2MB
        titleText="Upload Avatar"
        otherText="JPG or PNG (max 2MB)"
      />
    </div>
  );
};
```

### Bulk File Upload with Progress

```tsx
const BulkUploader = () => {
  const [files, setFiles] = useState<FileWithStatus[]>([]);

  const handleBulkUpload = (newFiles: File[]) => {
    const filesWithStatus = newFiles.map(file => ({
      file,
      validationStatus: "uploading" as const,
      progress: 0,
    }));

    setFiles(prev => [...prev, ...filesWithStatus]);

    // Upload files with individual progress tracking
    filesWithStatus.forEach(fileWithStatus => {
      const uploadPromise = uploadWithProgress(fileWithStatus.file, progress => {
        setFiles(prev => prev.map(f => (f.file === fileWithStatus.file ? { ...f, progress } : f)));
      });

      uploadPromise
        .then(() => {
          setFiles(prev =>
            prev.map(f =>
              f.file === fileWithStatus.file
                ? { ...f, validationStatus: "uploaded", progress: 100 }
                : f
            )
          );
        })
        .catch(error => {
          setFiles(prev =>
            prev.map(f =>
              f.file === fileWithStatus.file
                ? {
                    ...f,
                    validationStatus: "failed",
                    validationText: error.message,
                  }
                : f
            )
          );
        });
    });
  };

  const handleRetry = () => {
    const failedFiles = files.filter(f => f.validationStatus === "failed");
    handleBulkUpload(failedFiles.map(f => f.file));
  };

  return (
    <FileUpload
      files={files}
      onFileChange={handleBulkUpload}
      onRetry={handleRetry}
      uploadMode="multi"
      maxFileCount={20}
      maxFilesHeight="500px"
      showHeader={true}
      showFileCount={true}
      headerText="Bulk File Upload"
      fileCountText={`${files.length}/20 files`}
    />
  );
};
```

## Accessibility Features

### Keyboard Navigation

The component provides comprehensive keyboard accessibility:

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  // Automatically includes:
  // - Tab navigation for all interactive elements
  // - Enter/Space activation for buttons
  // - Arrow key navigation within file lists
  // - Escape key to close popovers
/>
```

### Screen Reader Support

- **ARIA Labels**: Descriptive labels for all interactive elements
- **Status Announcements**: Upload progress and completion announcements
- **Error Communication**: Clear error message association
- **File Information**: Accessible file details and status

### Focus Management

- **Focus Indicators**: Clear visual focus states
- **Focus Trapping**: Modal popover focus management
- **Tab Order**: Logical keyboard navigation sequence
- **Focus Restoration**: Returns focus after modal interactions

## Design Token Specifications

### Color System

| State    | Background Token                 | Border Token                   | Text Token                |
| -------- | -------------------------------- | ------------------------------ | ------------------------- |
| Default  | `bg-color-background-surface-10` | `border-color-neutral-grey-40` | `text-color-text-default` |
| Hover    | `bg-color-background-surface-20` | `border-color-neutral-grey-40` | `text-color-text-default` |
| Active   | `bg-color-primary-10`            | `border-color-primary-40`      | `text-color-primary-50`   |
| Disabled | `bg-color-neutral-grey-10`       | `border-color-neutral-grey-40` | `disabled-text`           |

### Status Colors

| Status    | Icon Background                | Icon Color                       | Progress Color                 |
| --------- | ------------------------------ | -------------------------------- | ------------------------------ |
| Uploading | `bg-color-primary-20`          | `text-color-primary-50`          | `bg-color-primary-50`          |
| Uploaded  | `bg-color-feedback-success-20` | `text-color-feedback-success-50` | `bg-color-feedback-success-50` |
| Failed    | `bg-color-feedback-error-20`   | `text-color-feedback-error-50`   | `bg-color-feedback-error-50`   |

### Typography Scale

| Element     | Typography Token            | Font Size | Line Height |
| ----------- | --------------------------- | --------- | ----------- |
| Title Text  | `text-en-desktop-heading-l` | 18px      | 24px        |
| Description | `text-en-desktop-body-s`    | 12px      | 16px        |
| File Names  | `text-en-desktop-body-m`    | 14px      | 20px        |
| Status Text | `text-en-desktop-body-s`    | 12px      | 16px        |

### Spacing System

| Element           | Spacing Token   | Value |
| ----------------- | --------------- | ----- |
| Container Padding | `p-gd-20`       | 20px  |
| Content Gap       | `gap-gd-12`     | 12px  |
| File List Gap     | `gap-gd-8`      | 8px   |
| Border Radius     | `rounded-gd-16` | 16px  |

### Icon Specifications

| Icon Type    | Size | Context             |
| ------------ | ---- | ------------------- |
| Upload Cloud | 28px | Main dropzone icon  |
| File Type    | 28px | File list icons     |
| Status       | 16px | Upload status icons |
| Action       | 16px | Button icons        |

## Best Practices

### When to Use

**Multi-File Upload:**

- Document management systems
- Media galleries
- Bulk data processing
- Archive uploads

**Single File Upload:**

- Profile avatars
- Document replacement
- Configuration files
- Single data imports

**Compact Single Upload:**

- Inline forms
- Profile settings
- Quick file replacement
- Space-constrained interfaces

### Performance Considerations

- **File Size Limits**: Set appropriate maximum file sizes
- **Concurrent Uploads**: Limit simultaneous upload connections
- **Progress Tracking**: Implement efficient progress reporting
- **Memory Management**: Handle large files with streaming
- **Error Handling**: Provide robust error recovery mechanisms

### Validation Guidelines

- **Client-Side Validation**: Immediate feedback for file type and size
- **Server-Side Validation**: Comprehensive security validation
- **User Feedback**: Clear error messages and validation states
- **File Sanitization**: Secure file processing practices

### User Experience Guidelines

- **Clear Instructions**: Descriptive text for supported formats and limits
- **Visual Feedback**: Immediate response to user actions
- **Progress Indication**: Real-time upload progress and status
- **Error Recovery**: Easy retry mechanisms for failed uploads
- **Accessibility**: Full keyboard and screen reader support

## Integration Examples

### With Form Libraries

```tsx
import { useForm, Controller } from "react-hook-form";

const FormWithFileUpload = () => {
  const { control, handleSubmit } = useForm();

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Controller
        name="documents"
        control={control}
        render={({ field }) => (
          <FileUpload
            files={field.value || []}
            onFileChange={files => {
              const filesWithStatus = files.map(file => ({
                file,
                validationStatus: "uploaded" as const,
                progress: 100,
              }));
              field.onChange(filesWithStatus);
            }}
            uploadMode="multi"
            showHeader={true}
            headerText="Required Documents"
            showMandatory={true}
          />
        )}
      />
    </form>
  );
};
```

### With State Management

```tsx
// Redux Toolkit example
const fileUploadSlice = createSlice({
  name: "fileUpload",
  initialState: {
    files: [],
    isUploading: false,
    error: null,
  },
  reducers: {
    startUpload: (state, action) => {
      state.files = action.payload;
      state.isUploading = true;
      state.error = null;
    },
    updateProgress: (state, action) => {
      const { fileId, progress } = action.payload;
      const file = state.files.find(f => f.id === fileId);
      if (file) {
        file.progress = progress;
      }
    },
    uploadComplete: (state, action) => {
      const { fileId } = action.payload;
      const file = state.files.find(f => f.id === fileId);
      if (file) {
        file.validationStatus = "uploaded";
        file.progress = 100;
      }
    },
    uploadFailed: (state, action) => {
      const { fileId, error } = action.payload;
      const file = state.files.find(f => f.id === fileId);
      if (file) {
        file.validationStatus = "failed";
        file.validationText = error;
      }
    },
  },
});
```

## Troubleshooting

### Common Issues

**Files Not Uploading:**

- Verify `onFileChange` callback is properly implemented
- Check file size and type restrictions
- Ensure server endpoint is accessible
- Validate file validation logic

**Validation Errors:**

- Check `allowedFileTypes` array format
- Verify `maxSize` value is in bytes
- Ensure Zod schema validation logic
- Review custom validation functions

**Progress Not Updating:**

- Implement proper progress tracking in upload function
- Update file status using `setFiles` state updater
- Ensure progress values are between 0-100
- Check for race conditions in state updates

**UI Issues:**

- Verify all required props are provided
- Check container styling and layout constraints
- Ensure proper CSS imports for component styling
- Review responsive design considerations

### Migration Notes

When upgrading from previous versions:

- File interface now requires `validationStatus` field
- Progress tracking requires explicit progress updates
- Layout prop replaces deprecated styling props
- URL submission is now optional feature

Remember: The File Uploader component is designed to provide comprehensive file upload functionality while maintaining accessibility, performance, and user experience standards consistent with the Genesis Design System.
