# Notification Banner Component

## Overview

The Notification Banner component displays important messages, alerts, and feedback to users in a prominent, non-intrusive way. It supports multiple layout modes (single-line and multi-line), semantic color variants, and flexible content with customizable actions. The component is designed to capture user attention while providing clear actionable options for different notification contexts.

## Component API

### Banner Props

| Prop                 | Type                                                          | Default         | Description                                            |
| -------------------- | ------------------------------------------------------------- | --------------- | ------------------------------------------------------ |
| `title`              | `string`                                                      | `"Title"`       | Main heading text for the banner                       |
| `description`        | `string`                                                      | `"Description"` | Descriptive content text                               |
| `icon`               | `React.ReactNode`                                             | `undefined`     | Custom icon element (defaults to warning icon)         |
| `variant`            | `"neutral" \| "primary" \| "error" \| "success" \| "warning"` | `"primary"`     | Semantic color theme and meaning                       |
| `hideTitle`          | `boolean`                                                     | `false`         | Whether to hide the title section                      |
| `isFullWidth`        | `boolean`                                                     | `false`         | Whether to use full-width layout (screen edge to edge) |
| `isSingleLine`       | `boolean`                                                     | `false`         | Whether to use single-line compact layout              |
| `hideButtons`        | `boolean`                                                     | `false`         | Whether to hide all action buttons                     |
| `hidePrimaryBtn`     | `boolean`                                                     | `false`         | Whether to hide the primary action button              |
| `hideSecondaryBtn`   | `boolean`                                                     | `false`         | Whether to hide the secondary action button            |
| `primaryBtnText`     | `string`                                                      | `"Submit"`      | Text label for the primary action button               |
| `secondaryBtnText`   | `string`                                                      | `"Cancel"`      | Text label for the secondary action button             |
| `primaryBtnAction`   | `() => void`                                                  | `() => {}`      | Click handler for primary action button                |
| `secondaryBtnAction` | `() => void`                                                  | `() => {}`      | Click handler for secondary action button              |
| `hideClose`          | `boolean`                                                     | `false`         | Whether to hide the close/dismiss button               |
| `hideIcon`           | `boolean`                                                     | `false`         | Whether to hide the icon element                       |
| `loading`            | `boolean`                                                     | `false`         | Whether to show loading spinner instead of icon        |
| `showBanner`         | `boolean`                                                     | `true`          | Whether to display the banner                          |
| `onClose`            | `() => void`                                                  | `undefined`     | Custom close handler (overrides default visibility)    |

## Basic Usage

### Default Banner

The standard multi-line banner with title, description, and action buttons.

```tsx
import { Banner } from "gends";

<Banner
  title="Notification Title"
  description="This is a detailed description of the notification content that provides context and information to the user."
  variant="primary"
/>;
```

### Simple Text-Only Banner

Minimal banner without buttons for informational content.

```tsx
<Banner
  title="Information"
  description="This is an informational message."
  hideButtons={true}
  variant="neutral"
/>
```

## Layout Variants

### Multi-Line Layout (Default)

The standard layout with vertical content arrangement for detailed notifications.

```tsx
<Banner
  title="System Update Available"
  description="A new system update is available with important security fixes and performance improvements. We recommend updating at your earliest convenience."
  variant="primary"
  primaryBtnText="Update Now"
  secondaryBtnText="Later"
/>
```

### Single-Line Layout

Compact horizontal layout for brief notifications and status messages.

```tsx
<Banner
  isSingleLine={true}
  description="Your changes have been saved successfully."
  variant="success"
  primaryBtnText="Continue"
  hideSecondaryBtn={true}
/>
```

### Full-Width Layout

Edge-to-edge banner that spans the entire screen width for critical notifications.

```tsx
<Banner
  isFullWidth={true}
  isSingleLine={true}
  description="Scheduled maintenance will begin in 30 minutes. Please save your work."
  variant="warning"
  primaryBtnText="Acknowledge"
  hideSecondaryBtn={true}
/>
```

## Semantic Variants

### Primary Variant

General purpose notifications and brand-related content.

```tsx
<Banner
  variant="primary"
  title="New Feature Available"
  description="Discover our latest feature that helps you work more efficiently and manage your tasks better."
  primaryBtnText="Learn More"
  secondaryBtnText="Dismiss"
/>
```

### Success Variant

Positive feedback, completion confirmations, and successful actions.

```tsx
<Banner
  variant="success"
  title="Operation Completed"
  description="Your request has been processed successfully and all changes have been saved."
  primaryBtnText="View Details"
  secondaryBtnText="OK"
/>
```

### Error Variant

Error messages, failure notifications, and critical alerts requiring immediate attention.

