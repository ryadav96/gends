# Bottom Sheet Component

## Overview

The Bottom Sheet component is a modal overlay that slides up from the bottom of the screen, commonly used in mobile interfaces to provide contextual details, actions, or additional controls. It supports flexible content configuration with customizable header, body, and footer sections, making it ideal for confirmation dialogs, forms, navigation menus, and content presentation in mobile-first applications.

## Component API

### Bottom Sheet Props

| Prop                  | Type                  | Default                                     | Description                                         |
| --------------------- | --------------------- | ------------------------------------------- | --------------------------------------------------- |
| `title`               | `string`              | `"Sheet title"`                             | Main heading text displayed in the header           |
| `bodyText`            | `string`              | `"This is a bottom sheet used commonly..."` | Default descriptive text content in the body        |
| `size`                | `"sm" \| "md"`        | `"md"`                                      | Size variant controlling overall dimensions         |
| `scroll`              | `boolean`             | `true`                                      | Whether body content is scrollable                  |
| `backIcon`            | `boolean`             | `true`                                      | Whether to show back navigation button in header    |
| `headerSlot`          | `boolean`             | `true`                                      | Whether to enable custom header content slot        |
| `headerTitle`         | `boolean`             | `true`                                      | Whether to display the title in the header          |
| `bodyTextVisible`     | `boolean`             | `true`                                      | Whether to show the default body text               |
| `showBodySlot`        | `boolean`             | `true`                                      | Whether to display the body content slot            |
| `swapHeaderSlot`      | `React.ReactNode`     | `<Slot className="h-gd-32" />`              | Custom content to replace default header slot       |
| `swapBodySlot`        | `React.ReactNode`     | `null`                                      | Custom content to replace default body content      |
| `primaryButtonText`   | `string`              | `"Button"`                                  | Text label for the primary action button            |
| `secondaryButtonText` | `string`              | `"Cancel"`                                  | Text label for the secondary action button          |
| `onClose`             | `() => void`          | `() => {}`                                  | Handler function called when bottom sheet is closed |
| `onPrimaryClick`      | `() => void`          | `() => {}`                                  | Handler function for primary button click           |
| `onSecondaryClick`    | `() => void`          | `() => {}`                                  | Handler function for secondary button click         |
| `onBackClick`         | `() => void`          | `() => {}`                                  | Handler function for back button click              |
| `classNames`          | `ClassNames`          | `{}`                                        | Custom CSS classes for different sections           |
| `id`                  | `string`              | `""`                                        | Unique identifier for the bottom sheet element      |
| `style`               | `React.CSSProperties` | `{}`                                        | Inline styles for the container                     |

### ClassNames Interface

```typescript
interface ClassNames {
  container?: string; // Custom classes for the main bottom sheet container
  header?: string; // Custom classes for the header section
  body?: string; // Custom classes for the body section
  footer?: string; // Custom classes for the footer section
  backdrop?: string; // Custom classes for the backdrop overlay
}
```

## Basic Usage

### Default Bottom Sheet

The standard bottom sheet with title, description, and action buttons.

```tsx
import { BottomSheet } from "gends";

<BottomSheet
  title="Bottom Sheet"
  bodyText="This is a standard bottom sheet with default configuration. It provides contextual details or controls in the lower area of the screen."
  primaryButtonText="Confirm"
  secondaryButtonText="Cancel"
  onClose={() => setIsOpen(false)}
/>;
```

### Interactive Implementation

Complete example showing how to integrate the bottom sheet with state management.

```tsx
import React, { useState } from "react";
import { BottomSheet, Button } from "gends";

const App = () => {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div>
      <Button onClick={() => setIsOpen(true)}>Open Bottom Sheet</Button>

      {isOpen && (
        <div className="fixed inset-0 z-50 bg-black/30 flex items-end justify-center">
          <BottomSheet
            title="Interactive Example"
            bodyText="This bottom sheet can be opened and closed with button controls."
            primaryButtonText="Done"
            secondaryButtonText="Cancel"
            onClose={() => setIsOpen(false)}
            onPrimaryClick={() => {
              handlePrimaryAction();
              setIsOpen(false);
            }}
            onSecondaryClick={() => setIsOpen(false)}
          />
        </div>
      )}
    </div>
  );
};
```

## Size Variants

### Small Size (sm)

Compact variant with reduced button heights for simple interactions.

```tsx
<BottomSheet
  size="sm"
  title="Compact Sheet"
  bodyText="This is a smaller variant of the bottom sheet used when less space is needed or for simpler interactions."
  primaryButtonText="Save"
  secondaryButtonText="Cancel"
/>
```

