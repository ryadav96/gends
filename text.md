# Text

A flexible typography component that implements a consistent type scale across the application, supporting various text styles from display text to body copy—with semantic HTML rendering and customizable variants.

## Key Features

- **Comprehensive Style Variants**: 22 predefined desktop-optimized styles for displays, headings, and body text
- **Semantic HTML Support**: Override default elements using the `as` prop for proper HTML semantics
- **Style Customization**: Extend or override styles using Tailwind CSS classes
- **Responsive Ready**: Designed for desktop-first experiences (add mobile variants when needed)
- **Accessibility Friendly**: Encourages proper heading hierarchy and text contrast

## 1. Quick start

```tsx
import { Text } from "gends";

function Example() {
  return (
    <>
      <Text variant="desktop-display-l">Large Display Text</Text>
      <Text variant="desktop-heading-m">Medium Heading</Text>
      <Text variant="desktop-body-m">Regular body text</Text>
    </>
  );
}
```

The `Text` component automatically maps variants to appropriate semantic HTML elements (h1-h5, p, span).

---

## 2. Text Categories

### Display Text

| Variant               | HTML Element | Use Case           |
| --------------------- | ------------ | ------------------ |
| `desktop-display-2xl` | h1           | Hero sections      |
| `desktop-display-xl`  | h1           | Main headlines     |
| `desktop-display-l`   | h1           | Large headers      |
| `desktop-display-m`   | h1           | Medium headers     |
| `desktop-display-s`   | h2           | Section headers    |
| `desktop-display-xs`  | h2           | Subsection headers |
| `desktop-display-2xs` | h2           | Minor headers      |

### Headings

| Variant               | HTML Element | Use Case       |
| --------------------- | ------------ | -------------- |
| `desktop-heading-2xl` | h2           | Major sections |
| `desktop-heading-xl`  | h3           | Section titles |
| `desktop-heading-l`   | h4           | Subsections    |
| `desktop-heading-m`   | h5           | Minor sections |

### Body Text

| Variant                      | HTML Element | Use Case             |
| ---------------------------- | ------------ | -------------------- |
| `desktop-body-2xl-prominent` | p            | Featured content     |
| `desktop-body-xl-prominent`  | p            | Important paragraphs |
| `desktop-body-xl`            | p            | Large body text      |
| `desktop-body-l-prominent`   | p            | Emphasized content   |
| `desktop-body-l`             | p            | Standard paragraphs  |
| `desktop-body-m-prominent`   | p            | Medium emphasized    |
| `desktop-body-m`             | p            | Default body text    |
| `desktop-body-s-prominent`   | p            | Small emphasized     |
| `desktop-body-s`             | p            | Small text           |
| `desktop-body-xs-prominent`  | span         | Tiny emphasized      |
| `desktop-body-xs`            | span         | Tiny text            |

---

## 3. Semantic HTML

The component automatically maps variants to semantic HTML elements:

```tsx
// Renders as <h1>
<Text variant="desktop-display-xl">Title</Text>

// Renders as <p>
<Text variant="desktop-body-m">Paragraph</Text>

// Renders as <span>
<Text variant="desktop-body-xs">Small text</Text>
```

You can override the default element using the `as` prop:

```tsx
// Force rendering as a different element
<Text variant="desktop-body-m" as="div">
  Div element with body text styling
</Text>
```

---

## 4. Customization

### Custom Classes

```tsx
<Text variant="desktop-body-m" className="text-blue-500 hover:text-blue-600">
  Custom styled text
</Text>
```

### HTML Attributes

```tsx
<Text
  variant="desktop-body-m"
  id="main-content"
  aria-label="Main content"
  onClick={() => console.log("clicked")}
>
  Interactive text
</Text>
```

---

## 5. Full prop reference

| Prop        | Type                          | Default            | Description            |
| ----------- | ----------------------------- | ------------------ | ---------------------- |
| `variant`   | `TextVariant`                 | `'desktop-body-m'` | Typography variant     |
| `as`        | `keyof JSX.IntrinsicElements` | Based on variant   | HTML element override  |
| `className` | `string`                      | -                  | Additional CSS classes |
| `children`  | `ReactNode`                   | -                  | Text content           |

Plus all standard HTML text element attributes.

---

## 6. Recipes

### Article Layout

```tsx
function Article() {
  return (
    <article>
      <Text variant="desktop-display-xl">Article Title</Text>

      <Text variant="desktop-heading-l">Section Heading</Text>

      <Text variant="desktop-body-l">Introduction paragraph with larger text...</Text>

      <Text variant="desktop-body-m">Regular content paragraph...</Text>

      <Text variant="desktop-body-s">Small print information...</Text>
    </article>
  );
}
```

### Card Component

```tsx
function Card() {
  return (
    <div className="card">
      <Text variant="desktop-heading-m">Card Title</Text>

      <Text variant="desktop-body-m-prominent">Featured content or summary...</Text>

      <Text variant="desktop-body-s">Additional details...</Text>
    </div>
  );
}
```

### Form Labels

```tsx
function FormField() {
  return (
    <div className="field">
      <Text variant="desktop-body-s-prominent" as="label">
        Field Label
      </Text>

      <input type="text" />

      <Text variant="desktop-body-xs" className="text-gray-500">
        Helper text
      </Text>
    </div>
  );
}
```

---

## 7. Accessibility considerations

- Uses semantic HTML elements by default
- Maintains proper heading hierarchy
- Supports ARIA attributes
- Preserves text scaling
- Screen reader friendly

```tsx
// Proper heading hierarchy
<Text variant="desktop-display-xl">Page Title</Text>
<Text variant="desktop-heading-l">Section Title</Text>
<Text variant="desktop-heading-m">Subsection Title</Text>
```

---

## 8. Design patterns

### Typography Hierarchy

- Use appropriate variants for content hierarchy
- Maintain consistent spacing between text elements
- Follow heading levels sequentially
- Use prominent variants for emphasis

### Content Organization

- Use display variants for main titles
- Apply heading variants for sections
- Utilize body variants for content
- Implement consistent spacing

### Responsive Patterns

- Consider readability across devices
- Adjust text sizes responsively
- Maintain proper contrast
- Ensure proper line lengths

---
