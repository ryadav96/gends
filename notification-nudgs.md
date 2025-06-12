# Notification Nudge Component

## Overview

The Notification Nudge component is a flexible and accessible notification system built with Genesis Design System tokens. It provides a comprehensive set of features for displaying non-intrusive notifications (nudges or toasts) with multiple variants, positioning options, and interactive capabilities. The component is designed for various use cases such as success confirmations, error alerts, loading states, and general information messages.

## Component API

### Notification Options

| Prop            | Type                                                                                              | Default       | Description                                             |
| --------------- | ------------------------------------------------------------------------------------------------- | ------------- | ------------------------------------------------------- |
| title           | `string`                                                                                          | Required      | Main title text displayed on the notification           |
| description     | `string`                                                                                          | `undefined`   | Optional additional detail below the title              |
| variant         | `"info" \| "success" \| "error" \| "loading"`                                                     | `"info"`      | Visual style/type of notification                       |
| position        | `"top-left" \| "top-center" \| "top-right" \| "bottom-left" \| "bottom-center" \| "bottom-right"` | `"top-right"` | Screen position for notification                        |
| duration        | `number \| null`                                                                                  | `5000`        | Auto-dismiss duration in milliseconds (null for manual) |
| showProgressBar | `boolean`                                                                                         | `false`       | Whether to show progress bar for auto-dismiss           |
| showActions     | `boolean`                                                                                         | `false`       | Whether to show action buttons                          |
| customIcon      | `ReactNode`                                                                                       | `undefined`   | Custom icon to override default variant icon            |
| primaryAction   | `ActionConfig`                                                                                    | `undefined`   | Primary action button configuration                     |
| secondaryAction | `ActionConfig`                                                                                    | `undefined`   | Secondary action button configuration                   |
| className       | `string`                                                                                          | `undefined`   | Additional CSS classes for notification                 |
| style           | `CSSProperties`                                                                                   | `undefined`   | Inline styles for notification                          |
| iconStyle       | `CSSProperties`                                                                                   | `undefined`   | Inline styles for icon container                        |
| onClose         | `() => void`                                                                                      | `undefined`   | Callback when notification is dismissed                 |
| stackable       | `boolean`                                                                                         | `true`        | Whether multiple notifications can stack                |

### Action Configuration

```typescript
interface ActionConfig {
  label: string;
  onClick: () => void;
  className?: string;
  style?: React.CSSProperties;
}
```

### Import Statement

```typescript
import { notification-nudge } from "gends";
```

## Basic Usage

### Setup Provider

```tsx
import { NotificationProvider } from "gends";

function App() {
  return (
    <NotificationProvider>
      <YourApp />
    </NotificationProvider>
  );
}
```

### Basic Notification

```tsx
import { notify } from "gends";

// Simple info notification
notify({
  title: "Information",
  description: "This is a basic notification",
  variant: "info",
});

// Success notification
notify({
  title: "Success!",
  description: "Operation completed successfully",
  variant: "success",
});

// Error notification
notify({
  title: "Error",
  description: "Something went wrong",
  variant: "error",
});

// Loading notification
notify({
  title: "Processing",
  description: "Please wait...",
  variant: "loading",
});
```

## Advanced Features

### With Actions

```tsx
notify({
  title: "Update Available",
  description: "A new version is ready to install",
  variant: "info",
  showActions: true,
  primaryAction: {
    label: "Install Now",
    onClick: () => handleInstall(),
  },
  secondaryAction: {
    label: "Later",
    onClick: () => handleDismiss(),
  },
});
```

### With Progress Bar

```tsx
notify({
  title: "Uploading",
  description: "Your file is being uploaded",
  variant: "loading",
  showProgressBar: true,
  duration: 10000, // 10 seconds
});
```

### Custom Positioning

```tsx
notify({
  title: "Custom Position",
  description: "This notification appears at the bottom center",
  position: "bottom-center",
  duration: 3000,
});
```

### Non-Stackable Notifications

```tsx
notify({
  title: "Single Notification",
  description: "This will replace any existing notification",
  stackable: false,
});
```

### Custom Styling

