# Button Component

## Overview

The Button component is a highly versatile interactive element that supports multiple variants, sizes, appearances, loading states, icons, and accessibility features. Built with Genesis Design System tokens, it provides consistent styling across themes while offering extensive customization options for different use cases from simple actions to complex AI-powered features.

## Component API

### Button Props

| Prop                 | Type                                                                       | Default     | Description                                       |
| -------------------- | -------------------------------------------------------------------------- | ----------- | ------------------------------------------------- |
| `children`           | `string`                                                                   | `"Click"`   | Button text content (required)                    |
| `size`               | `'xs' \| 's' \| 'm' \| 'l' \| 'xl'`                                        | `'m'`       | Button size controlling dimensions and typography |
| `kind`               | `'primary' \| 'secondary' \| 'tertiary'`                                   | `'primary'` | Button style variant determining visual hierarchy |
| `appearance`         | `'default' \| 'contrast' \| 'positive' \| 'negative' \| 'warning' \| 'ai'` | `'default'` | Color scheme variant for semantic meaning         |
| `loading`            | `boolean`                                                                  | `false`     | Shows loading spinner and disables interaction    |
| `disabled`           | `boolean`                                                                  | `false`     | Disables button and prevents interaction          |
| `fullWidth`          | `boolean`                                                                  | `false`     | Makes button expand to full container width       |
| `prefixIcon`         | `React.ReactNode`                                                          | `undefined` | Icon displayed before the button text             |
| `suffixIcon`         | `React.ReactNode`                                                          | `undefined` | Icon displayed after the button text              |
| `hideUnderline`      | `boolean`                                                                  | `false`     | Hides underline decoration for tertiary buttons   |
| `iconContainerProps` | `React.HTMLAttributes<HTMLSpanElement>`                                    | `undefined` | Props for the icon container elements             |
| `iconProps`          | `React.HTMLAttributes<SVGElement>`                                         | `undefined` | Props passed directly to icon elements            |
| `className`          | `string`                                                                   | `undefined` | Additional CSS classes for custom styling         |
| `onClick`            | `(event: React.MouseEvent<HTMLButtonElement>) => void`                     | `undefined` | Click event handler                               |
| `type`               | `'button' \| 'submit' \| 'reset'`                                          | `'button'`  | HTML button type attribute                        |
| `...props`           | `React.ButtonHTMLAttributes<HTMLButtonElement>`                            | `{}`        | Additional HTML button attributes                 |

## Basic Usage

```tsx
import { Button } from "gends";

// Default primary button
<Button>Click me</Button>

// With custom appearance and size
<Button kind="secondary" appearance="positive" size="l">
  Confirm Action
</Button>

// With icons
<Button prefixIcon={<PlusIcon />} suffixIcon={<ChevronRightIcon />}>
  Add Item
</Button>
```

## Size Variants

The Button component supports five size variants optimized for different use cases:

| Size | Height | Padding     | Font Size | Use Case                    |
| ---- | ------ | ----------- | --------- | --------------------------- |
| `xs` | 24px   | 8px × 4px   | 12px      | Compact spaces, dense UIs   |
| `s`  | 32px   | 12px × 4px  | 14px      | Table actions, inline forms |
| `m`  | 40px   | 16px × 8px  | 14px      | Standard button size        |
| `l`  | 48px   | 20px × 12px | 16px      | Primary CTAs, emphasized    |
| `xl` | 64px   | 32px × 16px | 24px      | Hero sections, landing CTA  |

```tsx
// Size variants
<Button size="xs">Extra Small</Button>
<Button size="s">Small</Button>
<Button size="m">Medium</Button>
<Button size="l">Large</Button>
<Button size="xl">Extra Large</Button>
```

## Button Kinds

### Primary Buttons

Solid background with high visual prominence for main actions:

```tsx
<Button kind="primary" appearance="default">Primary Action</Button>
<Button kind="primary" appearance="positive">Save Changes</Button>
<Button kind="primary" appearance="negative">Delete Item</Button>
<Button kind="primary" appearance="warning">Proceed with Caution</Button>
<Button kind="primary" appearance="ai">Generate with AI</Button>
```