```tsx
<Banner
  variant="error"
  title="Connection Failed"
  description="Unable to connect to the server. Please check your internet connection and try again."
  primaryBtnText="Retry"
  secondaryBtnText="Cancel"
/>
```

### Warning Variant

Cautionary messages, potential issues, and actions requiring user consideration.

```tsx
<Banner
  variant="warning"
  title="Unsaved Changes"
  description="You have unsaved changes that will be lost if you navigate away from this page."
  primaryBtnText="Save Changes"
  secondaryBtnText="Discard"
/>
```

### Neutral Variant

General information, system status, and non-urgent notifications.

```tsx
<Banner
  variant="neutral"
  title="System Information"
  description="Regular maintenance is scheduled for this weekend. Some features may be temporarily unavailable."
  primaryBtnText="Learn More"
  secondaryBtnText="OK"
/>
```

## Content Customization

### Custom Icon Integration

Replace the default warning icon with custom icons for specific contexts.

```tsx
import { IcCheck, IcError, IcInfo } from "gends";

// Success notification with check icon
<Banner
  variant="success"
  icon={<IcCheck />}
  title="Upload Complete"
  description="All files have been uploaded successfully."
  primaryBtnText="View Files"
/>;

// Error notification with error icon
<Banner
  variant="error"
  icon={<IcError />}
  title="Upload Failed"
  description="Some files could not be uploaded due to size restrictions."
  primaryBtnText="Try Again"
/>;

// Information with info icon
<Banner
  variant="neutral"
  icon={<IcInfo />}
  title="Tips"
  description="Use keyboard shortcuts to work more efficiently."
  hideButtons={true}
/>;
```

### Loading State

Show loading spinner during asynchronous operations.

```tsx
<Banner
  variant="primary"
  loading={true}
  title="Processing Request"
  description="Please wait while we process your request. This may take a few moments."
  hideButtons={true}
/>
```

### Without Icons

Hide icons for text-focused notifications.

```tsx
<Banner
  hideIcon={true}
  variant="neutral"
  title="Newsletter Subscription"
  description="Subscribe to our newsletter for the latest updates and announcements."
  primaryBtnText="Subscribe"
  secondaryBtnText="No Thanks"
/>
```

## Button Configuration

### Single Action Button

Show only the primary action button for simple yes/no scenarios.

```tsx
<Banner
  variant="success"
  title="Email Verified"
  description="Your email address has been successfully verified."
  primaryBtnText="Continue"
  hideSecondaryBtn={true}
/>
```

### Secondary Action Only

Show only the secondary action for cancel/dismiss scenarios.

```tsx
<Banner
  variant="neutral"
  title="Optional Update"
  description="An optional feature update is available for download."
  hidePrimaryBtn={true}
  secondaryBtnText="Maybe Later"
/>
```

### No Action Buttons

Pure informational banners without user actions.

```tsx
<Banner
  variant="neutral"
  title="System Status"
  description="All systems are operating normally."
  hideButtons={true}
/>
```

### Custom Button Text

Customize button labels for specific contexts and actions.

```tsx
<Banner
  variant="warning"
  title="Storage Almost Full"
  description="Your storage is 90% full. Free up space or upgrade your plan."
  primaryBtnText="Upgrade Plan"
  secondaryBtnText="Free Up Space"
/>
```

## Dismissal Behavior

### Default Close Behavior

Built-in close functionality that hides the banner.

```tsx
<Banner
  variant="primary"
  title="Default Behavior"
  description="Click the close button to dismiss this banner."
/>
```

### Custom Close Handler

Implement custom logic when the banner is dismissed.

```tsx
const handleBannerClose = () => {
  // Custom cleanup logic
  analytics.track("banner_dismissed");
  localStorage.setItem("banner_dismissed", "true");
};

<Banner
  variant="primary"
  title="Custom Close Handler"
  description="This banner has custom close behavior."
  onClose={handleBannerClose}
/>;
```

### Non-Dismissible Banner

Remove close button for persistent notifications.

```tsx
<Banner
  variant="error"
  title="Critical System Alert"
  description="This is a critical system alert that requires immediate attention."
  hideClose={true}
  primaryBtnText="Acknowledge"
  hideSecondaryBtn={true}
/>
```

## Advanced Use Cases

### Progressive Disclosure

Use single-line layout for initial display, expand to multi-line for details.

```tsx
// Initial compact view
<Banner
  isSingleLine={true}
  description="New update available"
  variant="primary"
  primaryBtnText="Details"
  hideSecondaryBtn={true}
/>;

// Expanded detailed view
<Banner
  title="System Update Available"
  description="Version 2.1.0 includes security improvements, bug fixes, and new features. The update will require a system restart."
  variant="primary"
  primaryBtnText="Install Now"
  secondaryBtnText="Schedule Later"
/>;
```