### Medium Size (md) - Default

Standard size with full button heights for rich content and complex interactions.

```tsx
<BottomSheet
  size="md"
  title="Standard Sheet"
  bodyText="This is the default medium-sized bottom sheet suitable for most use cases."
  primaryButtonText="Continue"
  secondaryButtonText="Cancel"
/>
```

### Size Comparison

```tsx
// Small size - Button height: 32px (h-gd-32)
<BottomSheet size="sm" title="Small" primaryButtonText="Action" />

// Medium size - Button height: 40px (h-gd-40)
<BottomSheet size="md" title="Medium" primaryButtonText="Action" />
```

## Header Configuration

### Default Header

Standard header with back button, title, and close button.

```tsx
<BottomSheet
  title="Header Example"
  backIcon={true}
  headerTitle={true}
  onBackClick={() => console.log("Back clicked")}
/>
```

### Header Without Back Button

Remove back navigation for primary contexts.

```tsx
<BottomSheet
  title="No Back Button"
  backIcon={false}
  bodyText="This bottom sheet doesn't show a back button. This is useful when the sheet is the primary context rather than a nested view."
/>
```

### Header Without Title

Hide the title for cleaner header appearance.

```tsx
<BottomSheet
  title="Hidden Title"
  headerTitle={false}
  bodyText="This bottom sheet doesn't display the title in the header. This can be useful when you want a cleaner header area."
/>
```

### Custom Header Content

Add custom components to the header slot area.

```tsx
import { Button } from "gends";

<BottomSheet
  title="Custom Header"
  headerSlot={true}
  swapHeaderSlot={
    <div className="flex items-center gap-2 px-2">
      <Button variant="secondary" size="s">
        Action 1
      </Button>
      <Button variant="secondary" size="s">
        Action 2
      </Button>
    </div>
  }
  bodyText="This bottom sheet includes custom content in the header slot area."
/>;
```

## Body Content Configuration

### Default Body Text

Standard text content with optional scrolling.

```tsx
<BottomSheet
  title="Standard Content"
  bodyText="This is the main content area of the bottom sheet where you can display information, forms, or other interactive elements."
  bodyTextVisible={true}
  scroll={true}
/>
```

### Scrollable Content

Handle long content with automatic scrolling.

```tsx
<BottomSheet
  title="Scrollable Content"
  scroll={true}
  bodyText={`This is an example of a bottom sheet with long scrollable content.
  
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
  
  Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  
  Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.`}
/>
```

### Custom Body Content

Replace default text with custom components.

```tsx
import { Button } from "gends";

<BottomSheet
  title="Custom Body Content"
  showBodySlot={true}
  swapBodySlot={
    <div className="flex flex-col gap-4 p-4">
      <Button variant="primary" size="l" block>
        Primary Action
      </Button>
      <Button variant="secondary" size="l" block>
        Secondary Action
      </Button>
      <Button variant="tertiary" size="l" block>
        Tertiary Action
      </Button>
    </div>
  }
/>;
```

### Hide Body Content

Display only header and footer sections.

```tsx
<BottomSheet
  title="Header and Footer Only"
  bodyTextVisible={false}
  showBodySlot={false}
  primaryButtonText="Continue"
  secondaryButtonText="Cancel"
/>
```

## Footer Actions

### Custom Button Labels

Customize action button text for specific contexts.

```tsx
<BottomSheet
  title="Confirmation"
  bodyText="Are you sure you want to delete this item? This action cannot be undone."
  primaryButtonText="Yes, Delete"
  secondaryButtonText="Cancel"
  onPrimaryClick={() => handleDelete()}
  onSecondaryClick={() => handleCancel()}
/>
```

### Different Action Types

Examples of various action combinations.

```tsx
// Save/Cancel actions
<BottomSheet
  title="Edit Profile"
  primaryButtonText="Save Changes"
  secondaryButtonText="Cancel"
  onPrimaryClick={handleSave}
  onSecondaryClick={handleCancel}
/>

// Continue/Skip actions
<BottomSheet
  title="Tutorial Step"
  primaryButtonText="Continue"
  secondaryButtonText="Skip"
  onPrimaryClick={handleContinue}
  onSecondaryClick={handleSkip}
/>

// Confirm/Deny actions
<BottomSheet
  title="Permission Request"
  primaryButtonText="Allow"
  secondaryButtonText="Deny"
  onPrimaryClick={handleAllow}
  onSecondaryClick={handleDeny}
/>
```

## Advanced Use Cases

### Form Integration

Bottom sheet containing form elements for data collection.

