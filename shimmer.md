# Shimmer Component

## Overview

The Shimmer component is a versatile loading placeholder that provides visual feedback during content loading states. Built with Genesis Design System tokens, it offers a smooth animation effect and extensive customization capabilities for creating skeleton loading states across various UI elements. The component is designed to work seamlessly within the MCP context while maintaining full accessibility support.

## Component API

### Shimmer Props

| Prop            | Type            | Default     | Description                                      |
| --------------- | --------------- | ----------- | ------------------------------------------------ |
| className       | `string`        | `""`        | Custom class for the shimmer element             |
| backgroundColor | `string`        | `"#e0e0e0"` | Background color of the shimmer                  |
| width           | `string`        | `"100%"`    | Width of the shimmer element                     |
| height          | `string`        | `"1rem"`    | Height of the shimmer element                    |
| borderRadius    | `string`        | `"4px"`     | Border radius of the shimmer element             |
| style           | `CSSProperties` | `{}`        | Additional inline styles for the shimmer element |

### Import Statement

```typescript
import { Shimmer } from "gends";
```

## Basic Usage

### Default Shimmer

```tsx
import { Shimmer } from "gends";

function MyComponent() {
  return <Shimmer width="100px" height="20px" backgroundColor="#e0e0e0" borderRadius="4px" />;
}
```

## Variants

### Size Variants

#### Custom Size

```tsx
<Shimmer width="200px" height="40px" backgroundColor="#d1d1d1" borderRadius="8px" />
```

#### Dark Mode

```tsx
<Shimmer width="150px" height="30px" backgroundColor="#444" borderRadius="6px" />
```

#### Rounded

```tsx
<Shimmer width="100px" height="100px" backgroundColor="#e0e0e0" borderRadius="50%" />
```

## Real-World Usage Examples

### Avatar with Text

```tsx
function AvatarWithText() {
  return (
    <div style={{ display: "flex", alignItems: "center", gap: "10px" }}>
      <Shimmer width="50px" height="50px" borderRadius="50%" />
      <div>
        <Shimmer width="120px" height="16px" borderRadius="4px" />
        <Shimmer width="80px" height="12px" borderRadius="4px" style={{ marginTop: "4px" }} />
      </div>
    </div>
  );
}
```

### Table Skeleton

```tsx
function TableSkeleton() {
  return (
    <div style={{ width: "100%", maxWidth: "90vw" }}>
      <Shimmer width="100%" height="30px" borderRadius="4px" />
      {[...Array(8)].map((_, index) => (
        <div key={index} style={{ display: "flex", gap: "10px", marginTop: "10px" }}>
          <Shimmer width="20%" height="20px" borderRadius="4px" />
          <Shimmer width="20%" height="20px" borderRadius="4px" />
          <Shimmer width="10%" height="20px" borderRadius="4px" />
          <Shimmer width="40%" height="20px" borderRadius="4px" />
          <Shimmer width="10%" height="20px" borderRadius="4px" />
        </div>
      ))}
    </div>
  );
}
```

### Card Layout

```tsx
function CardSkeleton() {
  return (
    <div style={{ width: "300px", padding: "16px", border: "1px solid #ddd", borderRadius: "8px" }}>
      <Shimmer width="100%" height="180px" borderRadius="8px" />
      <Shimmer width="70%" height="20px" borderRadius="4px" style={{ marginTop: "10px" }} />
      <Shimmer width="50%" height="16px" borderRadius="4px" style={{ marginTop: "6px" }} />
    </div>
  );
}
```

### Form Elements

```tsx
function FormSkeleton() {
  return (
    <div style={{ display: "flex", flexDirection: "column", gap: "10px" }}>
      <Shimmer width="100%" height="40px" borderRadius="4px" />
      <div style={{ display: "flex", gap: "5px" }}>
        {[...Array(6)].map((_, i) => (
          <Shimmer key={i} width="40px" height="40px" borderRadius="4px" />
        ))}
      </div>
      <Shimmer width="100%" height="80px" borderRadius="4px" />
    </div>
  );
}
```

### Calendar View

```tsx
function CalendarSkeleton() {
  return (
    <div style={{ width: "350px", border: "1px solid #ddd", borderRadius: "8px", padding: "10px" }}>
      <div style={{ display: "grid", gridTemplateColumns: "repeat(7, 1fr)", gap: "4px" }}>
        {[...Array(42)].map((_, i) => (
          <Shimmer key={i} width="100%" height="40px" borderRadius="4px" />
        ))}
      </div>
    </div>
  );
}
```

## Advanced Usage Examples

### File Viewer Skeleton

```tsx
function FileViewerSkeleton() {
  return (
    <div
      style={{
        display: "flex",
        width: "100%",
        height: "500px",
        border: "1px solid #ddd",
        borderRadius: "8px",
        overflow: "hidden",
      }}
    >
      <div
        style={{
          width: "80px",
          padding: "8px",
          overflowY: "auto",
          borderRight: "1px solid #ddd",
          display: "flex",
          flexDirection: "column",
          gap: "10px",
        }}
      >
        {[...Array(8)].map((_, i) => (
          <Shimmer key={i} width="100%" height="100px" borderRadius="4px" />
        ))}
      </div>
      <div
        style={{
          flex: 1,
          display: "flex",
          flexDirection: "column",
          alignItems: "center",
          justifyContent: "center",
          padding: "16px",
        }}
      >
        <Shimmer width="90%" height="80%" borderRadius="4px" />
      </div>
    </div>
  );
}
```

### Navigation Elements

```tsx
function NavigationSkeleton() {
  return (
    <div style={{ display: "flex", flexDirection: "column", gap: "10px" }}>
      <Shimmer width="100%" height="40px" borderRadius="4px" />
      <div style={{ display: "flex", gap: "10px" }}>
        {[...Array(5)].map((_, i) => (
          <Shimmer key={i} width="100px" height="30px" borderRadius="4px" />
        ))}
      </div>
    </div>
  );
}
```

## Accessibility Features

### Screen Reader Support

- **ARIA Hidden**: The shimmer is marked as `aria-hidden="true"` to prevent screen readers from announcing it
- **Loading States**: Properly indicates loading state to assistive technologies
- **Semantic Structure**: Maintains proper document structure during loading

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Motion**: Respects reduced motion preferences
- **Focus Management**: Does not interfere with keyboard navigation

## Design System Integration

### Genesis Design Tokens

**Colors:**

- Default Background: `#e0e0e0`
- Dark Mode: `#444`
- Custom Colors: Any valid CSS color value

**Sizing:**

- Default Height: `1rem`
- Default Width: `100%`
- Custom Dimensions: Any valid CSS size value

**Border Radius:**

- Default: `4px`
- Rounded: `50%`
- Custom: Any valid CSS border-radius value

## Best Practices

### Performance

- Use appropriate sizes for different viewports
- Avoid excessive shimmer elements
- Consider lazy loading for complex skeletons

### User Experience

- Match shimmer dimensions to actual content
- Use consistent styling across related elements
- Provide smooth transitions between states

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle errors appropriately

## Troubleshooting

### Common Issues

**Styling:**

- Check custom styles
- Verify design tokens
- Review responsive behavior

**Layout:**

- Verify dimensions
- Check container constraints
- Review flex/grid layouts

**Accessibility:**

- Verify ARIA attributes
- Test screen reader behavior
- Check color contrast

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Shimmer component provides a flexible and accessible way to indicate loading states. Choose the appropriate configuration based on your specific use case and requirements.
