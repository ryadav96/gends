# Popover Component

## Overview

The Popover component is a flexible and accessible floating panel built with Genesis Design System tokens. It provides a comprehensive set of features for displaying contextual information, actions, or forms in a floating panel that appears relative to a trigger element. The component supports various configurations including different sizes, scrollable content, custom headers and footers, and interactive states.

## Component API

### Popover Props

| Prop                        | Type                             | Default     | Description                                 |
| --------------------------- | -------------------------------- | ----------- | ------------------------------------------- |
| title                       | `string`                         | `"Title"`   | Title text displayed in the header          |
| children                    | `ReactNode`                      | `undefined` | Main content of the popover                 |
| open                        | `boolean`                        | `false`     | Whether the popover is visible              |
| onOpenChange                | `(open: boolean) => void`        | `undefined` | Callback when open state changes            |
| className                   | `string`                         | `undefined` | Additional CSS classes for the container    |
| contentClassName            | `string`                         | `undefined` | Additional CSS classes for the content area |
| buttonColor                 | `string`                         | `undefined` | Custom color for primary button             |
| secondaryButtonColor        | `string`                         | `undefined` | Custom color for secondary button           |
| footerColor                 | `string`                         | `undefined` | Custom color for footer background          |
| scrollable                  | `boolean`                        | `false`     | Whether the content area is scrollable      |
| hasHeader                   | `boolean`                        | `true`      | Whether to show the header section          |
| hasFooter                   | `boolean`                        | `true`      | Whether to show the footer section          |
| size                        | `"small" \| "large"`             | `"small"`   | Size variant of the popover                 |
| showCloseIcon               | `boolean`                        | `true`      | Whether to show the close icon in header    |
| hasHeaderSlot               | `boolean`                        | `true`      | Whether to show the header slot             |
| hasSecondaryButton          | `boolean`                        | `true`      | Whether to show the secondary button        |
| headerSlotContent           | `ReactNode`                      | `undefined` | Custom content for the header slot          |
| bodySlotContent             | `ReactNode`                      | `undefined` | Custom content for the body slot            |
| primaryButtonIcon           | `ReactNode`                      | `undefined` | Icon for the primary button                 |
| primaryButtonLabel          | `ReactNode`                      | `"Confirm"` | Label for the primary button                |
| primaryButtonDisabled       | `boolean`                        | `false`     | Whether the primary button is disabled      |
| secondaryButtonIcon         | `ReactNode`                      | `undefined` | Icon for the secondary button               |
| secondaryButtonLabel        | `string`                         | `"Cancel"`  | Label for the secondary button              |
| trigger                     | `ReactNode`                      | Required    | Element that triggers the popover           |
| onPrimaryButtonClick        | `() => void`                     | `undefined` | Callback when primary button is clicked     |
| onSecondaryButtonClick      | `() => void`                     | `undefined` | Callback when secondary button is clicked   |
| onCloseButtonClick          | `() => void`                     | `undefined` | Callback when close button is clicked       |
| stopContentPropagation      | `boolean`                        | `false`     | Whether to stop event propagation           |
| bodyProps                   | `HTMLAttributes<HTMLDivElement>` | `undefined` | Additional props for body element           |
| contentProps                | `HTMLAttributes<HTMLDivElement>` | `undefined` | Additional props for content element        |
| headerProps                 | `HTMLAttributes<HTMLDivElement>` | `undefined` | Additional props for header element         |
| footerProps                 | `HTMLAttributes<HTMLDivElement>` | `undefined` | Additional props for footer element         |
| intermediateState           | `ReactNode`                      | `undefined` | Content to show during intermediate state   |
| onIntermediateStateComplete | `() => void`                     | `undefined` | Callback when intermediate state completes  |

### Import Statement

```typescript
import { Popover } from "gends";
```

## Basic Usage

### Default Popover

```tsx
import { useState } from "react";
import { Button } from "gends";
import { Popover } from "gends";

function MyComponent() {
  const [open, setOpen] = useState(false);

  return (
    <Popover
      open={open}
      onOpenChange={setOpen}
      trigger={<Button onClick={() => setOpen(!open)}>Open Popover</Button>}
      title="My Popover"
    >
      Default popover content
    </Popover>
  );
}
```

## Variants

### Size Variants

#### Small (Default)

```tsx
<Popover size="small" title="Small Popover" trigger={<Button>Open Small Popover</Button>}>
  Compact popover content
</Popover>
```

#### Large

```tsx
<Popover size="large" title="Large Popover" trigger={<Button>Open Large Popover</Button>}>
  More spacious popover content
</Popover>
```

### Content Variants

#### Scrollable Content

```tsx
<Popover
  title="Scrollable Content"
  scrollable={true}
  trigger={<Button>Open Scrollable Popover</Button>}
>
  {Array(50)
    .fill(null)
    .map((_, i) => (
      <div key={i}>Scrollable content line {i + 1}</div>
    ))}
</Popover>
```

