# Scrollbar Component

## Overview

The Scrollbar component is a customizable and accessible scrollable area that provides a consistent scrolling experience across different browsers and platforms. Built with Genesis Design System tokens and Radix UI primitives, it offers multiple size variants, orientation options, and extensive customization capabilities. The component is designed to work seamlessly within the MCP context while maintaining full accessibility support.

## Component API

### Scrollbar Props

| Prop        | Type                                   | Default      | Description                          |
| ----------- | -------------------------------------- | ------------ | ------------------------------------ |
| size        | `"small" \| "large"`                   | `"small"`    | Size variant of the scrollbar        |
| orientation | `"vertical" \| "horizontal" \| "both"` | `"vertical"` | Scrollbar orientation                |
| height      | `string`                               | `undefined`  | Custom height for scrollbar          |
| width       | `string`                               | `undefined`  | Custom width for scrollbar           |
| maxHeight   | `string`                               | `"100%"`     | Maximum height of the viewport       |
| maxWidth    | `string`                               | `"100%"`     | Maximum width of the viewport        |
| className   | `string`                               | `undefined`  | Custom class for the root element    |
| classNames  | `ScrollbarClassNames`                  | `undefined`  | Custom classes for internal elements |
| id          | `string`                               | `""`         | Unique identifier for the scrollbar  |
| style       | `CSSProperties`                        | `{}`         | Custom styles for the root element   |

### ScrollbarClassNames Interface

```typescript
interface ScrollbarClassNames {
  viewport?: string;
  container?: string;
  scrollbar?: string;
}
```

### Import Statement

```typescript
import { Scrollbar } from "gends";
```

## Basic Usage

### Default Scrollbar

```tsx
import { Scrollbar } from "gends";

function MyComponent() {
  return (
    <Scrollbar>
      <div className="p-4">
        <h3>Scrollable Content</h3>
        <p>Your content goes here</p>
      </div>
    </Scrollbar>
  );
}
```

## Variants

### Size Variants

#### Small (default)

```tsx
<Scrollbar size="small">
  <div className="h-[200px] p-4">
    <h3>Small Scrollbar</h3>
    <p>Content with small scrollbar</p>
  </div>
</Scrollbar>
```

#### Large

```tsx
<Scrollbar size="large">
  <div className="h-[200px] p-4">
    <h3>Large Scrollbar</h3>
    <p>Content with large scrollbar</p>
  </div>
</Scrollbar>
```

### Orientation Variants

#### Vertical (default)

```tsx
<Scrollbar orientation="vertical">
  <div className="h-[200px] p-4">
    <h3>Vertical Scrollbar</h3>
    <p>Content with vertical scrolling</p>
  </div>
</Scrollbar>
```

#### Horizontal

```tsx
<Scrollbar orientation="horizontal">
  <div className="w-[200px] p-4">
    <h3>Horizontal Scrollbar</h3>
    <p>Content with horizontal scrolling</p>
  </div>
</Scrollbar>
```

#### Both

```tsx
<Scrollbar orientation="both">
  <div className="h-[200px] w-[200px] p-4">
    <h3>Both Scrollbars</h3>
    <p>Content with both vertical and horizontal scrolling</p>
  </div>
</Scrollbar>
```

## Advanced Features

### Custom Dimensions

```tsx
<Scrollbar height="300px" width="400px" maxHeight="500px" maxWidth="600px">
  <div className="p-4">
    <h3>Custom Dimensions</h3>
    <p>Content with custom scrollbar dimensions</p>
  </div>
</Scrollbar>
```

### Custom Styling

```tsx
<Scrollbar
  className="border border-gray-200 rounded-lg"
  classNames={{
    viewport: "bg-gray-50",
    container: "bg-gray-100",
    scrollbar: "bg-blue-500",
  }}
>
  <div className="p-4">
    <h3>Custom Styling</h3>
    <p>Content with custom scrollbar styling</p>
  </div>
</Scrollbar>
```

## Real-World Usage Examples

### List with Tags

```tsx
function TagList() {
  const tags = Array.from({ length: 50 }).map((_, i) => `Tag ${i + 1}`);

  return (
    <Scrollbar size="small">
      <div className="p-4">
        <h4 className="mb-4 text-sm font-medium">Tags</h4>
        {tags.map(tag => (
          <div key={tag} className="text-sm mb-2">
            {tag}
          </div>
        ))}
      </div>
    </Scrollbar>
  );
}
```

### Image Gallery

```tsx
function ImageGallery() {
  const images = Array.from({ length: 10 }).map((_, i) => ({
    src: `https://example.com/image${i + 1}.jpg`,
    alt: `Image ${i + 1}`,
  }));

  return (
    <Scrollbar orientation="horizontal" size="large">
      <div className="flex space-x-4 p-4">
        {images.map(image => (
          <img
            key={image.src}
            src={image.src}
            alt={image.alt}
            className="w-32 h-32 object-cover rounded"
          />
        ))}
      </div>
    </Scrollbar>
  );
}
```

### Grid Layout

```tsx
function GridLayout() {
  const items = Array.from({ length: 30 }).map((_, i) => ({
    id: i + 1,
    title: `Item ${i + 1}`,
  }));

  return (
    <Scrollbar orientation="both" size="large">
      <div className="grid grid-cols-4 gap-4 p-4">
        {items.map(item => (
          <div key={item.id} className="p-4 bg-white rounded shadow">
            {item.title}
          </div>
        ))}
      </div>
    </Scrollbar>
  );
}
```

## Accessibility Features

### Keyboard Navigation

- **Focus Management**: Proper focus handling within scrollable content
- **ARIA Attributes**: Appropriate roles and labels
- **Keyboard Shortcuts**: Arrow keys for navigation
- **Focus Indicators**: Clear visual feedback

### Screen Reader Support

- **ARIA Labels**: Clear identification of scrollable area
- **Live Regions**: Dynamic content updates announced
- **Role Descriptions**: Proper semantic structure

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Focus Indicators**: Clear visual feedback
- **Motion**: Respects reduced motion preferences

## Design System Integration

### Genesis Design Tokens

**Sizing:**

- Small Vertical: `w-gd-4`
- Small Horizontal: `h-gd-4`
- Large Vertical: `w-gd-8`
- Large Horizontal: `h-gd-8`

**Colors:**

- Scrollbar: `bg-color-neutral-grey-100`
- Corner: `bg-color-neutral-grey-50`
- Opacity: `opacity-15` (default), `opacity-30` (hover/active)

**Spacing:**

- Container Padding: `p-gd-16`
- Gap Between Elements: `gap-gd-4`

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

**Scrolling:**

- Check content dimensions
- Verify scrollbar visibility
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

Remember: The Scrollbar component provides a flexible and accessible way to handle scrollable content. Choose the appropriate configuration based on your specific use case and requirements.
