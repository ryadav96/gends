# Text

A flexible typography component that provides consistent desktop-optimized text styles while maintaining accessibility and customization capabilities.

## Key Features
- **Comprehensive Style Variants**: 22 predefined desktop-optimized styles for displays, headings, and body text
- **Semantic HTML Support**: Override default elements using the `as` prop for proper HTML semantics
- **Style Customization**: Extend or override styles using Tailwind CSS classes
- **Responsive Ready**: Designed for desktop-first experiences (add mobile variants when needed)
- **Accessibility Friendly**: Encourages proper heading hierarchy and text contrast

## 1. Quick start

```tsx
import { Text } from 'gends';

// Default body text
<Text>Regular paragraph text</Text>

// Semantic heading with variant
<Text variant="desktop-heading-xl" as="h1">Main page heading</Text>

// Prominent body text with custom color
<Text variant="desktop-body-l-prominent" className="text-brand-primary">
  Important notice text
</Text>
```

## 2. Display Variants

```tsx
// Display variants (largest to smallest)
<Text variant="desktop-display-2xl" as="h1">Display 2XL (64px)</Text>
<Text variant="desktop-display-xl" as="h1">Display XL (56px)</Text>
<Text variant="desktop-display-l" as="h2">Display L (48px)</Text>
<Text variant="desktop-display-m" as="h3">Display M (40px)</Text>
<Text variant="desktop-display-s" as="h4">Display S (32px)</Text>
<Text variant="desktop-display-xs" as="h5">Display XS (24px)</Text>
<Text variant="desktop-display-2xs" as="h6">Display 2XS (20px)</Text>
```

## 3. Heading Variants

```tsx
// Heading variants (largest to smallest)
<Text variant="desktop-heading-2xl" as="h1">Heading 2XL (56px)</Text>
<Text variant="desktop-heading-xl" as="h2">Heading XL (48px)</Text>
<Text variant="desktop-heading-l" as="h3">Heading L (40px)</Text>
<Text variant="desktop-heading-m" as="h4">Heading M (32px)</Text>
```

## 4. Body Text Variants

```tsx
// Body text variants (largest to smallest)
<Text variant="desktop-body-2xl-prominent">Body 2XL Prominent</Text>
<Text variant="desktop-body-xl-prominent">Body XL Prominent</Text>
<Text variant="desktop-body-xl">Body XL</Text>
<Text variant="desktop-body-l-prominent">Body L Prominent</Text>
<Text variant="desktop-body-l">Body L</Text>
<Text variant="desktop-body-m-prominent">Body M Prominent</Text>
<Text variant="desktop-body-m">Body M (default)</Text>
<Text variant="desktop-body-s-prominent">Body S Prominent</Text>
<Text variant="desktop-body-s">Body S</Text>
<Text variant="desktop-body-xs-prominent">Body XS Prominent</Text>
<Text variant="desktop-body-xs">Body XS</Text>
```

## 5. Semantic HTML Elements

```tsx
// Different HTML elements for semantic markup
<Text as="p">Paragraph text (default)</Text>
<Text as="span">Span text</Text>
<Text as="h1">Heading 1</Text>
<Text as="h2">Heading 2</Text>
<Text as="h3">Heading 3</Text>
<Text as="h4">Heading 4</Text>
<Text as="h5">Heading 5</Text>
<Text as="h6">Heading 6</Text>
<Text as="div">Div text</Text>
<Text as="label">Label text</Text>
```

## 6. Customization

```tsx
// Custom styling with Tailwind classes
<Text className="text-brand-primary">Custom color</Text>
<Text className="font-bold">Bold text</Text>
<Text className="italic">Italic text</Text>
<Text className="underline">Underlined text</Text>
<Text className="text-center">Centered text</Text>
<Text className="truncate">Truncated text that's too long...</Text>
```

## 7. Full prop reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `variant` | `TextVariant` | `'desktop-body-m'` | Predefined text style variant |
| `as` | `keyof JSX.IntrinsicElements` | `'p'` | HTML element to render |
| `className` | `string` | – | Additional Tailwind classes |
| `children` | `React.ReactNode` | – | Text content |

### TextVariant type

```tsx
type TextVariant =
  | 'desktop-display-2xl'
  | 'desktop-display-xl'
  | 'desktop-display-l'
  | 'desktop-display-m'
  | 'desktop-display-s'
  | 'desktop-display-xs'
  | 'desktop-display-2xs'
  | 'desktop-heading-2xl'
  | 'desktop-heading-xl'
  | 'desktop-heading-l'
  | 'desktop-heading-m'
  | 'desktop-body-2xl-prominent'
  | 'desktop-body-xl-prominent'
  | 'desktop-body-xl'
  | 'desktop-body-l-prominent'
  | 'desktop-body-l'
  | 'desktop-body-m-prominent'
  | 'desktop-body-m'
  | 'desktop-body-s-prominent'
  | 'desktop-body-s'
  | 'desktop-body-xs-prominent'
  | 'desktop-body-xs';
```

## 8. Best Practices

1. **Maintain Heading Hierarchy**
   ```tsx
   <Text variant="desktop-heading-xl" as="h1">Page Title</Text>
   <Text variant="desktop-heading-l" as="h2">Section Title</Text>
   <Text variant="desktop-heading-m" as="h3">Subsection Title</Text>
   ```

2. **Use Semantic Elements**
   ```tsx
   <Text as="label" variant="desktop-body-s">Form Label</Text>
   <Text as="p" variant="desktop-body-m">Paragraph</Text>
   ```

3. **Prominent Variants for Emphasis**
   ```tsx
   <Text variant="desktop-body-l">Regular text</Text>
   <Text variant="desktop-body-l-prominent">Important text</Text>
   ```