```tsx
import { Input, Select, Button } from "gends";

const FormBottomSheet = ({ isOpen, onClose }) => {
  const [formData, setFormData] = useState({});

  const handleSubmit = () => {
    // Process form data
    console.log(formData);
    onClose();
  };

  return (
    <BottomSheet
      title="Add New Contact"
      bodyTextVisible={false}
      swapBodySlot={
        <form className="space-y-4 p-4">
          <Input
            label="Full Name"
            placeholder="Enter full name"
            value={formData.name}
            onChange={e => setFormData({ ...formData, name: e.target.value })}
          />
          <Input
            label="Email"
            type="email"
            placeholder="Enter email address"
            value={formData.email}
            onChange={e => setFormData({ ...formData, email: e.target.value })}
          />
          <Select
            label="Category"
            options={[
              { value: "work", label: "Work" },
              { value: "personal", label: "Personal" },
              { value: "family", label: "Family" },
            ]}
            value={formData.category}
            onChange={value => setFormData({ ...formData, category: value })}
          />
        </form>
      }
      primaryButtonText="Add Contact"
      secondaryButtonText="Cancel"
      onPrimaryClick={handleSubmit}
      onSecondaryClick={onClose}
    />
  );
};
```

### Navigation Menu

Bottom sheet as a navigation interface.

```tsx
import { List, ListItem, Icon } from "gends";

<BottomSheet
  title="Menu"
  bodyTextVisible={false}
  swapBodySlot={
    <div className="py-2">
      <ListItem onClick={handleProfile}>
        <Icon name="user" />
        <span>Profile</span>
      </ListItem>
      <ListItem onClick={handleSettings}>
        <Icon name="settings" />
        <span>Settings</span>
      </ListItem>
      <ListItem onClick={handleHelp}>
        <Icon name="help" />
        <span>Help & Support</span>
      </ListItem>
      <ListItem onClick={handleLogout}>
        <Icon name="logout" />
        <span>Logout</span>
      </ListItem>
    </div>
  }
  primaryButtonText="Close"
  hideSecondaryBtn={true}
/>;
```

### Media Selection

Bottom sheet for selecting images or files.

```tsx
const MediaSelector = ({ onSelect, onClose }) => {
  const mediaOptions = [
    { id: 1, type: "camera", label: "Take Photo", icon: "camera" },
    { id: 2, type: "gallery", label: "Choose from Gallery", icon: "image" },
    { id: 3, type: "files", label: "Browse Files", icon: "folder" },
  ];

  return (
    <BottomSheet
      title="Select Media"
      bodyTextVisible={false}
      swapBodySlot={
        <div className="space-y-2 p-4">
          {mediaOptions.map(option => (
            <button
              key={option.id}
              className="w-full flex items-center gap-3 p-3 rounded-lg hover:bg-gray-50"
              onClick={() => {
                onSelect(option.type);
                onClose();
              }}
            >
              <Icon name={option.icon} />
              <span>{option.label}</span>
            </button>
          ))}
        </div>
      }
      primaryButtonText="Cancel"
      hideSecondaryBtn={true}
      onPrimaryClick={onClose}
    />
  );
};
```

### Confirmation Dialog

Critical action confirmation with detailed information.

```tsx
<BottomSheet
  title="Delete Account"
  bodyText="This action will permanently delete your account and all associated data. This cannot be undone."
  primaryButtonText="Delete Forever"
  secondaryButtonText="Keep Account"
  size="sm"
  classNames={{
    header: "bg-red-50",
    footer: "bg-red-50",
  }}
  onPrimaryClick={handleDeleteAccount}
  onSecondaryClick={onClose}
/>
```

### Multi-Step Wizard

Guide users through multi-step processes.

```tsx
const WizardBottomSheet = () => {
  const [currentStep, setCurrentStep] = useState(1);
  const totalSteps = 3;

  const stepContent = {
    1: {
      title: "Step 1: Basic Information",
      content: <BasicInfoForm />,
    },
    2: {
      title: "Step 2: Preferences",
      content: <PreferencesForm />,
    },
    3: {
      title: "Step 3: Confirmation",
      content: <ConfirmationView />,
    },
  };

  return (
    <BottomSheet
      title={stepContent[currentStep].title}
      backIcon={currentStep > 1}
      onBackClick={() => setCurrentStep(currentStep - 1)}
      bodyTextVisible={false}
      swapBodySlot={stepContent[currentStep].content}
      primaryButtonText={currentStep === totalSteps ? "Complete" : "Next"}
      secondaryButtonText="Cancel"
      onPrimaryClick={() => {
        if (currentStep === totalSteps) {
          handleComplete();
        } else {
          setCurrentStep(currentStep + 1);
        }
      }}
    />
  );
};
```