### Multi-Step Workflows

Guide users through multi-step processes with contextual banners.

```tsx
// Step 1: Initial action
<Banner
  variant="primary"
  title="Welcome to Setup"
  description="Let's get your account configured with the essential settings."
  primaryBtnText="Start Setup"
  secondaryBtnText="Skip"
/>;

// Step 2: Progress indication
<Banner
  variant="primary"
  loading={true}
  title="Setting Up Your Account"
  description="Please wait while we configure your preferences..."
  hideButtons={true}
/>;

// Step 3: Completion
<Banner
  variant="success"
  title="Setup Complete"
  description="Your account has been successfully configured and is ready to use."
  primaryBtnText="Get Started"
  hideSecondaryBtn={true}
/>;
```

### Contextual Help

Provide contextual guidance and tips within workflows.

```tsx
<Banner
  variant="neutral"
  title="Pro Tip"
  description="Use Ctrl+S (Cmd+S on Mac) to quickly save your work at any time."
  hideButtons={true}
  hideClose={true}
  isSingleLine={true}
/>
```

### Status Announcements

Communicate system status and maintenance information.

```tsx
// Maintenance warning
<Banner
  variant="warning"
  isFullWidth={true}
  isSingleLine={true}
  description="Scheduled maintenance begins in 2 hours. Save your work frequently."
  primaryBtnText="Learn More"
  hideSecondaryBtn={true}
/>;

// Service restoration
<Banner
  variant="success"
  isFullWidth={true}
  isSingleLine={true}
  description="All services have been restored. Thank you for your patience."
  hideButtons={true}
/>;
```

## Color Theme Reference

### Primary Theme

- **Background**: Primary-10 (light primary blue)
- **Border**: Primary-30 (medium primary blue)
- **Icon**: Primary-50 (standard primary blue)
- **Button**: Default appearance
- **Use**: General notifications, feature announcements, onboarding

### Success Theme

- **Background**: Success-20 (light green)
- **Border**: Success-default (standard green)
- **Icon**: Success-50 (medium green)
- **Button**: Positive appearance
- **Use**: Completion confirmations, successful operations, positive feedback

### Error Theme

- **Background**: Error-20 (light red)
- **Border**: Error-50 (medium red)
- **Icon**: Error-50 (medium red)
- **Button**: Negative appearance
- **Use**: Error messages, failed operations, critical alerts

### Warning Theme

- **Background**: Warning-20 (light orange/yellow)
- **Border**: Warning-50 (medium orange)
- **Icon**: Warning-50 (medium orange)
- **Button**: Warning appearance
- **Use**: Caution alerts, potential issues, unsaved changes

### Neutral Theme

- **Background**: Grey-10 (light grey)
- **Border**: Grey-40 (medium grey)
- **Icon**: Primary-50 (primary blue)
- **Button**: Default appearance
- **Use**: General information, system status, tips

## Layout Specifications

### Multi-Line Layout

- **Padding**: 12px (gd-12)
- **Gap**: 8px between icon and content, 12px between buttons
- **Border Radius**: 12px (gd-12)
- **Border Width**: 1px
- **Icon Size**: 24px × 24px
- **Title Typography**: body-l-prominent
- **Description Typography**: body-m with subdued color

### Single-Line Layout

- **Padding**: 8px (gd-8) for contained, 12px vertical for full-width
- **Gap**: 8px between elements, 12px between buttons
- **Border Radius**: 12px (gd-12) for contained, none for full-width
- **Border Width**: 1px for contained, none for full-width
- **Icon Size**: 24px × 24px
- **Description Typography**: body-m with subdued color

### Full-Width Layout

- **Width**: 100vw (full screen width)
- **Padding**: 24px horizontal, 12px vertical
- **Border**: None
- **Border Radius**: None
- **Position**: Fixed to screen edges

## Accessibility Features

- **Semantic Markup**: Proper heading hierarchy and content structure
- **Color Independence**: Information conveyed through text, not just color
- **Keyboard Navigation**: Full keyboard support for all interactive elements
- **Screen Reader Support**: Proper ARIA labels and announcements
- **Focus Management**: Clear focus indicators and logical tab order
- **High Contrast**: Sufficient contrast ratios for all text and UI elements

## Best Practices

### Design Guidelines

- Use appropriate semantic variants that match the content meaning
- Keep descriptions concise but informative
- Use single-line layout for brief status messages
- Reserve full-width layout for critical system-wide notifications
- Provide clear, actionable button labels
- Include dismiss functionality unless the notification requires mandatory action

### Content Guidelines

- Write clear, actionable titles that summarize the notification
- Provide sufficient context in descriptions
- Use consistent language and terminology
- Consider internationalization for text content
- Avoid jargon and technical terms for user-facing notifications
- Include specific instructions for actions users should take

