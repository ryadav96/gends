# Badge Component

## Overview

The Badge component is a small, compact label used to highlight status, category, or numeric values. It provides clear visual feedback through semantic color palettes and supports customizable content including text, icons, and React elements. The component offers five appearance variants, four size options, and two visual intensities (standard and subtle) for maximum flexibility.

## Component API

### Badge Props

| Prop           | Type                                                          | Default     | Description                                              |
| -------------- | ------------------------------------------------------------- | ----------- | -------------------------------------------------------- |
| `size`         | `"xs" \| "s" \| "m" \| "l"`                                   | `"m"`       | Size variant controlling dimensions and typography       |
| `appearance`   | `"Default" \| "Success" \| "Error" \| "Warning" \| "Neutral"` | `"Default"` | Color theme and semantic meaning of the badge            |
| `subtle`       | `boolean`                                                     | `false`     | Whether to use subtle (light) or intense (solid) styling |
| `text`         | `string`                                                      | `"label"`   | Text content to display in the badge                     |
| `icon`         | `React.ReactNode`                                             | `undefined` | Icon element to display before the text                  |
| `children`     | `React.ReactNode`                                             | `undefined` | Custom content (overrides text if provided)              |
| `classNames`   | `ClassNames`                                                  | `{}`        | Custom class names for different parts of the badge      |
| `customStyles` | `CustomStyles`                                                | `{}`        | Inline styles for complete customization                 |

### ClassNames Interface

```typescript
interface ClassNames {
  badgeContainerClasses?: string; // Custom classes for the main badge container
  iconContainerClasses?: string; // Custom classes for the icon wrapper
  textClasses?: string; // Custom classes for the text content
}
```

### CustomStyles Interface

```typescript
interface CustomStyles {
  backgroundColor?: string; // Custom background color
  textColor?: string; // Custom text color
  padding?: string; // Custom padding
  height?: string; // Custom height
  borderRadius?: string; // Custom border radius
  iconColor?: string; // Custom icon color
}
```

## Basic Usage

### Default Badge

The simplest badge with default styling and medium size.

```tsx
import { Badge } from "gends";

<Badge text="Default Badge" />;
```

### Badge with Custom Content

Use children prop for custom content instead of simple text.

```tsx
<Badge>
  <span>Custom Content</span>
</Badge>
```

## Size Variants

Badge supports four size variants for different UI contexts and information hierarchy.

### Extra Small (xs)

Height: 20px, Text: 12px (body-s)

```tsx
<Badge size="xs" text="XS Badge" />
```

### Small (s)

Height: 24px, Text: 12px (body-s)

```tsx
<Badge size="s" text="Small Badge" />
```

### Medium (m) - Default

Height: 28px, Text: 14px (body-m)

```tsx
<Badge size="m" text="Medium Badge" />
```

### Large (l)

Height: 32px, Text: 16px (body-l)

```tsx
<Badge size="l" text="Large Badge" />
```

### Size Comparison

```tsx
<div className="flex gap-2 items-center">
  <Badge size="xs" text="XS" />
  <Badge size="s" text="Small" />
  <Badge size="m" text="Medium" />
  <Badge size="l" text="Large" />
</div>
```

## Appearance Variants

Badge provides five semantic color themes for different contexts and meanings.

### Default Appearance

Primary brand colors for general use.

```tsx
<Badge appearance="Default" text="Default" />
```

### Success Appearance

Green colors for positive states and successful actions.

```tsx
<Badge appearance="Success" text="Success" />
```

### Error Appearance

Red colors for error states and critical alerts.

```tsx
<Badge appearance="Error" text="Error" />
```

### Warning Appearance

Yellow/orange colors for warning states and caution alerts.

```tsx
<Badge appearance="Warning" text="Warning" />
```

### Neutral Appearance

Grey colors for neutral states and inactive elements.

```tsx
<Badge appearance="Neutral" text="Neutral" />
```

### Appearance Comparison

```tsx
<div className="flex gap-2 flex-wrap">
  <Badge appearance="Default" text="Default" />
  <Badge appearance="Success" text="Success" />
  <Badge appearance="Error" text="Error" />
  <Badge appearance="Warning" text="Warning" />
  <Badge appearance="Neutral" text="Neutral" />
</div>
```

## Visual Intensity Variants

Control the visual prominence with subtle and intense styling options.

### Intense Styling (Default)

Solid background with high contrast for maximum visibility.

```tsx
<Badge appearance="Success" subtle={false} text="Intense" />
```

### Subtle Styling

Light background with reduced contrast for softer appearance.

```tsx
<Badge appearance="Success" subtle={true} text="Subtle" />
```

### Intensity Comparison

