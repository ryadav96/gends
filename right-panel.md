# Right Panel Component

## Overview

The Right Panel component is a versatile slide-out panel that provides a flexible and accessible way to display supplementary content, forms, or detailed information. Built with Genesis Design System tokens, it offers multiple width variants, expandable functionality, customizable headers and footers, and comprehensive interaction controls. The component is designed to work seamlessly within the MCP context while maintaining full accessibility support.

## Component API

### RightPanel Props

| Prop             | Type                               | Default         | Description                                      |
| ---------------- | ---------------------------------- | --------------- | ------------------------------------------------ |
| title            | `string`                           | `"Page Label"`  | The title displayed in the panel header          |
| subTitle         | `string`                           | `"description"` | Subtitle text displayed below the title          |
| openBtnTitle     | `string`                           | `"Open"`        | Text for the button that opens the panel         |
| width            | `"xs" \| "s" \| "m" \| "l" \| "f"` | `"s"`           | Initial width of the panel                       |
| maxWidth         | `"xs" \| "s" \| "m" \| "l" \| "f"` | `"l"`           | Maximum width when expanded                      |
| extension        | `boolean`                          | `false`         | Whether to show expand/collapse controls         |
| tagText          | `string`                           | `"tag"`         | Text to display in the tag                       |
| showTag          | `boolean`                          | `false`         | Whether to show the tag next to the title        |
| showSubTitle     | `boolean`                          | `false`         | Whether to show the subtitle                     |
| showBack         | `boolean`                          | `false`         | Whether to show the back button                  |
| showFooter       | `boolean`                          | `true`          | Whether to show the footer with action buttons   |
| showSecondaryBtn | `boolean`                          | `true`          | Whether to show the secondary button in footer   |
| showPrimaryBtn   | `boolean`                          | `true`          | Whether to show the primary button in footer     |
| primaryAction    | `() => void`                       | `() => {}`      | Function called when primary button is clicked   |
| secondaryAction  | `() => void`                       | `() => {}`      | Function called when secondary button is clicked |
| backAction       | `() => void`                       | `() => {}`      | Function called when back button is clicked      |
| children         | `ReactNode`                        | `undefined`     | Content to display inside the panel              |
| noTriggerBtn     | `boolean`                          | `false`         | Whether to hide trigger button                   |
| open             | `boolean`                          | `false`         | Controls the open state of the panel             |
| setOpen          | `(open: boolean) => void`          | `() => {}`      | Function to control the open state               |
| trigger          | `ReactNode`                        | `undefined`     | Custom trigger element to open the panel         |

### Import Statement

```typescript
import { RightPanel } from "gends";
```

## Basic Usage

### Default Panel

```tsx
import { RightPanel } from "gends";

function MyComponent() {
  return (
    <RightPanel title="Settings" subTitle="Configure your preferences" openBtnTitle="Open Settings">
      <div className="p-4">
        <h3>Panel Content</h3>
        <p>Your content goes here</p>
      </div>
    </RightPanel>
  );
}
```

## Variants

### Width Variants

#### Extra Small (xs) - 362px

```tsx
<RightPanel width="xs" title="Compact Panel" subTitle="Extra small width variant">
  <div className="p-4">Compact content</div>
</RightPanel>
```

#### Small (s) - 475px

```tsx
<RightPanel width="s" title="Small Panel" subTitle="Small width variant">
  <div className="p-4">Small content</div>
</RightPanel>
```

#### Medium (m) - 700px

```tsx
<RightPanel width="m" title="Medium Panel" subTitle="Medium width variant">
  <div className="p-4">Medium content</div>
</RightPanel>
```

#### Large (l) - 925px

```tsx
<RightPanel width="l" title="Large Panel" subTitle="Large width variant">
  <div className="p-4">Large content</div>
</RightPanel>
```

#### Full (f) - 100vw

```tsx
<RightPanel width="f" title="Full Panel" subTitle="Full width variant">
  <div className="p-4">Full width content</div>
</RightPanel>
```

### Header Variants

#### With Tag

```tsx
<RightPanel title="Panel with Tag" showTag tagText="New">
  <div className="p-4">Content with tag</div>
</RightPanel>
```

#### With Back Button

```tsx
<RightPanel title="Panel with Back" showBack backAction={() => console.log("Back clicked")}>
  <div className="p-4">Content with back button</div>
</RightPanel>
```

#### With Subtitle

```tsx
<RightPanel title="Panel with Subtitle" showSubTitle subTitle="Additional context about this panel">
  <div className="p-4">Content with subtitle</div>
</RightPanel>
```