### Interaction Guidelines

- Make primary actions obvious and easy to find
- Provide alternative actions when appropriate
- Don't overwhelm users with too many buttons
- Use loading states for operations that take time
- Implement proper feedback for user actions
- Consider the notification's urgency and persistence needs

### Technical Guidelines

- Handle banner visibility state properly
- Implement proper cleanup in onClose handlers
- Test across different screen sizes and devices
- Ensure proper z-index layering with other UI elements
- Consider performance impact of persistent banners
- Implement proper error handling for async operations

## Integration Examples

### Form Validation Feedback

```tsx
const FormWithValidation = () => {
  const [showError, setShowError] = useState(false);

  const handleSubmit = data => {
    try {
      validateForm(data);
      setShowError(false);
    } catch (error) {
      setShowError(true);
    }
  };

  return (
    <div>
      {showError && (
        <Banner
          variant="error"
          title="Validation Failed"
          description="Please correct the highlighted fields and try again."
          primaryBtnText="Review Form"
          hideSecondaryBtn={true}
          onClose={() => setShowError(false)}
        />
      )}
      <form onSubmit={handleSubmit}>{/* Form fields */}</form>
    </div>
  );
};
```

### Application Notifications

```tsx
const NotificationSystem = () => {
  const [notifications, setNotifications] = useState([]);

  const addNotification = notification => {
    setNotifications(prev => [...prev, { ...notification, id: Date.now() }]);
  };

  const removeNotification = id => {
    setNotifications(prev => prev.filter(n => n.id !== id));
  };

  return (
    <div className="fixed top-4 right-4 space-y-2 z-50">
      {notifications.map(notification => (
        <Banner
          key={notification.id}
          variant={notification.variant}
          title={notification.title}
          description={notification.description}
          onClose={() => removeNotification(notification.id)}
          hideButtons={true}
        />
      ))}
    </div>
  );
};
```

### Onboarding Flow

```tsx
const OnboardingBanner = ({ currentStep, totalSteps }) => {
  const stepConfig = {
    1: {
      title: "Welcome to the Platform",
      description: "Let's get you started with a quick tour of the key features.",
      primaryBtnText: "Start Tour",
    },
    2: {
      title: "Create Your First Project",
      description: "Set up your workspace by creating your first project.",
      primaryBtnText: "Create Project",
    },
    3: {
      title: "Invite Team Members",
      description: "Collaborate better by inviting your team to join the project.",
      primaryBtnText: "Send Invites",
    },
  };

  const config = stepConfig[currentStep];

  return (
    <Banner
      variant="primary"
      title={config.title}
      description={config.description}
      primaryBtnText={config.primaryBtnText}
      secondaryBtnText={currentStep < totalSteps ? "Skip" : "Maybe Later"}
    />
  );
};
```

## Performance Considerations

- **Conditional Rendering**: Use showBanner prop to control visibility efficiently
- **Event Handler Optimization**: Memoize callback functions to prevent unnecessary re-renders
- **Icon Performance**: Reuse icon components instead of creating new instances
- **Animation Performance**: Consider CSS transitions for smooth show/hide animations
- **Memory Management**: Properly clean up timers and subscriptions in onClose handlers

## Troubleshooting

### Common Issues

- **Banner not displaying**: Check showBanner prop and parent container visibility
- **Button actions not working**: Verify callback functions are properly defined
- **Layout issues**: Ensure proper container sizing and overflow handling
- **Icon not showing**: Confirm icon prop is a valid React element
- **Styling conflicts**: Check for CSS specificity issues with custom styling
- **Responsive behavior**: Test layout across different screen sizes
- **Z-index conflicts**: Ensure proper stacking context for overlay positioning

### Debugging Tips

- Use browser dev tools to inspect banner structure and styling
- Check console for any JavaScript errors in callback functions
- Verify proper prop types and values
- Test interactive states (hover, focus, click)
- Validate accessibility with screen reader testing
- Check performance impact with React DevTools Profiler

## Migration Guide

When upgrading from older versions:

1. Update import statements to use `gends` package
2. Replace deprecated color prop names with new variant values
3. Update button configuration props to match new API
4. Test layout behavior with new single-line and full-width options
5. Verify custom icon integration with new icon prop structure
6. Update close handling to use new onClose callback pattern

## Technical Notes

- Component uses Genesis spacing tokens (gd-\*) for consistent spacing
- Typography follows Genesis design system specifications
- Color values use Genesis color variables for theme compatibility
- Component supports forwardRef for advanced ref management
- Layout automatically adapts based on isSingleLine and isFullWidth props
- Button appearances automatically match the banner variant theme
- Icon sizing and colors are managed automatically based on variant
- Component handles internal visibility state with external override capability