```tsx
<div className="space-y-2">
  <div className="flex gap-2">
    <Badge appearance="Default" subtle={false} text="Intense Default" />
    <Badge appearance="Success" subtle={false} text="Intense Success" />
    <Badge appearance="Error" subtle={false} text="Intense Error" />
  </div>
  <div className="flex gap-2">
    <Badge appearance="Default" subtle={true} text="Subtle Default" />
    <Badge appearance="Success" subtle={true} text="Subtle Success" />
    <Badge appearance="Error" subtle={true} text="Subtle Error" />
  </div>
</div>
```

## Icon Integration

Add icons to badges for enhanced visual communication and context.

### Badge with Icon

```tsx
import { IcFavorite } from "gends";

<Badge icon={<IcFavorite />} text="Favorite" appearance="Success" size="l" />;
```

### Different Icons with Sizes

```tsx
import { IcError, IcWarning, IcCheck } from "gends";

<div className="flex gap-2">
  <Badge size="s" icon={<IcCheck />} text="Complete" appearance="Success" />
  <Badge size="m" icon={<IcWarning />} text="Warning" appearance="Warning" />
  <Badge size="l" icon={<IcError />} text="Error" appearance="Error" />
</div>;
```

### Icon Color Inheritance

Icons automatically inherit colors based on appearance and subtle mode.

```tsx
// Intense mode: icons use white color
<Badge icon={<IcFavorite />} text="Intense" appearance="Default" subtle={false} />

// Subtle mode: icons use theme color
<Badge icon={<IcFavorite />} text="Subtle" appearance="Default" subtle={true} />
```

## Customization Options

### Custom Classes

Apply custom styling through the classNames prop for fine-grained control.

```tsx
<Badge
  text="Custom Styled"
  classNames={{
    badgeContainerClasses: "shadow-lg border border-blue-300",
    iconContainerClasses: "opacity-80",
    textClasses: "font-bold tracking-wide",
  }}
  icon={<IcFavorite />}
/>
```

### Custom Inline Styles

Use customStyles for complete visual customization.

```tsx
<Badge
  text="Custom Badge"
  customStyles={{
    backgroundColor: "#1f2937",
    textColor: "#f9fafb",
    borderRadius: "16px",
    padding: "6px 12px",
    height: "auto",
  }}
/>
```

### Custom Icon Color

Override icon colors independently from the theme.

```tsx
<Badge
  icon={<IcFavorite />}
  text="Custom Icon"
  customStyles={{
    iconColor: "#ff6b6b",
  }}
/>
```

## Advanced Use Cases

### Status Indicators

Use badges to show various system or content states.

```tsx
// Online status
<Badge size="s" appearance="Success" text="Online" />

// Offline status
<Badge size="s" appearance="Neutral" text="Offline" />

// Pending status
<Badge size="s" appearance="Warning" text="Pending" />

// Failed status
<Badge size="s" appearance="Error" text="Failed" />
```

### Category Labels

Create category badges with subtle styling for content organization.

```tsx
<div className="flex gap-2">
  <Badge subtle appearance="Default" text="Technology" />
  <Badge subtle appearance="Success" text="Finance" />
  <Badge subtle appearance="Warning" text="Marketing" />
  <Badge subtle appearance="Neutral" text="Design" />
</div>
```

### Numeric Badges

Display counts and numeric values with appropriate sizing.

```tsx
// Small numeric badges
<Badge size="xs" text="5" appearance="Error" />
<Badge size="s" text="23" appearance="Warning" />

// Larger numeric displays
<Badge size="m" text="156" appearance="Success" />
<Badge size="l" text="1,234" appearance="Default" />
```

### Priority Indicators

Use different appearances to communicate priority levels.

```tsx
<div className="space-y-2">
  <div className="flex items-center gap-2">
    <Badge size="s" appearance="Error" text="Critical" />
    <span>Critical priority item</span>
  </div>
  <div className="flex items-center gap-2">
    <Badge size="s" appearance="Warning" text="High" />
    <span>High priority item</span>
  </div>
  <div className="flex items-center gap-2">
    <Badge size="s" appearance="Success" text="Normal" />
    <span>Normal priority item</span>
  </div>
  <div className="flex items-center gap-2">
    <Badge size="s" appearance="Neutral" text="Low" />
    <span>Low priority item</span>
  </div>
</div>
```

### Pill-shaped Badges

Create rounded badges for modern UI design.

```tsx
<Badge
  text="Pill Badge"
  subtle
  customStyles={{
    borderRadius: "9999px",
    padding: "4px 12px",
  }}
/>
```

### Badge with Complex Content

Use children prop for complex content structures.

```tsx
<Badge size="l" appearance="Success">
  <div className="flex items-center gap-1">
    <IcCheck className="text-[12px]" />
    <span>Verified</span>
    <span className="text-[10px] opacity-75">✓</span>
  </div>
</Badge>
```

## Color Theme Reference

### Default Theme

