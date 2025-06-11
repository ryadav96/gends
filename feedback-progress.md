# Feedback Progress Component

## Overview

The Feedback Progress component (ProgressBar) is a versatile and accessible progress indicator built with Genesis Design System tokens. It provides clear visual feedback for task completion, loading states, and progress tracking through two distinct variants (linear and circular), four size options, semantic color states, and extensive customization capabilities. The component supports both determinate and visual progress patterns with comprehensive accessibility features.

## Component API

### ProgressBar Props

| Prop         | Type                                             | Default     | Description                                        |
| ------------ | ------------------------------------------------ | ----------- | -------------------------------------------------- |
| value        | `number`                                         | `0`         | Current progress value                             |
| max          | `number`                                         | `100`       | Maximum progress value for percentage calculation  |
| color        | `"default" \| "success" \| "error" \| "warning"` | `"default"` | Semantic color variant determining visual theme    |
| variant      | `"line" \| "circle"`                             | `"line"`    | Visual variant of the progress indicator           |
| size         | `"xs" \| "sm" \| "md" \| "lg"`                   | `"md"`      | Size variant controlling dimensions and typography |
| showLabel    | `boolean`                                        | `true`      | Whether to display the label text                  |
| showValue    | `boolean`                                        | `true`      | Whether to display the progress value              |
| label        | `string`                                         | `""`        | Label text displayed above progress bar            |
| className    | `string`                                         | -           | Additional CSS classes for the container           |
| textStyle    | `React.CSSProperties`                            | `{}`        | Custom styles for the label text                   |
| valueStyle   | `React.CSSProperties`                            | `{}`        | Custom styles for the value text                   |
| circleRadius | `number`                                         | -           | Custom radius for circle variant (in pixels)       |
| strokeWidth  | `number`                                         | -           | Custom stroke width for circle variant             |

### Extended HTML Props

The component extends standard div attributes and supports:

- Event handlers (`onClick`, `onMouseOver`, etc.)
- Data attributes (`data-*`)
- ARIA attributes (`aria-*`)
- Standard HTML attributes (`id`, `role`, etc.)

## Import

```tsx
import { ProgressBar } from "gends";

```

## Progress Variants

### Linear Progress (Default)

Linear progress bars are ideal for showing completion of finite tasks with clear start and end points.

```tsx
<ProgressBar
  variant="line"
  value={75}
  max={100}
  label="Upload Progress"
  color="default"
  size="md"
/>
```

**Characteristics:**

- **Layout**: Horizontal bar with optional label and value
- **Animation**: Smooth width transition with 300ms duration
- **Accessibility**: Full progressbar role and ARIA attributes
- **Use Cases**: File uploads, form completion, download progress, multi-step workflows

### Circular Progress

Circular progress indicators are perfect for compact spaces and continuous feedback scenarios.

```tsx
<ProgressBar variant="circle" value={65} max={100} color="success" size="lg" showValue={true} />
```

**Characteristics:**

- **Layout**: SVG-based circular indicator with centered value
- **Animation**: Smooth stroke-dashoffset transition
- **Positioning**: Value centered for md/lg sizes, inline for xs size
- **Use Cases**: Loading states, dashboards, metrics, compact progress indicators

## Color Variants

### Default Color

Primary color scheme for general progress indication.

```tsx
<ProgressBar value={60} color="default" label="Processing Request" />
```

**Visual Characteristics:**

- **Progress Fill**: `bg-color-primary-50`
- **Text Color**: `var(--gd-primary-60)`
- **Use Cases**: General progress, data processing, standard workflows

### Success Color

Green color scheme for positive progress and completed states.

```tsx
<ProgressBar value={90} color="success" label="Upload Complete" />
```

**Visual Characteristics:**

- **Progress Fill**: `bg-color-feedback-success-50`
- **Text Color**: `var(--gd-feedback-success-80)`
- **Use Cases**: Successful uploads, completed tasks, positive metrics

### Error Color

Red color scheme for error states and failed processes.

```tsx
<ProgressBar value={25} color="error" label="Upload Failed" />
```

**Visual Characteristics:**

- **Progress Fill**: `bg-color-feedback-error-50`
- **Text Color**: `var(--gd-feedback-error-80)`
- **Use Cases**: Failed uploads, error states, critical alerts

### Warning Color

Orange color scheme for warning states and attention-required processes.

```tsx
<ProgressBar value={45} color="warning" label="Connection Unstable" />
```