## Styling and Customization

### Custom Section Styling

Apply custom styles to different sections of the bottom sheet.

```tsx
<BottomSheet
  title="Styled Sheet"
  bodyText="This bottom sheet has custom styling applied to each of its sections."
  classNames={{
    container: "shadow-xl",
    header: "bg-blue-50 border-b border-blue-200",
    body: "bg-gray-50",
    footer: "bg-blue-50 border-t border-blue-200",
  }}
/>
```

### Inline Styling

Apply custom styles using the style prop.

```tsx
<BottomSheet
  title="Custom Width"
  bodyText="This bottom sheet has custom width and positioning."
  style={{
    maxWidth: "500px",
    margin: "0 auto",
  }}
/>
```

### Backdrop Customization

Customize the overlay backdrop appearance.

```tsx
<BottomSheet
  title="Custom Backdrop"
  bodyText="This bottom sheet has a custom backdrop style."
  classNames={{
    backdrop: "bg-purple-900/40 backdrop-blur-sm",
  }}
/>
```

## Layout Specifications

### Dimensions and Spacing

- **Container**: `max-w-md` (maximum width), `rounded-t-xl` (top border radius)
- **Header**: `px-gd-12 py-gd-16` (padding), `h-gd-64` (fixed height)
- **Body**: `px-gd-24 py-gd-0` (padding), `max-h-[60vh]` (scrollable max height)
- **Footer**: `px-gd-24 py-gd-16` (padding), `gap-gd-12` (button spacing)
- **Button Heights**: `h-gd-32` (sm), `h-gd-40` (md)

### Typography Hierarchy

- **Title**: `text-en-desktop-heading-xl` (heading extra large)
- **Body Text**: `text-color-neutral-grey-80` (subdued body text)
- **Buttons**: Inherited from Button component styling

### Color Specifications

- **Background**: `bg-color-neutral-white` (white background)
- **Backdrop**: `bg-color-neutral-grey-100` with opacity
- **Text**: `text-color-neutral-grey-80` for body content
- **Borders**: System default border colors

## Accessibility Features

- **Modal Dialog**: Proper `role="dialog"` and `aria-modal="true"` attributes
- **Focus Management**: Automatic focus handling and trap within the modal
- **Keyboard Navigation**: ESC key support for closing, tab navigation
- **Screen Reader Support**: Proper heading hierarchy and ARIA labels
- **Backdrop Interaction**: Click outside to close functionality
- **Semantic Structure**: Logical content flow and heading hierarchy

```tsx
<BottomSheet
  title="Accessible Example"
  bodyText="This bottom sheet follows accessibility best practices."
  // Automatic ARIA attributes:
  // role="dialog"
  // aria-modal="true"
  // aria-labelledby="bottom-sheet-title"
/>
```

## Best Practices

### Design Guidelines

- Use bottom sheets primarily for mobile interfaces and touch interactions
- Keep content concise and focused on the primary task
- Provide clear action buttons with descriptive labels
- Use appropriate size variants based on content complexity
- Include proper navigation controls for multi-step flows
- Consider the context and urgency of the action when designing

### Content Guidelines

- Write clear, actionable titles that describe the sheet's purpose
- Keep body text concise but provide sufficient context
- Use familiar button labels that clearly indicate the action
- Consider the user's mental model and task flow
- Provide help text or examples when needed
- Test content with actual users in realistic scenarios

### Interaction Guidelines

- Always provide a way to close or dismiss the bottom sheet
- Use consistent button placement and behavior
- Implement proper feedback for user actions
- Consider touch target sizes for mobile devices
- Handle edge cases like network errors or validation failures
- Test gesture interactions like swipe-to-dismiss

### Technical Guidelines

- Manage focus properly when opening and closing
- Handle viewport changes and device rotation
- Implement proper z-index layering for overlays
- Consider performance impact of complex content
- Test across different devices and screen sizes
- Implement proper cleanup for event listeners and timers

## Integration Examples

### E-commerce Product Details

```tsx
const ProductDetailsSheet = ({ product, onClose }) => {
  return (
    <BottomSheet
      title={product.name}
      bodyTextVisible={false}
      swapBodySlot={
        <div className="space-y-4 p-4">
          <img
            src={product.image}
            alt={product.name}
            className="w-full h-48 object-cover rounded"
          />
          <div className="space-y-2">
            <p className="text-2xl font-bold">${product.price}</p>
            <p className="text-gray-600">{product.description}</p>
            <div className="flex items-center gap-2">
              <span className="text-sm">Rating:</span>
              <StarRating value={product.rating} />
              <span className="text-sm text-gray-500">({product.reviewCount} reviews)</span>
            </div>
          </div>
        </div>
      }
      primaryButtonText="Add to Cart"
      secondaryButtonText="Close"
      onPrimaryClick={() => handleAddToCart(product)}
      onSecondaryClick={onClose}
    />
  );
};
```