- **Subtle**: Primary-20 background, Primary-60 text
- **Intense**: Primary-60 background, white text
- **Use**: General purpose, brand-related content

### Success Theme

- **Subtle**: Success-20 background, Success-80 text
- **Intense**: Success-50 background, white text
- **Use**: Positive states, completed actions, success messages

### Error Theme

- **Subtle**: Error-20 background, Error-80 text
- **Intense**: Error-50 background, white text
- **Use**: Error states, critical alerts, failed actions

### Warning Theme

- **Subtle**: Warning-20 background, Warning-80 text
- **Intense**: Warning-50 background, white text
- **Use**: Warning states, caution alerts, pending actions

### Neutral Theme

- **Subtle**: Grey-40 background, Grey-80 text
- **Intense**: Grey-80 background, white text
- **Use**: Inactive states, neutral information, secondary content

## Size and Spacing Reference

| Size | Height | Typography    | Icon Size | Padding | Use Case                |
| ---- | ------ | ------------- | --------- | ------- | ----------------------- |
| `xs` | 20px   | body-s (12px) | 12px      | 4px     | Compact lists, dense UI |
| `s`  | 24px   | body-s (12px) | 12px      | 8px     | Secondary information   |
| `m`  | 28px   | body-m (14px) | 16px      | 8px     | Standard use (default)  |
| `l`  | 32px   | body-l (16px) | 20px      | 8px     | Prominent placement     |

## Accessibility Features

- **Semantic Colors**: Color themes follow WCAG contrast guidelines
- **Text Alternative**: Text content provides meaning independent of color
- **Focus States**: Inherits focus behavior when used within interactive elements
- **Screen Reader Support**: Content is properly exposed to assistive technologies
- **High Contrast**: Both subtle and intense modes meet accessibility standards

## Best Practices

### Design Guidelines

- Use consistent appearance themes for similar content types
- Reserve intense styling for critical information or primary actions
- Combine badges with icons for enhanced communication
- Maintain appropriate size hierarchy based on content importance
- Use subtle styling for secondary or background information

### Content Guidelines

- Keep text concise and meaningful (typically 1-3 words)
- Use familiar terminology that users understand
- Ensure badge content makes sense without surrounding context
- Consider internationalization for text content
- Use consistent capitalization patterns

### Layout Guidelines

- Provide adequate spacing around badges in dense layouts
- Align badges consistently with related content
- Group related badges with consistent sizing and spacing
- Consider badge placement in responsive layouts
- Use appropriate size for the content hierarchy level

### Performance Considerations

- Reuse common badge configurations to improve rendering performance
- Avoid excessive customStyles that could impact bundle size
- Use CSS classes instead of inline styles when possible
- Consider badge grouping patterns for large lists

## Integration Examples

### Data Table Status

```tsx
// In a data table cell
<Badge
  size="s"
  appearance={row.status === "active" ? "Success" : "Neutral"}
  text={row.status}
  subtle
/>
```

### Navigation Menu

```tsx
// In navigation items
<div className="flex items-center gap-2">
  <span>Messages</span>
  <Badge size="xs" appearance="Error" text="3" />
</div>
```

### Card Headers

```tsx
// In card components
<div className="flex justify-between items-center">
  <h3>Project Title</h3>
  <Badge appearance="Success" text="Active" subtle />
</div>
```

### Form Validation

```tsx
// Field validation feedback
<div className="space-y-1">
  <label>Email Address</label>
  <input type="email" />
  <Badge size="s" appearance="Error" text="Required field" />
</div>
```

### User Profile

```tsx
// User status indicator
<div className="flex items-center gap-3">
  <Avatar src="/user.jpg" />
  <div>
    <p>John Doe</p>
    <Badge size="xs" appearance="Success" text="Online" />
  </div>
</div>
```

## Technical Notes

- Badge uses Genesis spacing tokens (gd-\*) for consistent spacing
- Typography scales follow Genesis design system specifications
- Color values use Genesis color variables for theme compatibility
- Component supports forwardRef for advanced ref management
- Icon sizing automatically adapts to badge size for proper proportion
- Z-index management is handled automatically for proper layering
- Component is fully responsive across all device sizes
- Supports both controlled and uncontrolled usage patterns

## Migration Guide

When upgrading from older versions:

1. Update import statements to use `gends` package
2. Replace deprecated color names with new appearance values
3. Update custom styling props to use new customStyles structure
4. Replace size prop values with new standardized options
5. Update classNames structure to match new interface
6. Test icon integration with new automatic sizing system

## Troubleshooting

### Common Issues

- **Icon not displaying**: Ensure icon is a valid React element
- **Custom styles not applying**: Check customStyles object structure
- **Text overflow**: Use appropriate size for content length
- **Color contrast**: Verify appearance choice meets accessibility requirements
- **Spacing issues**: Use Genesis spacing tokens in surrounding layout