**Visual Characteristics:**

- **Progress Fill**: `bg-color-feedback-warning-50`
- **Text Color**: `var(--gd-feedback-warning-80)`
- **Use Cases**: Slow processes, warnings, partial failures

## Size Variants

### Extra Small (xs)

```tsx
<ProgressBar size="xs" value={40} label="Compact Progress" />
```

**Linear Specifications:**

- **Height**: `h-gd-2` (2px)
- **Typography**: `text-en-desktop-body-s`
- **Use Cases**: Inline progress, compact UI, status indicators

**Circular Specifications:**

- **Radius**: 8px (16px diameter)
- **Stroke Width**: 2px
- **Value Display**: Inline beside circle (not centered)

### Small (sm)

```tsx
<ProgressBar size="sm" value={55} label="Small Progress" />
```

**Linear Specifications:**

- **Height**: `h-gd-4` (4px)
- **Typography**: `text-en-desktop-body-xs`
- **Use Cases**: Dense layouts, secondary progress indicators

**Circular Specifications:**

- **Radius**: 12px (24px diameter)
- **Stroke Width**: 2px
- **Value Display**: Centered within circle

### Medium (md) - Default

```tsx
<ProgressBar size="md" value={70} label="Standard Progress" />
```

**Linear Specifications:**

- **Height**: `h-[6px]` (6px)
- **Typography**: `text-en-desktop-body-m`
- **Use Cases**: Standard progress bars, forms, general use

**Circular Specifications:**

- **Radius**: 24px (48px diameter)
- **Stroke Width**: 4px
- **Value Display**: Centered within circle

### Large (lg)

```tsx
<ProgressBar size="lg" value={85} label="Prominent Progress" />
```

**Linear Specifications:**

- **Height**: `h-gd-8` (8px)
- **Typography**: `text-en-desktop-heading-xl`
- **Use Cases**: Primary progress indicators, hero sections

**Circular Specifications:**

- **Radius**: 36px (72px diameter)
- **Stroke Width**: 8px
- **Value Display**: Centered within circle

## Advanced Features

### Custom Maximum Values

Set custom maximum values for different scales and contexts.

```tsx
<ProgressBar value={150} max={200} label="Custom Maximum (200)" color="success" />
```

**Use Cases:**

- Custom scoring systems
- Non-percentage based progress
- Multi-scale indicators

### Custom Circle Sizing

Control exact circle dimensions with `circleRadius` prop.

```tsx
{
  /* Default sizing */
}
<ProgressBar variant="circle" value={75} size="md" />;

{
  /* Custom 60px radius */
}
<ProgressBar variant="circle" value={75} size="md" circleRadius={60} />;

{
  /* Large 100px radius */
}
<ProgressBar variant="circle" value={75} size="md" circleRadius={100} />;
```

**Benefits:**

- Precise sizing for specific layouts
- Maintains consistent stroke proportions
- Custom dimensions for design requirements

### Custom Stroke Width

Control circle stroke thickness independently of size.

```tsx
<ProgressBar variant="circle" value={80} size="md" circleRadius={50} strokeWidth={6} />
```

### Text and Value Styling

Customize label and value appearance with inline styles.

```tsx
<ProgressBar
  value={65}
  label="Custom Styled Progress"
  textStyle={{ fontWeight: "bold", color: "#333" }}
  valueStyle={{ fontSize: "18px", color: "#007bff" }}
/>
```

### Hidden Labels and Values

Control visibility of labels and values independently.

```tsx
{
  /* Value only */
}
<ProgressBar value={75} showLabel={false} showValue={true} />;

{
  /* Label only */
}
<ProgressBar value={75} label="Processing..." showLabel={true} showValue={false} />;

{
  /* Neither (visual only) */
}
<ProgressBar value={75} showLabel={false} showValue={false} />;
```

## Real-World Usage Examples

### File Upload Progress

```tsx
const FileUploadProgress = () => {
  const [uploadProgress, setUploadProgress] = useState(0);

  return (
    <div className="w-full max-w-md">
      <ProgressBar
        value={uploadProgress}
        max={100}
        color={uploadProgress === 100 ? "success" : "default"}
        label="Uploading file..."
        size="md"
        variant="line"
      />
    </div>
  );
};
```

### Dashboard Metrics