### Social Media Actions

```tsx
const PostActionsSheet = ({ post, onClose }) => {
  const actions = [
    { id: "share", label: "Share Post", icon: "share" },
    { id: "save", label: "Save Post", icon: "bookmark" },
    { id: "report", label: "Report Post", icon: "flag" },
    { id: "hide", label: "Hide Post", icon: "eye-off" },
  ];

  return (
    <BottomSheet
      title="Post Options"
      bodyTextVisible={false}
      swapBodySlot={
        <div className="py-2">
          {actions.map(action => (
            <button
              key={action.id}
              className="w-full flex items-center gap-3 p-4 hover:bg-gray-50"
              onClick={() => {
                handleAction(action.id, post);
                onClose();
              }}
            >
              <Icon name={action.icon} />
              <span>{action.label}</span>
            </button>
          ))}
        </div>
      }
      primaryButtonText="Cancel"
      hideSecondaryBtn={true}
      onPrimaryClick={onClose}
    />
  );
};
```

### Settings Configuration

```tsx
const SettingsSheet = ({ settings, onSave, onClose }) => {
  const [localSettings, setLocalSettings] = useState(settings);

  return (
    <BottomSheet
      title="Notification Settings"
      bodyTextVisible={false}
      swapBodySlot={
        <div className="space-y-4 p-4">
          <Toggle
            label="Push Notifications"
            checked={localSettings.pushNotifications}
            onChange={checked => setLocalSettings({ ...localSettings, pushNotifications: checked })}
          />
          <Toggle
            label="Email Notifications"
            checked={localSettings.emailNotifications}
            onChange={checked =>
              setLocalSettings({ ...localSettings, emailNotifications: checked })
            }
          />
          <Select
            label="Notification Frequency"
            value={localSettings.frequency}
            options={[
              { value: "immediate", label: "Immediate" },
              { value: "daily", label: "Daily Digest" },
              { value: "weekly", label: "Weekly Summary" },
            ]}
            onChange={frequency => setLocalSettings({ ...localSettings, frequency })}
          />
        </div>
      }
      primaryButtonText="Save Settings"
      secondaryButtonText="Cancel"
      onPrimaryClick={() => {
        onSave(localSettings);
        onClose();
      }}
      onSecondaryClick={onClose}
    />
  );
};
```

## Performance Considerations

- **Conditional Rendering**: Only render when needed to optimize performance
- **Content Optimization**: Lazy load heavy content or images within the sheet
- **Animation Performance**: Use CSS transitions for smooth animations
- **Memory Management**: Properly cleanup event listeners and subscriptions
- **Virtualization**: Consider virtual scrolling for very long content lists
- **Bundle Size**: Import only the components and features you need

## Troubleshooting

### Common Issues

- **Z-index conflicts**: Ensure proper stacking context and z-index values
- **Touch interactions**: Verify touch events work properly on mobile devices
- **Content overflow**: Check that long content scrolls correctly
- **Focus management**: Ensure focus is handled properly when opening/closing
- **Backdrop clicks**: Verify backdrop click detection works correctly
- **Animation glitches**: Test animations across different devices and browsers

### Debugging Tips

- Use browser dev tools to inspect modal structure and z-index layering
- Test touch interactions on actual mobile devices, not just desktop simulators
- Check console for JavaScript errors related to event handlers
- Validate ARIA attributes and accessibility with screen reader testing
- Test with different content lengths to ensure proper responsive behavior
- Monitor performance with large amounts of content or complex components

## Migration Guide

When upgrading from older versions:

1. Update import statements to use `gends` package
2. Replace deprecated prop names with new API structure
3. Update custom styling to use new classNames interface
4. Test header and body slot customizations with new prop structure
5. Verify event handler functions match new callback signatures
6. Update accessibility attributes to use new automatic implementation

## Technical Notes

- Component uses Genesis spacing tokens (gd-\*) for consistent spacing
- Typography follows Genesis design system specifications
- Color values use Genesis color variables for theme compatibility
- Component supports forwardRef for advanced ref management
- Modal behavior includes proper focus trapping and backdrop handling
- Responsive design adapts to different screen sizes automatically
- Component handles touch gestures and mobile-specific interactions
- Z-index management ensures proper layering with other UI elements