```tsx
notify({
  title: "Custom Styled",
  description: "With custom colors and spacing",
  className: "custom-notification",
  style: {
    backgroundColor: "#2A2A2A",
    borderLeft: "4px solid #4B4BFF",
  },
  iconStyle: {
    color: "#4B4BFF",
  },
});
```

## Real-World Usage Examples

### Form Submission Feedback

```tsx
const handleSubmit = async formData => {
  try {
    notify({
      title: "Submitting",
      description: "Please wait while we process your request",
      variant: "loading",
      duration: null, // Manual close
    });

    await submitForm(formData);

    notify({
      title: "Success!",
      description: "Your form has been submitted successfully",
      variant: "success",
      duration: 5000,
    });
  } catch (error) {
    notify({
      title: "Error",
      description: "Failed to submit form. Please try again.",
      variant: "error",
      showActions: true,
      primaryAction: {
        label: "Retry",
        onClick: () => handleSubmit(formData),
      },
    });
  }
};
```

### File Upload Progress

```tsx
const handleFileUpload = async file => {
  const notificationId = notify({
    title: "Uploading File",
    description: `${file.name} is being uploaded`,
    variant: "loading",
    showProgressBar: true,
    duration: null,
  });

  try {
    await uploadFile(file, progress => {
      // Update progress
      notify({
        id: notificationId,
        title: "Uploading File",
        description: `${file.name} is being uploaded`,
        variant: "loading",
        showProgressBar: true,
        duration: null,
      });
    });

    notify({
      title: "Upload Complete",
      description: `${file.name} has been uploaded successfully`,
      variant: "success",
    });
  } catch (error) {
    notify({
      title: "Upload Failed",
      description: "Failed to upload file. Please try again.",
      variant: "error",
      showActions: true,
      primaryAction: {
        label: "Retry",
        onClick: () => handleFileUpload(file),
      },
    });
  }
};
```

### Promise-based Notifications

```tsx
import { notifyPromise } from "gends";

const handleAsyncOperation = async () => {
  await notifyPromise(performAsyncOperation(), {
    loading: "Processing your request...",
    success: data => `Operation completed: ${data.result}`,
    error: err => `Failed: ${err.message}`,
  });
};
```

## Accessibility Features

### Keyboard Navigation

- **Focus Management**: Notifications are focusable and can be dismissed with keyboard
- **ARIA Roles**: Proper alert roles for screen readers
- **Focus Trap**: Prevents focus from leaving notification when open

### Screen Reader Support

- **ARIA Attributes**: Proper roles and states
- **Announcements**: Clear identification of notification purpose
- **Status Updates**: Dynamic updates for progress and state changes

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Icon Indicators**: Clear visual distinction between variants
- **Progress Indication**: Visual feedback for timing and progress

## Design System Integration

### Genesis Design Tokens

**Colors:**

- Info: `bg-[#141414]`
- Success: `bg-[#135610]`
- Error: `bg-[#660014]`
- Loading: `bg-[#141414]`

**Typography:**

- Title: `text-en-desktop-body-m-prominent`
- Description: `text-en-desktop-body-s`

**Spacing:**

- Container: `p-gd-12`
- Content: `gap-gd-8`
- Actions: `gap-gd-12`

**Shadows:**

- Notification: `shadow-[0_0_8px_0_var(--gd-neutral-shadow-opacity)]`

## Best Practices

### Performance

- Use appropriate duration values
- Clean up notifications when component unmounts
- Handle multiple notifications efficiently

### User Experience

- Keep messages clear and concise
- Use appropriate variants for different states
- Consider mobile responsiveness
- Don't overwhelm with too many notifications

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle errors gracefully

## Troubleshooting

### Common Issues

**Notification Stacking:**

- Check stackable prop
- Verify z-index values
- Review positioning

**Auto-dismiss:**

- Verify duration value
- Check for hover pause
- Review timer cleanup

**Styling:**

- Check custom styles
- Verify design tokens
- Review responsive behavior

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Notification Nudge component provides a flexible and accessible way to display temporary messages to users. Choose the appropriate configuration based on your specific use case and requirements.