```tsx
const DashboardMetrics = () => (
  <div className="grid grid-cols-2 gap-6">
    <div className="text-center">
      <h3 className="mb-2">CPU Usage</h3>
      <ProgressBar
        variant="circle"
        value={72}
        max={100}
        color="warning"
        size="lg"
        showLabel={false}
      />
    </div>
    <div className="text-center">
      <h3 className="mb-2">Memory</h3>
      <ProgressBar
        variant="circle"
        value={45}
        max={100}
        color="success"
        size="lg"
        showLabel={false}
      />
    </div>
  </div>
);
```

### Multi-Step Form Progress

```tsx
const FormStepProgress = ({ currentStep, totalSteps }) => (
  <div className="mb-8">
    <ProgressBar
      value={currentStep}
      max={totalSteps}
      label={`Step ${currentStep} of ${totalSteps}`}
      color="default"
      size="sm"
      variant="line"
    />
  </div>
);
```

### Loading State Indicators

```tsx
const LoadingIndicators = () => (
  <div className="space-y-4">
    {/* Compact loading */}
    <div className="flex items-center gap-3">
      <ProgressBar variant="circle" value={0} size="xs" showValue={false} showLabel={false} />
      <span>Loading...</span>
    </div>

    {/* Standard loading */}
    <ProgressBar value={0} label="Please wait..." showValue={false} size="md" />
  </div>
);
```

### Progress Variants Showcase

```tsx
const ProgressShowcase = () => (
  <div className="space-y-8">
    {/* Color variants */}
    <div className="space-y-4">
      <h3>Color Variants</h3>
      <ProgressBar value={60} color="default" label="Default Progress" />
      <ProgressBar value={60} color="success" label="Success Progress" />
      <ProgressBar value={60} color="error" label="Error Progress" />
      <ProgressBar value={60} color="warning" label="Warning Progress" />
    </div>

    {/* Size variants */}
    <div className="space-y-4">
      <h3>Size Variants</h3>
      <ProgressBar value={60} size="xs" label="Extra Small" />
      <ProgressBar value={60} size="sm" label="Small" />
      <ProgressBar value={60} size="md" label="Medium" />
      <ProgressBar value={60} size="lg" label="Large" />
    </div>

    {/* Circle variants */}
    <div className="flex gap-8 flex-wrap">
      <ProgressBar variant="circle" value={25} color="default" size="xs" />
      <ProgressBar variant="circle" value={50} color="success" size="sm" />
      <ProgressBar variant="circle" value={75} color="error" size="md" />
      <ProgressBar variant="circle" value={100} color="warning" size="lg" />
    </div>
  </div>
);
```

## Accessibility Features

### ARIA Attributes

The component includes comprehensive accessibility support:

```tsx
<ProgressBar
  value={75}
  max={100}
  label="Upload Progress"
  // Automatically includes:
  // role="progressbar"
  // aria-valuenow={75}
  // aria-valuemin={0}
  // aria-valuemax={100}
  // aria-label="Upload Progress"
/>
```

### Screen Reader Support

- **Linear Variant**: Uses semantic `role="progressbar"` with complete ARIA attributes
- **Circular Variant**: SVG includes `role="img"` with accessible structure
- **Value Announcements**: Progress values are announced by screen readers
- **Label Association**: Labels are properly associated with progress indicators

### Keyboard Navigation

- Progress bars are focusable when interactive
- Support for standard keyboard navigation patterns
- Value changes are announced to assistive technologies

## Design Token Specifications

### Color System

| Color   | Progress Fill Token            | Text Color Token                |
| ------- | ------------------------------ | ------------------------------- |
| Default | `bg-color-primary-50`          | `var(--gd-primary-60)`          |
| Success | `bg-color-feedback-success-50` | `var(--gd-feedback-success-80)` |
| Error   | `bg-color-feedback-error-50`   | `var(--gd-feedback-error-80)`   |
| Warning | `bg-color-feedback-warning-50` | `var(--gd-feedback-warning-80)` |

### Typography Scale

| Size | Typography Token             | Font Size | Line Height |
| ---- | ---------------------------- | --------- | ----------- |
| xs   | `text-en-desktop-body-s`     | 12px      | 16px        |
| sm   | `text-en-desktop-body-xs`    | 11px      | 14px        |
| md   | `text-en-desktop-body-m`     | 14px      | 20px        |
| lg   | `text-en-desktop-heading-xl` | 18px      | 24px        |

### Spacing System