### Secondary Buttons

Outlined style for secondary actions that complement primary buttons:

```tsx
<Button kind="secondary" appearance="default">Secondary Action</Button>
<Button kind="secondary" appearance="positive">Approve</Button>
<Button kind="secondary" appearance="negative">Reject</Button>
<Button kind="secondary" appearance="warning">Review</Button>
<Button kind="secondary" appearance="contrast">Light Theme</Button>
```

### Tertiary Buttons

Text-only buttons for subtle actions and navigation links:

```tsx
<Button kind="tertiary" appearance="default">Learn More</Button>
<Button kind="tertiary" appearance="positive">View Details</Button>
<Button kind="tertiary" appearance="negative">Cancel</Button>
<Button kind="tertiary" hideUnderline>No Underline</Button>
```

## Appearance Variants

### Default Appearance

Standard blue color scheme for general actions:

```tsx
<Button kind="primary" appearance="default">Primary Default</Button>
<Button kind="secondary" appearance="default">Secondary Default</Button>
<Button kind="tertiary" appearance="default">Tertiary Default</Button>
```

### Contrast Appearance

Light colors designed for dark backgrounds:

```tsx
<div className="bg-gray-900 p-4">
  <Button kind="primary" appearance="contrast">
    Light on Dark
  </Button>
  <Button kind="secondary" appearance="contrast">
    Outlined Light
  </Button>
  <Button kind="tertiary" appearance="contrast">
    Text Light
  </Button>
</div>
```

### Positive Appearance

Green color scheme for success and confirmation actions:

```tsx
<Button kind="primary" appearance="positive">Save Changes</Button>
<Button kind="secondary" appearance="positive">Approve Request</Button>
<Button kind="tertiary" appearance="positive">View Success</Button>
```

### Negative Appearance

Red color scheme for destructive and danger actions:

```tsx
<Button kind="primary" appearance="negative">Delete Account</Button>
<Button kind="secondary" appearance="negative">Remove Item</Button>
<Button kind="tertiary" appearance="negative">Cancel Action</Button>
```

### Warning Appearance

Orange color scheme for caution and warning actions:

```tsx
<Button kind="primary" appearance="warning">Proceed Anyway</Button>
<Button kind="secondary" appearance="warning">Review Changes</Button>
<Button kind="tertiary" appearance="warning">See Warnings</Button>
```

### AI Appearance

Special gradient design for AI-powered features (Primary only):

```tsx
<Button kind="primary" appearance="ai" prefixIcon={<SparklesIcon />}>
  Generate with AI
</Button>
```

## Icons and Content

### Icon Positioning

Add icons before or after text content with automatic sizing:

```tsx
// Prefix icon
<Button prefixIcon={<PlusIcon />}>Add New</Button>

// Suffix icon
<Button suffixIcon={<ChevronRightIcon />}>Continue</Button>

// Both icons
<Button prefixIcon={<DownloadIcon />} suffixIcon={<ExternalLinkIcon />}>
  Download File
</Button>
```

### Icon-Only Buttons

Create compact icon-only buttons with screen reader support:

```tsx
<Button size="s" prefixIcon={<EditIcon />} className="px-2">
  <span className="sr-only">Edit item</span>
</Button>

<Button size="m" prefixIcon={<DeleteIcon />} className="px-3" appearance="negative">
  <span className="sr-only">Delete item</span>
</Button>
```

### Custom Icon Styling

Control icon appearance with advanced props:

```tsx
<Button
  prefixIcon={<CustomIcon />}
  iconProps={{ className: "text-blue-500" }}
  iconContainerProps={{ className: "mr-3" }}
>
  Custom Icon Style
</Button>
```

## Loading States

Show loading spinners while preserving button dimensions:

```tsx
const [isSubmitting, setIsSubmitting] = useState(false);

<Button
  loading={isSubmitting}
  onClick={async () => {
    setIsSubmitting(true);
    await submitForm();
    setIsSubmitting(false);
  }}
>
  {isSubmitting ? "Submitting..." : "Submit Form"}
</Button>;
```

### Loading with Different Sizes

Loading spinners automatically scale with button size:

```tsx
<Button size="xs" loading>Small Loading</Button>
<Button size="m" loading>Medium Loading</Button>
<Button size="xl" loading>Large Loading</Button>
```

## Layout Options

### Full Width Buttons

Expand buttons to fill container width:

```tsx
<div className="w-full max-w-md">
  <Button fullWidth kind="primary" size="l">
    Full Width Primary
  </Button>
  <Button fullWidth kind="secondary" className="mt-2">
    Full Width Secondary
  </Button>
</div>
```

### Button Groups

Create cohesive button layouts:

```tsx
// Horizontal button group
<div className="flex gap-3">
  <Button kind="secondary">Cancel</Button>
  <Button kind="primary" appearance="positive">Confirm</Button>
</div>

// Vertical button group
<div className="flex flex-col gap-2 w-full max-w-xs">
  <Button fullWidth>Primary Action</Button>
  <Button fullWidth kind="secondary">Secondary Action</Button>
  <Button fullWidth kind="tertiary">Tertiary Action</Button>
</div>
```

## Advanced Use Cases

### Form Submission

Handle form states with validation:

```tsx
const FormExample = () => {
  const [isValid, setIsValid] = useState(false);
  const [isSubmitting, setIsSubmitting] = useState(false);

  return (
    <form onSubmit={handleSubmit}>
      {/* Form fields */}
      <div className="flex gap-2 mt-4">
        <Button type="button" kind="secondary">
          Cancel
        </Button>
        <Button type="submit" disabled={!isValid} loading={isSubmitting} appearance="positive">
          Submit
        </Button>
      </div>
    </form>
  );
};
```

### Navigation Actions

Create navigational button patterns:

```tsx
// Back/Forward navigation
<div className="flex justify-between">
  <Button
    kind="tertiary"
    prefixIcon={<ChevronLeftIcon />}
    onClick={() => router.back()}
  >
    Back
  </Button>
  <Button
    suffixIcon={<ChevronRightIcon />}
    onClick={() => router.push('/next')}
  >
    Continue
  </Button>
</div>

// Breadcrumb navigation
<div className="flex items-center gap-1">
  <Button kind="tertiary" size="s">Home</Button>
  <ChevronRightIcon className="w-4 h-4 text-gray-400" />
  <Button kind="tertiary" size="s">Products</Button>
  <ChevronRightIcon className="w-4 h-4 text-gray-400" />
  <Button kind="tertiary" size="s" disabled>Current Page</Button>
</div>
```

### Confirmation Dialogs

Implement confirmation patterns:

```tsx
const ConfirmationDialog = ({ onConfirm, onCancel }) => (
  <div className="p-6 bg-white rounded-lg shadow-lg">
    <h2 className="text-lg font-semibold mb-4">Confirm Action</h2>
    <p className="text-gray-600 mb-6">This action cannot be undone.</p>
    <div className="flex gap-3 justify-end">
      <Button kind="secondary" onClick={onCancel}>
        Cancel
      </Button>
      <Button kind="primary" appearance="negative" onClick={onConfirm} prefixIcon={<WarningIcon />}>
        Delete
      </Button>
    </div>
  </div>
);
```

### Multi-Step Workflows

Guide users through processes:

```tsx
const MultiStepWorkflow = ({ currentStep, onNext, onPrevious, onFinish }) => (
  <div className="flex justify-between items-center">
    <Button
      kind="secondary"
      prefixIcon={<ChevronLeftIcon />}
      onClick={onPrevious}
      disabled={currentStep === 1}
    >
      Previous
    </Button>

    <span className="text-sm text-gray-500">Step {currentStep} of 3</span>

    {currentStep < 3 ? (
      <Button suffixIcon={<ChevronRightIcon />} onClick={onNext}>
        Next
      </Button>
    ) : (
      <Button appearance="positive" onClick={onFinish} prefixIcon={<CheckIcon />}>
        Finish
      </Button>
    )}
  </div>
);
```

### AI-Powered Features

Highlight artificial intelligence capabilities:

```tsx
// AI generation button
<Button
  kind="primary"
  appearance="ai"
  size="l"
  prefixIcon={<SparklesIcon />}
  className="mb-4"
>
  Generate with AI
</Button>

// AI suggestion
<Button
  kind="secondary"
  appearance="default"
  prefixIcon={<LightbulbIcon />}
  size="s"
>
  AI Suggestion
</Button>

// Smart automation
<Button
  kind="tertiary"
  appearance="default"
  prefixIcon={<AutomationIcon />}
>
  Auto-complete
</Button>
```

## Accessibility Features

### Keyboard Navigation

Full keyboard support with proper focus management:

```tsx
<Button
  onKeyDown={e => {
    if (e.key === "Enter" || e.key === " ") {
      handleAction();
    }
  }}
>
  Keyboard Accessible
</Button>
```

### Screen Reader Support

Proper ARIA attributes and labels:

```tsx
// Loading state announcement
<Button
  loading={isLoading}
  aria-describedby="loading-description"
>
  Submit
</Button>
<div id="loading-description" className="sr-only">
  {isLoading ? "Submitting form, please wait" : ""}
</div>

// Icon-only buttons
<Button prefixIcon={<CloseIcon />} aria-label="Close dialog">
  <span className="sr-only">Close</span>
</Button>

// Disabled state
<Button disabled aria-describedby="disabled-reason">
  Submit
</Button>
<div id="disabled-reason" className="sr-only">
  Form must be completed before submitting
</div>
```

### Focus Management

Proper focus indication and management:

```tsx
// Focus trap in modals
const Modal = () => {
  const firstButtonRef = useRef(null);

  useEffect(() => {
    firstButtonRef.current?.focus();
  }, []);

  return (
    <div className="modal">
      <Button ref={firstButtonRef}>First Action</Button>
      <Button>Second Action</Button>
    </div>
  );
};
```

## Theming and Customization

### Theme-Aware Colors

Button automatically adapts to Genesis theme system:

```tsx
// Falcon theme
<div className="falcon-theme">
  <Button>Falcon Primary</Button>
</div>

// Phoenix theme
<div className="phoenix-theme">
  <Button>Phoenix Primary</Button>
</div>

// Jarvis theme
<div className="jarvis-theme">
  <Button>Jarvis Primary</Button>
</div>
```

### Custom Styling

Extend button appearance with custom classes:

```tsx
// Custom colors
<Button className="bg-purple-500 hover:bg-purple-600 text-white">
  Custom Purple
</Button>

// Custom spacing
<Button className="px-8 py-4">
  Extra Padding
</Button>

// Custom border radius
<Button className="rounded-none">
  Square Button
</Button>
```

### CSS Variables

Leverage Genesis design tokens:

```css
.custom-button {
  background-color: var(--gd-primary-50);
  color: var(--gd-primary-inverse);
  border-radius: var(--gd-border-radius-button);
}
```

## Performance Considerations

### Loading State Optimization

Prevent layout shift during loading transitions:

```tsx
const OptimizedButton = ({ loading, children, ...props }) => (
  <Button
    loading={loading}
    style={{
      minWidth: loading ? "auto" : "fit-content",
      width: loading ? props.width : "auto",
    }}
    {...props}
  >
    {children}
  </Button>
);
```

### Icon Optimization

Use properly sized icons for better performance:

```tsx
// Prefer SVG icons over bitmap images
import { CheckIcon } from "gends";

<Button prefixIcon={<CheckIcon />}>Optimized Icon</Button>;

// Lazy load heavy icons
const HeavyIcon = lazy(() => import("./HeavyIcon"));

<Button
  prefixIcon={
    <Suspense fallback={<Spinner />}>
      <HeavyIcon />
    </Suspense>
  }
>
  Lazy Icon
</Button>;
```

## Design Tokens Reference

### Color System

