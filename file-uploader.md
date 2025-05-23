# FileUploader Component

The FileUploader component provides a flexible interface for uploading files through drag-and-drop, file selection, or URL submission.

## Features

- Drag and drop file upload
- Multiple or single file upload modes
- File validation with Zod schema
- Upload progress tracking
- File type restrictions
- File size limits
- Upload status indicators
- Retry mechanism for failed uploads
- URL submission support
- Vertical and horizontal layouts
- Responsive design
- Support for custom headers and help text

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| files | FileWithStatus[] | [] | Array of files with their upload status |
| onFileChange | (files: File[]) => void | - | Callback when files are added or removed |
| onUrlSubmit | (url: string) => void | - | Optional callback for URL submissions |
| onRetry | () => void | - | Optional callback for retry attempts |
| layout | 'vertical' \| 'horizontal' | 'vertical' | Layout orientation of the uploader |
| uploadMode | 'single' \| 'multi' | 'multi' | Single or multiple file upload mode |
| titleText | string | 'Drag and drop your file here' | Main title text |
| otherText | string | 'Supported Format: XLS, XLSX, CSV (5MB)' | Supporting text |
| maxSize | number | 5 * 1024 * 1024 | Maximum file size in bytes (5MB default) |
| maxFilesHeight | string | '151px' | Maximum height of files list container |
| acceptedFileTypes | Record<string, string[]> | - | Accepted MIME types and extensions |
| zodSchema | z.ZodSchema | - | Optional Zod schema for file validation |
| disabled | boolean | false | Disables the file uploader |
| showHeader | boolean | false | Shows the header section |
| showHelpIcon | boolean | false | Shows help icon in header |
| showMandatory | boolean | false | Shows mandatory asterisk |
| showFileCount | boolean | false | Shows file count in header |
| headerText | string | - | Header text content |
| fileCountText | string | - | Text for file count display |
| supportText | string | - | Support text below uploader |
| isSingleUploadSmall | boolean | false | Enables compact single upload mode |

## File Status Interface

```typescript
interface FileWithStatus {
  file: File;                                    // The actual File object
  validationStatus: "uploading" | "uploaded" | "failed";   // Current upload status
  progress?: number;                             // Upload progress (0-100)
  validationText?: string;                       // Optional validation message
}
```

## Basic Usage

```tsx
import { FileUpload } from '@genesis/components';

function MyComponent() {
  const [files, setFiles] = useState<FileWithStatus[]>([]);

  const handleFileChange = (newFiles: File[]) => {
    // Convert File objects to FileWithStatus objects
    const filesWithStatus = newFiles.map(file => ({
      file,
      validationStatus: "uploading",
      progress: 0
    }));
    
    setFiles(filesWithStatus);
    // Handle file upload logic here
  };

  return (
    <FileUpload
      files={files}
      onFileChange={handleFileChange}
      uploadMode="multi"
      layout="vertical"
    />
  );
}
```

## File Validation Example

```tsx
import { z } from 'zod';

const zodSchema = z.object({
  file: z
    .instanceof(File)
    .refine((file) => file.size <= 5 * 1024 * 1024, "File must be under 5MB")
    .refine(
      (file) => ["text/csv", "application/vnd.ms-excel"].includes(file.type),
      "Only CSV and Excel files are allowed"
    )
});

<FileUpload
  files={files}
  onFileChange={handleFileChange}
  zodSchema={zodSchema}
  acceptedFileTypes={{
    "application/vnd.ms-excel": [".xls"],
    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet": [".xlsx"],
    "text/csv": [".csv"]
  }}
/>
```

## Variants

### 1. Default Multi-Upload

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  layout="vertical"
  uploadMode="multi"
/>
```

### 2. Single File Upload

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  layout="vertical"
  uploadMode="single"
  isSingleUploadSmall={false}
/>
```

### 3. Compact Single Upload

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  uploadMode="single"
  isSingleUploadSmall={true}
/>
```

### 4. With Header and Help Icon

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  showHeader={true}
  showHelpIcon={true}
  headerText="Upload Documents"
  showFileCount={true}
  fileCountText="Maximum 5 files allowed"
/>
```

### 5. Horizontal Layout

```tsx
<FileUpload
  files={files}
  onFileChange={handleFileChange}
  layout="horizontal"
  uploadMode="multi"
/>
```

## File States

The component handles different file states with appropriate visual feedback:

1. **Uploading**: Shows progress bar and upload percentage
2. **Uploaded**: Shows success state with checkmark
3. **Failed**: Shows error state with retry option

## Best Practices

1. Always provide feedback for file upload status
2. Implement proper error handling and validation
3. Use appropriate file type restrictions
4. Set reasonable file size limits
5. Provide clear instructions and supported file formats
6. Consider implementing retry mechanism for failed uploads
7. Show progress indication for large file uploads
8. Validate files both on client and server side

## Accessibility

- The component is keyboard accessible
- Provides clear focus states
- Includes proper ARIA labels
- Supports screen readers with status updates
- Provides clear error messages and validation feedback