| Element          | Spacing Token              | Value |
| ---------------- | -------------------------- | ----- |
| Content Gap      | `space-y-gd-16`            | 16px  |
| Track Background | `bg-color-neutral-grey-40` | -     |
| Border Radius    | `rounded-full`             | 250px |

### Height Specifications

| Size | Height Token | Height Value |
| ---- | ------------ | ------------ |
| xs   | `h-gd-2`     | 2px          |
| sm   | `h-gd-4`     | 4px          |
| md   | `h-[6px]`    | 6px          |
| lg   | `h-gd-8`     | 8px          |

### Circle Specifications

| Size | Radius | Diameter | Stroke Width |
| ---- | ------ | -------- | ------------ |
| xs   | 8px    | 16px     | 2px          |
| sm   | 12px   | 24px     | 2px          |
| md   | 24px   | 48px     | 4px          |
| lg   | 36px   | 72px     | 8px          |

## Best Practices

### When to Use

**Linear Progress:**

- File uploads and downloads
- Form completion progress
- Multi-step workflows
- Data processing tasks
- Installation progress

**Circular Progress:**

- Loading states
- Dashboard metrics
- Compact spaces
- Real-time indicators
- Achievement progress

### Performance Considerations

- Use CSS transitions for smooth animations
- Avoid frequent value updates (debounce if necessary)
- Consider using `transform` properties for better performance
- Implement proper cleanup for dynamic progress tracking

### Visual Design Guidelines

- Maintain consistent sizing within interface sections
- Use semantic colors appropriately (success for completion, error for failures)
- Provide clear labels for context
- Consider contrast ratios for accessibility
- Use appropriate sizes for the interface hierarchy

### Content Guidelines

- Keep labels concise and descriptive
- Use present tense for ongoing processes ("Uploading...", "Processing...")
- Include context when helpful ("Step 2 of 5", "75% complete")
- Provide clear completion states

## Integration Examples

### With React Hook Form

```tsx
const ProgressForm = () => {
  const { watch, formState } = useForm();
  const watchedFields = watch();

  const completedFields = Object.values(watchedFields).filter(
    value => value && value !== ""
  ).length;
  const totalFields = 5;

  return (
    <div>
      <ProgressBar
        value={completedFields}
        max={totalFields}
        label="Form Completion"
        color={completedFields === totalFields ? "success" : "default"}
        size="sm"
      />
      {/* Form fields */}
    </div>
  );
};
```

### With State Management

```tsx
const useUploadProgress = () => {
  const [progress, setProgress] = useState(0);
  const [status, setStatus] = useState<"idle" | "uploading" | "success" | "error">("idle");

  const uploadFile = async (file: File) => {
    setStatus("uploading");
    setProgress(0);

    try {
      // Upload simulation
      const interval = setInterval(() => {
        setProgress(prev => {
          if (prev >= 100) {
            clearInterval(interval);
            setStatus("success");
            return 100;
          }
          return prev + 10;
        });
      }, 200);
    } catch (error) {
      setStatus("error");
    }
  };

  return { progress, status, uploadFile };
};

const UploadComponent = () => {
  const { progress, status, uploadFile } = useUploadProgress();

  const getColor = () => {
    switch (status) {
      case "success":
        return "success";
      case "error":
        return "error";
      default:
        return "default";
    }
  };

  return (
    <ProgressBar
      value={progress}
      max={100}
      color={getColor()}
      label={`Upload ${status === "success" ? "Complete" : "Progress"}`}
      size="md"
    />
  );
};
```

## Troubleshooting

### Common Issues

**Progress Not Updating:**

- Ensure `value` prop is being updated
- Check that `max` prop is set correctly
- Verify percentage calculation: `(value / max) * 100`

**Circle Not Rendering:**

- Check `circleRadius` is positive number
- Ensure `strokeWidth` doesn't exceed radius
- Verify SVG viewBox calculations

**Styling Issues:**

- Use `textStyle` and `valueStyle` for text customization
- Apply `className` to container for layout adjustments
- Check CSS specificity for style overrides

**Performance Issues:**

- Debounce rapid value updates
- Avoid updating progress more than 60fps
- Use `transform` properties for animations

### Migration Notes

When upgrading from previous versions:

- `variant` prop replaces deprecated `type` prop
- `circleRadius` replaces `size` for custom circle dimensions
- Color tokens now use Genesis Design System variables
- Typography follows new Genesis scale

Remember: The Feedback Progress component is designed to provide clear, accessible progress indication across all variants and use cases while maintaining consistency with the Genesis Design System.