#### No Header

```tsx
<Popover hasHeader={false} trigger={<Button>Open Popover Without Header</Button>}>
  Content without header
</Popover>
```

#### No Footer

```tsx
<Popover hasFooter={false} trigger={<Button>Open Popover Without Footer</Button>}>
  Content without footer
</Popover>
```

## Advanced Features

### Custom Header

```tsx
import { Slot } from "gends";

<Popover
  title="Custom Header"
  headerSlotContent={<Slot>Custom Header Content</Slot>}
  trigger={<Button>Open Custom Header Popover</Button>}
>
  Content with custom header
</Popover>;
```

### Custom Buttons

```tsx
<Popover
  title="Custom Buttons"
  primaryButtonLabel="Save Changes"
  secondaryButtonLabel="Discard"
  onPrimaryButtonClick={() => handleSave()}
  onSecondaryButtonClick={() => handleDiscard()}
  trigger={<Button>Open Custom Buttons Popover</Button>}
>
  Content with custom button labels
</Popover>
```

### Intermediate State

```tsx
<Popover
  title="With Intermediate State"
  intermediateState={<div>Processing...</div>}
  onIntermediateStateComplete={() => handleComplete()}
  trigger={<Button>Open Intermediate State Popover</Button>}
>
  Content that shows intermediate state
</Popover>
```

## Real-World Usage Examples

### Form in Popover

```tsx
function FormPopover() {
  const [open, setOpen] = useState(false);
  const [formData, setFormData] = useState({});

  const handleSubmit = () => {
    // Handle form submission
    setOpen(false);
  };

  return (
    <Popover
      open={open}
      onOpenChange={setOpen}
      title="Edit Profile"
      primaryButtonLabel="Save"
      secondaryButtonLabel="Cancel"
      onPrimaryButtonClick={handleSubmit}
      trigger={<Button>Edit Profile</Button>}
    >
      <form className="space-y-4">
        <input
          type="text"
          placeholder="Name"
          onChange={e => setFormData({ ...formData, name: e.target.value })}
        />
        <input
          type="email"
          placeholder="Email"
          onChange={e => setFormData({ ...formData, email: e.target.value })}
        />
      </form>
    </Popover>
  );
}
```

### Confirmation Dialog

```tsx
function ConfirmationPopover() {
  const [open, setOpen] = useState(false);

  const handleConfirm = () => {
    // Handle confirmation
    setOpen(false);
  };

  return (
    <Popover
      open={open}
      onOpenChange={setOpen}
      title="Confirm Action"
      primaryButtonLabel="Delete"
      secondaryButtonLabel="Cancel"
      onPrimaryButtonClick={handleConfirm}
      trigger={<Button>Delete Item</Button>}
    >
      Are you sure you want to delete this item? This action cannot be undone.
    </Popover>
  );
}
```

### Custom Styled Popover

```tsx
<Popover
  title="Custom Styled"
  className="custom-popover"
  contentClassName="custom-content"
  buttonColor="#4B4BFF"
  secondaryButtonColor="#F5F5F5"
  footerColor="#FAFAFA"
  trigger={<Button>Open Custom Styled Popover</Button>}
>
  Content with custom styling
</Popover>
```

## Accessibility Features

### Keyboard Navigation

- **Focus Management**: Proper focus trapping within popover
- **ARIA Attributes**: Appropriate roles and labels
- **Keyboard Shortcuts**: Escape to close, Tab for navigation
- **Focus Return**: Returns focus to trigger when closed

### Screen Reader Support

- **ARIA Labels**: Clear identification of popover purpose
- **Live Regions**: Dynamic content updates announced
- **Role Descriptions**: Proper semantic structure

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Focus Indicators**: Clear visual feedback
- **Motion**: Respects reduced motion preferences

## Design System Integration

### Genesis Design Tokens

**Typography:**

- Title: `text-en-desktop-heading-xl`
- Content: `text-en-desktop-body-m`

**Spacing:**

- Small Header: `h-gd-40 px-gd-12 py-gd-8`
- Large Header: `h-[56px] px-gd-16 py-gd-12`
- Small Content: `px-gd-12 py-gd-16`
- Large Content: `p-gd-16`

**Layout:**

- Width: `w-[364px]`
- Border Radius: `rounded-gd-16`
- Shadow: `shadow-gd-shadow-m`

## Best Practices

### Performance

- Use intermediate states for async operations
- Optimize content rendering
- Handle cleanup properly

### User Experience

- Keep content concise and focused
- Provide clear actions
- Consider mobile interactions
- Handle edge cases gracefully

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle errors appropriately

## Troubleshooting

### Common Issues

**Positioning:**

- Check trigger element
- Verify z-index values
- Review overflow handling

**State Management:**

- Handle open/close properly
- Manage intermediate states
- Clean up timeouts

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

Remember: The Popover component provides a flexible and accessible way to display contextual information and actions. Choose the appropriate configuration based on your specific use case and requirements.