| Appearance | Primary Background | Text Color | Border Color | Focus Ring |
| ---------- | ------------------ | ---------- | ------------ | ---------- |
| Default    | `#3535F3`          | `#FFFFFF`  | `#E0E0E0`    | `#000093`  |
| Contrast   | `#FFFFFF`          | `#000093`  | `#E0E0E0`    | `#3535F3`  |
| Positive   | `#25AB21`          | `#FFFFFF`  | `#E0E0E0`    | `#000093`  |
| Negative   | `#F50031`          | `#FFFFFF`  | `#E0E0E0`    | `#000093`  |
| Warning    | `#F06D0F`          | `#FFFFFF`  | `#E0E0E0`    | `#000093`  |
| AI         | Gradient           | `#FFFFFF`  | None         | `#3535F3`  |

### Typography Scale

| Size | Font Size | Font Weight | Line Height |
| ---- | --------- | ----------- | ----------- |
| `xs` | 12px      | 500         | 16px        |
| `s`  | 14px      | 500         | 20px        |
| `m`  | 14px      | 500         | 20px        |
| `l`  | 16px      | 500         | 24px        |
| `xl` | 24px      | 500         | 32px        |

### Spacing System

| Size | Height | Padding X | Padding Y | Icon Size |
| ---- | ------ | --------- | --------- | --------- |
| `xs` | 24px   | 8px       | 4px       | 12px      |
| `s`  | 32px   | 12px      | 4px       | 14px      |
| `m`  | 40px   | 16px      | 8px       | 16px      |
| `l`  | 48px   | 20px      | 12px      | 18px      |
| `xl` | 64px   | 32px      | 16px      | 24px      |

## Troubleshooting

### Common Issues

**Button not responding to clicks:**

```tsx
// Check for event propagation issues
<Button
  onClick={e => {
    e.stopPropagation();
    handleClick();
  }}
>
  Click Me
</Button>
```

**Loading state not working:**

```tsx
// Ensure loading prop is boolean
<Button loading={Boolean(isLoading)}>Submit</Button>
```

**Icons not displaying:**

```tsx
// Verify icon component is valid React element
<Button prefixIcon={React.isValidElement(icon) ? icon : <DefaultIcon />}>With Icon</Button>
```

**Focus ring not visible:**

```tsx
// Ensure focus-visible styles are not overridden
<Button className="focus-visible:ring-4 focus-visible:ring-offset-0">Focusable</Button>
```

### Performance Issues

**Slow rendering with many buttons:**

```tsx
// Use React.memo for static buttons
const MemoizedButton = React.memo(Button);

// Virtualize large lists of buttons
import { FixedSizeList } from "react-window";
```

**Memory leaks with event handlers:**

```tsx
// Use useCallback for event handlers
const handleClick = useCallback(() => {
  // Handler logic
}, [dependencies]);

<Button onClick={handleClick}>Click</Button>;
```

## Migration Guide

### From v1.x to v2.x

```tsx
// OLD v1.x API
<Button variant="primary" color="blue" size="medium">
  Old Button
</Button>

// NEW v2.x API
<Button kind="primary" appearance="default" size="m">
  New Button
</Button>
```

### Breaking Changes

- `variant` prop renamed to `kind`
- `color` prop renamed to `appearance`
- Size values changed: `medium` → `m`, `small` → `s`
- `loading` prop behavior changed to overlay spinner

## Best Practices

### ✅ Do's

- Use semantic appearances (`positive`, `negative`, `warning`)
- Provide loading states for async actions
- Include proper ARIA labels for accessibility
- Use appropriate sizes for context
- Group related buttons logically
- Test keyboard navigation
- Provide visual feedback for interactions

### ❌ Don'ts

- Don't use multiple primary buttons in same context
- Don't disable buttons without explanation
- Don't use tertiary buttons for critical actions
- Don't override focus styles without alternatives
- Don't nest buttons inside other buttons
- Don't use buttons for navigation (use links instead)
- Don't forget loading states for async operations

## Browser Support

- **Chrome**: Latest 2 versions
- **Firefox**: Latest 2 versions
- **Safari**: Latest 2 versions
- **Edge**: Latest 2 versions
- **Mobile Safari**: iOS 14+
- **Chrome Mobile**: Android 8+

## Related Components

- **Input** - Use with buttons for form submissions
- **Modal** - Buttons for dialog actions and controls
- **Card** - Action buttons within content cards
- **Badge** - Status indicators alongside buttons
- **Navigation** - Menu and routing button patterns