### Footer Variants

#### Primary Button Only

```tsx
<RightPanel showSecondaryBtn={false} primaryAction={() => console.log("Primary action")}>
  <div className="p-4">Content with primary button only</div>
</RightPanel>
```

#### Secondary Button Only

```tsx
<RightPanel showPrimaryBtn={false} secondaryAction={() => console.log("Secondary action")}>
  <div className="p-4">Content with secondary button only</div>
</RightPanel>
```

#### No Footer

```tsx
<RightPanel showFooter={false}>
  <div className="p-4">Content without footer</div>
</RightPanel>
```

## Advanced Features

### Expandable Panel

```tsx
<RightPanel extension width="s" maxWidth="l" title="Expandable Panel">
  <div className="p-4">
    <p>This panel can be expanded to a larger width</p>
  </div>
</RightPanel>
```

### Custom Trigger

```tsx
<RightPanel noTriggerBtn trigger={<button className="custom-trigger">Custom Open Button</button>}>
  <div className="p-4">Content with custom trigger</div>
</RightPanel>
```

### Controlled State

```tsx
function ControlledPanel() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <RightPanel open={isOpen} setOpen={setIsOpen} title="Controlled Panel">
      <div className="p-4">
        <p>This panel's state is controlled externally</p>
        <button onClick={() => setIsOpen(false)}>Close Panel</button>
      </div>
    </RightPanel>
  );
}
```

## Real-World Usage Examples

### Form Panel

```tsx
function FormPanel() {
  const handleSubmit = () => {
    console.log("Form submitted");
  };

  return (
    <RightPanel
      title="Edit Profile"
      subTitle="Update your personal information"
      primaryAction={handleSubmit}
      secondaryAction={() => console.log("Cancelled")}
    >
      <form className="p-4 space-y-4">
        <div>
          <label>Name</label>
          <input type="text" />
        </div>
        <div>
          <label>Email</label>
          <input type="email" />
        </div>
      </form>
    </RightPanel>
  );
}
```

### Details Panel

```tsx
function DetailsPanel({ item }) {
  return (
    <RightPanel
      title={item.name}
      showTag
      tagText={item.status}
      showBack
      backAction={() => console.log("Back to list")}
    >
      <div className="p-4">
        <h3>Details</h3>
        <p>{item.description}</p>
        <div className="mt-4">
          <h4>Additional Information</h4>
          <ul>
            {item.details.map((detail, index) => (
              <li key={index}>{detail}</li>
            ))}
          </ul>
        </div>
      </div>
    </RightPanel>
  );
}
```

### Multi-step Panel

```tsx
function MultiStepPanel() {
  const [step, setStep] = useState(1);

  return (
    <RightPanel
      title={`Step ${step} of 3`}
      showBack={step > 1}
      backAction={() => setStep(step - 1)}
      primaryAction={() => setStep(step + 1)}
      showPrimaryBtn={step < 3}
    >
      <div className="p-4">
        {step === 1 && <div>Step 1 Content</div>}
        {step === 2 && <div>Step 2 Content</div>}
        {step === 3 && <div>Step 3 Content</div>}
      </div>
    </RightPanel>
  );
}
```

## Accessibility Features

### Keyboard Navigation

- **Focus Management**: Proper focus handling when opening/closing
- **ARIA Attributes**: Appropriate roles and labels
- **Keyboard Shortcuts**: Escape to close
- **Focus Trapping**: Focus remains within panel when open

### Screen Reader Support

- **ARIA Labels**: Clear identification of panel purpose
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
- Subtitle: `text-en-desktop-body-m`

**Spacing:**

- Header Padding: `p-gd-16`
- Content Padding: `p-gd-16`
- Gap Between Elements: `gap-gd-4`

**Colors:**

- Background: `bg-color-background-surface-0`
- Border: `border-color-neutral-grey-40`
- Text: `text-color-neutral-grey-80`

## Best Practices

### Performance

- Use controlled components when needed
- Optimize re-renders
- Handle cleanup properly

### User Experience

- Keep content focused and relevant
- Provide clear navigation options
- Consider mobile interactions
- Handle edge cases gracefully

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle errors appropriately

## Troubleshooting

### Common Issues

**Opening/Closing:**

- Check open state management
- Verify trigger button setup
- Review event handlers

**Styling:**

- Check custom styles
- Verify design tokens
- Review responsive behavior

**Accessibility:**

- Verify ARIA attributes
- Test keyboard navigation
- Check screen reader support

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Right Panel component provides a flexible and accessible way to display supplementary content. Choose the appropriate configuration based on your specific use case and requirements.
