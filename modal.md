# Modal Component

## Overview

The Modal component is a versatile and accessible dialog overlay built with Genesis Design System tokens. It provides a comprehensive set of features for creating interactive dialogs, including multiple size options, customizable header and footer sections, support for both controlled and uncontrolled usage patterns, and extensive accessibility features. The component is designed for various use cases such as confirmations, forms, alerts, and complex workflows.

## Component API

### Modal Props

| Prop                 | Type                               | Default                                                                            | Description                                      |
| -------------------- | ---------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------ |
| children             | `ReactNode`                        | `<>`                                                                               | Main content of the modal                        |
| modalButton          | `ReactNode`                        | `undefined`                                                                        | Custom trigger button component                  |
| acknowledgement      | `boolean`                          | `false`                                                                            | Centers content for acknowledgement-style modals |
| closeAction          | `boolean`                          | `false`                                                                            | Whether clicking outside closes the modal        |
| customWidth          | `string`                           | `undefined`                                                                        | Custom width override (e.g., '800px')            |
| description          | `string`                           | `""`                                                                               | Main descriptive text                            |
| headerTitle          | `string`                           | `"Leave page with unsaved changes?"`                                               | Title text in modal header                       |
| size                 | `"xs" \| "s" \| "m" \| "l" \| "f"` | `"m"`                                                                              | Modal width variant                              |
| btnTitle             | `string`                           | `"Open"`                                                                           | Text for trigger button                          |
| showPrimaryBtn       | `boolean`                          | `true`                                                                             | Whether to show primary button                   |
| showSecondaryBtn     | `boolean`                          | `true`                                                                             | Whether to show secondary button                 |
| primaryClose         | `boolean`                          | `false`                                                                            | Whether primary button closes modal              |
| secondaryClose       | `boolean`                          | `true`                                                                             | Whether secondary button closes modal            |
| open                 | `boolean`                          | `undefined`                                                                        | Controlled open state                            |
| setOpen              | `(open: boolean) => void`          | `() => {}`                                                                         | Function to update open state                    |
| noTriggerBtn         | `boolean`                          | `false`                                                                            | Whether to hide trigger button                   |
| headerClasses        | `string`                           | `"bg-color-background-surface-20..."`                                              | Custom CSS classes for header                    |
| footerClasses        | `string`                           | `"py-gd-16 px-gd-24..."`                                                           | Custom CSS classes for footer                    |
| showFooter           | `boolean`                          | `true`                                                                             | Whether to show footer section                   |
| noPadding            | `boolean`                          | `false`                                                                            | Whether to remove content padding                |
| showDesc             | `boolean`                          | `true`                                                                             | Whether to show description                      |
| footerSlot           | `ReactNode`                        | `undefined`                                                                        | Additional footer content                        |
| footer               | `ReactNode`                        | `undefined`                                                                        | Custom footer component                          |
| headerSlot           | `ReactNode`                        | `undefined`                                                                        | Additional header content                        |
| header               | `ReactNode`                        | `undefined`                                                                        | Custom header component                          |
| supportText          | `string`                           | `undefined`                                                                        | Additional text below header title               |
| showBackButton       | `boolean`                          | `false`                                                                            | Whether to show back button                      |
| primaryButtonProps   | `ButtonProps`                      | `{ onClick: () => {}, disabled: false, title: "Primary Button", kind: "primary" }` | Primary button configuration                     |
| secondaryButtonProps | `ButtonProps`                      | `{ onClick: () => {}, disabled: false, title: "Cancel", kind: "secondary" }`       | Secondary button configuration                   |
| onBack               | `() => void`                       | `undefined`                                                                        | Back button click handler                        |
| hideFooterShadow     | `boolean`                          | `false`                                                                            | Whether to hide footer shadow                    |

### Import Statement

```typescript
import { Modal } from "gends";
```

## Basic Usage

### Default Modal

```tsx
<Modal
  headerTitle="Confirm Action"
  description="Are you sure you want to proceed with this action?"
  primaryButtonProps={{
    title: "Confirm",
    onClick: () => console.log("Confirmed"),
  }}
  secondaryButtonProps={{
    title: "Cancel",
    onClick: () => console.log("Cancelled"),
  }}
/>
```

### Size Variants

```tsx
<div className="space-y-4">
  <Modal size="xs" headerTitle="Small Modal" description="Compact alert or simple confirmation" />

  <Modal size="s" headerTitle="Standard Modal" description="Forms or confirmations with details" />

  <Modal size="m" headerTitle="Medium Modal" description="Default size for most content" />

  <Modal size="l" headerTitle="Large Modal" description="Complex forms or data-heavy displays" />

  <Modal size="f" headerTitle="Full Width Modal" description="Immersive experiences" />
</div>
```

### Controlled Usage

```tsx
const [isOpen, setIsOpen] = useState(false);

<Modal
  open={isOpen}
  setOpen={setIsOpen}
  noTriggerBtn={true}
  headerTitle="Controlled Modal"
  description="This modal is controlled by parent component state"
  primaryButtonProps={{
    title: "Close",
    onClick: () => setIsOpen(false),
  }}
/>;
```

## Advanced Features

