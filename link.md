# Link Component

## Overview

The Link component is a versatile and accessible navigation element built with Genesis Design System tokens. It provides a comprehensive set of variants for different use cases, including multiple sizes, subtle and prominent styles, and disabled states. The component is designed for both inline text links and standalone navigation elements, with complete accessibility support and extensive customization options.

## Component API

### Link Props

| Prop      | Type                   | Default  | Description                   |
| --------- | ---------------------- | -------- | ----------------------------- |
| subtle    | `boolean`              | `true`   | Whether to use subtle styling |
| label     | `string`               | `"link"` | Text content of the link      |
| className | `string`               | `""`     | Additional CSS classes        |
| disabled  | `boolean`              | `false`  | Whether the link is disabled  |
| link      | `string`               | `""`     | URL or path to navigate to    |
| size      | `"sm" \| "md" \| "lg"` | `"md"`   | Size variant of the link      |

### Import Statement

```typescript
import { Link } from "gends";
```

## Basic Usage

### Default Link

```tsx
<Link link="https://example.com" label="Visit Example" />
```

### Size Variants

```tsx
<div className="flex flex-col gap-4">
  <Link size="sm" link="https://example.com" label="Small Link" />
  <Link size="md" link="https://example.com" label="Medium Link" />
  <Link size="lg" link="https://example.com" label="Large Link" />
</div>
```

### Style Variants

```tsx
<div className="flex flex-col gap-4">
  <Link subtle link="https://example.com" label="Subtle Link" />
  <Link subtle={false} link="https://example.com" label="Prominent Link" />
</div>
```

## Advanced Features

### Disabled State

```tsx
<div className="flex flex-col gap-4">
  <Link disabled link="https://example.com" label="Disabled Link" />
  <Link disabled subtle={false} link="https://example.com" label="Disabled Prominent Link" />
</div>
```

### Custom Styling

```tsx
<Link className="custom-link-class" link="https://example.com" label="Custom Styled Link" />
```

## Real-World Usage Examples

### Navigation Menu

```tsx
const NavigationMenu = () => {
  return (
    <nav className="flex flex-col gap-2">
      <Link size="md" link="/dashboard" label="Dashboard" subtle={false} />
      <Link size="md" link="/profile" label="Profile" />
      <Link size="md" link="/settings" label="Settings" />
    </nav>
  );
};
```

### Footer Links

```tsx
const FooterLinks = () => {
  return (
    <footer className="flex flex-wrap gap-4">
      <Link size="sm" link="/privacy" label="Privacy Policy" subtle />
      <Link size="sm" link="/terms" label="Terms of Service" subtle />
      <Link size="sm" link="/contact" label="Contact Us" subtle />
    </footer>
  );
};
```

### Interactive Content

```tsx
const InteractiveContent = () => {
  const [isEnabled, setIsEnabled] = React.useState(true);

  return (
    <div className="space-y-4">
      <Link size="lg" link="https://example.com" label="Interactive Link" disabled={!isEnabled} />
      <button onClick={() => setIsEnabled(!isEnabled)}>Toggle Link</button>
    </div>
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab Navigation**: Focus management through interactive elements
- **Enter/Space**: Activate focused link
- **Focus Management**: Clear focus indicators

### Screen Reader Support

- **ARIA Attributes**: Proper roles and states
- **Link Labels**: Descriptive text for screen readers
- **State Announcements**: Clear state changes

### Visual Accessibility

- **Focus Indicators**: Clear focus states
- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Size Variants**: Multiple size options for different needs

## Design System Integration

### Genesis Design Tokens

**Colors:**

- Primary: `var(--gd-primary-50)`, `var(--gd-primary-60)`
- Text: `var(--gd-text-subdued-1)`, `var(--gd-text-subdued-2)`

**Typography:**

- Small: `text-en-desktop-body-s-prominent`
- Medium: `text-en-desktop-body-m-prominent`
- Large: `text-en-desktop-body-l-prominent`

**Spacing:**

- `gd-2`: Focus outline
- `gd-4`: Underline offset

**States:**

- Hover: `hover:text-color-primary-50`
- Active: `active:text-color-primary-60`
- Visited: `visited:text-color-text-subdued-1`
- Focus: `focus-visible:outline-gd-2 focus-visible:outline-color-primary-60`

## Best Practices

### Performance

- Use appropriate size variants
- Optimize link rendering
- Handle state changes efficiently

### User Experience

- Choose appropriate size for context
- Use consistent styling
- Provide clear visual feedback

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider mobile responsiveness

## Troubleshooting

### Common Issues

**Link Styling:**

- Verify subtle prop usage
- Check custom class names
- Ensure proper color contrast

**State Management:**

- Handle disabled state properly
- Manage focus states
- Control visited states

**Styling Conflicts:**

- Check custom class names
- Verify style overrides
- Review typography tokens

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Link component provides a flexible and accessible way to implement navigation elements. Choose the appropriate configuration based on your specific use case and requirements.
