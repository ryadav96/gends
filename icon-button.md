# Icon Button Component

## Overview

The Icon Button component is a versatile and accessible button component built with Genesis Design System tokens. It provides a comprehensive set of variants for different use cases, including multiple sizes, appearances, types, and states. The component is designed for both standalone icon actions and as part of larger UI elements, with complete accessibility support and extensive customization options.

## Component API

### IconButton Props

| Prop         | Type                                                         | Default     | Description                                   |
| ------------ | ------------------------------------------------------------ | ----------- | --------------------------------------------- |
| size         | `"xs" \| "sm" \| "md" \| "lg" \| "xl"`                       | `"md"`      | Size of the icon button                       |
| appearance   | `"default" \| "positive" \| "negative" \| "warning" \| "ai"` | `"default"` | Visual style of the button                    |
| type         | `"primary" \| "secondary" \| "tertiary"`                     | `"primary"` | Type of button                                |
| inverse      | `boolean`                                                    | `false`     | Whether to use inverse styling                |
| selected     | `boolean`                                                    | `false`     | Whether the button is in selected state       |
| icon         | `ReactNode`                                                  | Required    | Icon to display                               |
| onClick      | `(ev: MouseEvent<HTMLButtonElement>) => void`                | `() => {}`  | Click handler                                 |
| disabled     | `boolean`                                                    | `false`     | Whether the button is disabled                |
| classNames   | `{ button?: string; icon?: string; container?: string; }`    | `{}`        | Custom class names for styling                |
| counterbadge | `boolean`                                                    | `false`     | Whether to show a counter badge               |
| id           | `string`                                                     | `""`        | Unique identifier for the button              |
| style        | `React.CSSProperties`                                        | `{}`        | Custom inline styles                          |
| buttonProps  | `ButtonProps`                                                | `{}`        | Additional props to pass to underlying Button |

### Import Statement

```typescript
import { IconButton } from "gends";
```

## Basic Usage

### Default Icon Button

```tsx
import { IcClose } from "gends";

<IconButton icon={<IcClose />} />;
```

### With Different Sizes

```tsx
<div className="flex items-end gap-4">
  <IconButton size="xs" icon={<IcClose />} />
  <IconButton size="sm" icon={<IcClose />} />
  <IconButton size="md" icon={<IcClose />} />
  <IconButton size="lg" icon={<IcClose />} />
  <IconButton size="xl" icon={<IcClose />} />
</div>
```

### With Different Types

```tsx
<div className="flex gap-4">
  <IconButton type="primary" icon={<IcClose />} />
  <IconButton type="secondary" icon={<IcClose />} />
  <IconButton type="tertiary" icon={<IcClose />} />
</div>
```

## Advanced Features

### Appearance Variants

```tsx
<div className="flex gap-4">
  <IconButton appearance="default" icon={<IcClose />} />
  <IconButton appearance="positive" icon={<IcClose />} />
  <IconButton appearance="negative" icon={<IcClose />} />
  <IconButton appearance="warning" icon={<IcClose />} />
  <IconButton appearance="ai" icon={<IcClose />} />
</div>
```

### Inverse Styling

```tsx
<div className="flex gap-4 p-4 bg-gray-800">
  <IconButton appearance="default" inverse icon={<IcClose />} />
  <IconButton appearance="positive" inverse icon={<IcClose />} />
  <IconButton appearance="negative" inverse icon={<IcClose />} />
  <IconButton appearance="warning" inverse icon={<IcClose />} />
</div>
```

### Selected State

```tsx
<div className="flex gap-4">
  <IconButton selected appearance="default" icon={<IcClose />} />
  <IconButton selected appearance="positive" icon={<IcClose />} />
  <IconButton selected appearance="negative" icon={<IcClose />} />
  <IconButton selected appearance="warning" icon={<IcClose />} />
</div>
```

### With Counter Badge

```tsx
<IconButton counterbadge icon={<IcClose />} />
```

## Real-World Usage Examples

### Navigation Actions

```tsx
const NavigationActions = () => {
  return (
    <div className="flex gap-2">
      <IconButton type="tertiary" icon={<IcBack />} onClick={() => handleBack()} />
      <IconButton type="tertiary" icon={<IcForward />} onClick={() => handleForward()} />
      <IconButton type="tertiary" icon={<IcRefresh />} onClick={() => handleRefresh()} />
    </div>
  );
};
```

### Form Actions

```tsx
const FormActions = () => {
  return (
    <div className="flex gap-2">
      <IconButton
        type="secondary"
        appearance="negative"
        icon={<IcDelete />}
        onClick={() => handleDelete()}
      />
      <IconButton
        type="primary"
        appearance="positive"
        icon={<IcSave />}
        onClick={() => handleSave()}
      />
    </div>
  );
};
```

### AI Feature Toggle

```tsx
const AIFeatureToggle = () => {
  const [isEnabled, setIsEnabled] = React.useState(false);

  return (
    <IconButton
      type="secondary"
      appearance="ai"
      selected={isEnabled}
      icon={<IcAiStar />}
      onClick={() => setIsEnabled(!isEnabled)}
    />
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab Navigation**: Focus management through interactive elements
- **Enter/Space**: Activate focused button
- **Focus Management**: Clear focus indicators

### Screen Reader Support

- **ARIA Attributes**: Proper roles and states
- **Icon Labels**: Descriptive labels for screen readers
- **State Announcements**: Clear state changes

### Visual Accessibility

- **Focus Indicators**: Clear focus states
- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Size Variants**: Multiple size options for different needs

## Design System Integration

### Genesis Design Tokens

**Colors:**

- Primary: `var(--gd-primary-50)`, `var(--gd-primary-60)`
- Success: `var(--gd-feedback-success-50)`, `var(--gd-feedback-success-80)`
- Error: `var(--gd-feedback-error-50)`, `var(--gd-feedback-error-80)`
- Warning: `var(--gd-feedback-warning-50)`, `var(--gd-feedback-warning-80)`

**Spacing:**

- `gd-12`: Extra small size
- `gd-16`: Small size
- `gd-20`: Medium size
- `gd-24`: Large size
- `gd-32`: Extra large size

**Typography:**

- Icon sizes match button sizes
- Consistent with Genesis Design System scale

**Border Radius:**

- `rounded-gd-8`: Standard border radius
- `rounded-gd-16`: Large border radius

## Best Practices

### Performance

- Use appropriate icon sizes
- Optimize icon rendering
- Handle state changes efficiently

### User Experience

- Choose appropriate size for context
- Use consistent iconography
- Provide clear visual feedback

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider mobile responsiveness

## Troubleshooting

### Common Issues

**Icon Sizing:**

- Verify icon component size
- Check container dimensions
- Ensure proper scaling

**State Management:**

- Handle disabled state properly
- Manage selected state
- Control inverse styling

**Styling Conflicts:**

- Check custom class names
- Verify style overrides
- Review button props

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Icon Button component provides a flexible and accessible way to implement icon-based actions. Choose the appropriate configuration based on your specific use case and requirements.