### Custom Header and Footer

```tsx
<Modal
  headerTitle="Custom Layout"
  header={
    <div className="flex items-center justify-between p-4 bg-primary-50">
      <h2 className="text-xl font-bold">Custom Header</h2>
      <button onClick={() => setOpen(false)}>Close</button>
    </div>
  }
  footer={
    <div className="flex justify-end gap-4 p-4">
      <button className="px-4 py-2 bg-gray-200">Cancel</button>
      <button className="px-4 py-2 bg-primary-500 text-white">Submit</button>
    </div>
  }
>
  <div className="p-4">Custom content here</div>
</Modal>
```

### Acknowledgement Style

```tsx
<Modal
  acknowledgement={true}
  headerTitle="Success!"
  description="Your changes have been saved successfully."
  primaryButtonProps={{
    title: "OK",
    onClick: () => setOpen(false),
  }}
  showSecondaryBtn={false}
/>
```

### With Back Navigation

```tsx
<Modal
  showBackButton={true}
  onBack={() => console.log("Back clicked")}
  headerTitle="Multi-step Process"
  description="Step 2 of 3"
  primaryButtonProps={{
    title: "Next",
    onClick: () => console.log("Next clicked"),
  }}
  secondaryButtonProps={{
    title: "Cancel",
    onClick: () => setOpen(false),
  }}
/>
```

## Real-World Usage Examples

### Confirmation Dialog

```tsx
const DeleteConfirmation = ({ onConfirm, onCancel }) => {
  return (
    <Modal
      size="s"
      headerTitle="Delete Item"
      description="Are you sure you want to delete this item? This action cannot be undone."
      primaryButtonProps={{
        title: "Delete",
        kind: "destructive",
        onClick: onConfirm,
      }}
      secondaryButtonProps={{
        title: "Cancel",
        onClick: onCancel,
      }}
    />
  );
};
```

### Form Modal

```tsx
const UserFormModal = ({ onSubmit, onCancel }) => {
  return (
    <Modal
      size="m"
      headerTitle="Edit User Profile"
      primaryButtonProps={{
        title: "Save Changes",
        onClick: onSubmit,
      }}
      secondaryButtonProps={{
        title: "Cancel",
        onClick: onCancel,
      }}
    >
      <form className="space-y-4 p-4">
        <div>
          <label>Name</label>
          <input type="text" className="w-full" />
        </div>
        <div>
          <label>Email</label>
          <input type="email" className="w-full" />
        </div>
      </form>
    </Modal>
  );
};
```

### Multi-step Process

```tsx
const MultiStepModal = ({ currentStep, onNext, onBack }) => {
  const steps = [
    { title: "Basic Information", description: "Step 1 of 3" },
    { title: "Contact Details", description: "Step 2 of 3" },
    { title: "Review", description: "Step 3 of 3" },
  ];

  return (
    <Modal
      showBackButton={currentStep > 0}
      onBack={onBack}
      headerTitle={steps[currentStep].title}
      description={steps[currentStep].description}
      primaryButtonProps={{
        title: currentStep === 2 ? "Submit" : "Next",
        onClick: onNext,
      }}
      secondaryButtonProps={{
        title: "Cancel",
        onClick: () => setOpen(false),
      }}
    >
      {/* Step content */}
    </Modal>
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab Navigation**: Focus management through interactive elements
- **Escape Key**: Closes modal
- **Enter/Space**: Activates focused buttons
- **Focus Management**: Traps focus within modal when open

### Screen Reader Support

- **ARIA Attributes**: Proper roles and states
- **Modal Title**: Clear identification of modal purpose
- **Focus Management**: Returns focus to trigger element when closed

### Visual Accessibility

- **Focus Indicators**: Clear focus states
- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Size Variants**: Multiple size options for different needs

## Design System Integration

### Genesis Design Tokens

**Colors:**

- Background: `var(--gd-background-surface-20)`, `var(--gd-background-surface-0)`
- Text: `var(--gd-text-subdued-1)`, `var(--gd-text-subdued-2)`

**Typography:**

- Header: `text-en-desktop-heading-xl`
- Description: `text-en-desktop-body-m`

**Spacing:**

- Header: `py-gd-12 px-gd-16`
- Footer: `py-gd-16 px-gd-24`
- Content: `p-gd-16`

**Shadows:**

- Modal: `shadow-[0px_4px_16px_0px_hsla(0,0%,0%,0.16)]`

## Best Practices

### Performance

- Use appropriate size variants
- Optimize content rendering
- Handle state changes efficiently

### User Experience

- Choose appropriate size for content
- Use clear, concise titles
- Provide clear action buttons
- Consider mobile responsiveness

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle errors gracefully

## Troubleshooting

### Common Issues

**Modal Positioning:**

- Check z-index values
- Verify parent container styles
- Review stacking context

**Content Overflow:**

- Use appropriate size variant
- Consider scrollable content
- Check padding and margins

**State Management:**

- Handle controlled/uncontrolled modes
- Manage focus properly
- Control animation states

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Modal component provides a flexible and accessible way to create dialog overlays. Choose the appropriate configuration based on your specific use case and requirements.
