# Button

Highly-configurable button component supporting multiple variants, appearances, sizes, icons, loading states, and accessibility—all in one composable component.

---

## 1. Quick start

```tsx
import { Button } from "gends";

function Example() {
  return (
    <Button onClick={() => alert('Clicked!')}>
      Click me
    </Button>
  );
}
```

---

## 2. Sizes

| size   | Height | Recommended type scale |
|--------|--------|-----------------------|
| `xs`   | 24 px  | `body-s`              |
| `s`    | 32 px  | `body-m`              |
| `m`    | 40 px  | `body-m`              |
| `l`    | 48 px  | `body-l`              |
| `xl`   | 56 px  | `body-xl`             |

```tsx
<Button size="xs">Extra Small</Button>
<Button size="s">Small</Button>
<Button size="m">Medium</Button>
<Button size="l">Large</Button>
<Button size="xl">Extra Large</Button>
```

---

## 3. Kinds & Appearances

### Kind

| kind        | Description                |
|-------------|---------------------------|
| `primary`   | Main action, filled       |
| `secondary` | Secondary action, subtle  |
| `tertiary`  | Minimal, text-like        |

### Appearance

| appearance   | Description                |
|--------------|---------------------------|
| `default`    | Standard                  |
| `positive`   | Success/confirm           |
| `negative`   | Error/destructive         |
| `warning`    | Warning                   |
| `contrast`   | High-contrast             |
| `ai`         | AI/assistant action       |

### All Kind + Appearance Combinations

| Kind       | Appearance    | Example Code |
|------------|--------------|--------------|
| primary    | default      | `<Button kind="primary" appearance="default">Primary</Button>` |
| primary    | positive     | `<Button kind="primary" appearance="positive">Primary Positive</Button>` |
| primary    | negative     | `<Button kind="primary" appearance="negative">Primary Negative</Button>` |
| primary    | warning      | `<Button kind="primary" appearance="warning">Primary Warning</Button>` |
| primary    | contrast     | `<Button kind="primary" appearance="contrast">Primary Contrast</Button>` |
| primary    | ai           | `<Button kind="primary" appearance="ai">Primary AI</Button>` |
| secondary  | default      | `<Button kind="secondary" appearance="default">Secondary</Button>` |
| secondary  | positive     | `<Button kind="secondary" appearance="positive">Secondary Positive</Button>` |
| secondary  | negative     | `<Button kind="secondary" appearance="negative">Secondary Negative</Button>` |
| secondary  | warning      | `<Button kind="secondary" appearance="warning">Secondary Warning</Button>` |
| secondary  | contrast     | `<Button kind="secondary" appearance="contrast">Secondary Contrast</Button>` |
| secondary  | ai           | `<Button kind="secondary" appearance="ai">Secondary AI</Button>` |
| tertiary   | default      | `<Button kind="tertiary" appearance="default">Tertiary</Button>` |
| tertiary   | positive     | `<Button kind="tertiary" appearance="positive">Tertiary Positive</Button>` |
| tertiary   | negative     | `<Button kind="tertiary" appearance="negative">Tertiary Negative</Button>` |
| tertiary   | warning      | `<Button kind="tertiary" appearance="warning">Tertiary Warning</Button>` |
| tertiary   | contrast     | `<Button kind="tertiary" appearance="contrast">Tertiary Contrast</Button>` |
| tertiary   | ai           | `<Button kind="tertiary" appearance="ai">Tertiary AI</Button>` |

---

## 4. States

| State      | Description                        |
|------------|------------------------------------|
| `default`  | Normal, interactive                |
| `hover`    | On mouse hover                     |
| `active`   | On click/press                     |
| `focus`    | Keyboard focus, shows ring         |
| `disabled` | Non-interactive, faded             |
| `loading`  | Shows spinner, disables actions    |

```tsx
<Button disabled>Disabled</Button>
<Button loading>Loading</Button>
```

---

## 5. Icons

Buttons can display icons before (prefix) or after (suffix) the label, or both.

| Prop         | Type         | Description                        |
|--------------|--------------|------------------------------------|
| `prefixIcon` | `ReactNode`  | Icon before the label              |
| `suffixIcon` | `ReactNode`  | Icon after the label               |

```tsx
<Button prefixIcon={<IcImport />}>Download</Button>
<Button suffixIcon={<IcImport />}>Download</Button>
<Button prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Download</Button>
```

### Icon + Size Combinations

```tsx
<Button size="xs" prefixIcon={<IcImport />}>XS</Button>
<Button size="s" suffixIcon={<IcImport />}>S</Button>
<Button size="m" prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>M</Button>
<Button size="l" prefixIcon={<IcImport />}>L</Button>
<Button size="xl" suffixIcon={<IcImport />}>XL</Button>
```

### Both Left and Right Icons

```tsx
<Button prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Download</Button>
```

---

## 6. Full width

Set `fullWidth` to make the button stretch to its container.

```tsx
<Button fullWidth>Full Width</Button>
<Button fullWidth prefixIcon={<IcImport />} loading>Full Width Loading</Button>
```

---

## 7. Accessibility

- All buttons are keyboard accessible by default.
- Use `aria-label` for icon-only buttons.
- Focus ring is visible for keyboard navigation.

```tsx
<Button aria-label="Download" prefixIcon={<IcImport />} />
```

---

## 8. Full prop reference

| Prop           | Type                                      | Default     | Description                                 |
|----------------|-------------------------------------------|-------------|---------------------------------------------|
| `children`     | `ReactNode`                               | –           | Button label                                |
| `onClick`      | `(e: MouseEvent) => void`                 | –           | Click handler                               |
| `size`         | `'xs' \| 's' \| 'm' \| 'l' \| 'xl'`        | `'m'`       | Button size                                 |
| `kind`         | `'primary' \| 'secondary' \| 'tertiary'`   | `'primary'` | Button kind                                 |
| `appearance`   | `'default' \| 'positive' \| 'negative' \| 'warning' \| 'contrast' \| 'ai'` | `'default'` | Visual appearance                           |
| `prefixIcon`   | `ReactNode`                               | –           | Icon before label                           |
| `suffixIcon`   | `ReactNode`                               | –           | Icon after label                            |
| `loading`      | `boolean`                                 | `false`     | Show loading spinner, disables button       |
| `disabled`     | `boolean`                                 | `false`     | Disable button                              |
| `fullWidth`    | `boolean`                                 | `false`     | Stretch to container width                  |
| `type`         | `'button' \| 'submit' \| 'reset'`         | `'button'`  | Button type                                 |
| `hideUnderline`| `boolean`                                 | `false`     | Hide underline (for link/tertiary)          |
| `className`    | `string`                                  | –           | Custom class for root element               |
| `iconClassName`| `string`                                  | –           | Custom class for icon(s)                    |
| `aria-label`   | `string`                                  | –           | Accessibility label (for icon-only)         |

---

## 9. Recipes

### Primary with left icon

```tsx
<Button prefixIcon={<IcImport />}>Import</Button>
```

### Secondary with right icon

```tsx
<Button kind="secondary" suffixIcon={<IcMoreHorizontal />}>More</Button>
```

### Tertiary, icon only

```tsx
<Button kind="tertiary" aria-label="More options" prefixIcon={<IcMoreHorizontal />} />
```

### Loading state

```tsx
<Button loading>Loading…</Button>
<Button kind="secondary" loading>Secondary Loading</Button>
<Button kind="tertiary" appearance="warning" loading>Warning Tertiary Loading</Button>
```

### Full width, large, destructive

```tsx
<Button fullWidth size="l" appearance="negative">Delete</Button>
<Button fullWidth size="xl" kind="secondary" appearance="contrast">Contrast Secondary XL</Button>
```

### Both left and right icons, loading, and fullWidth

```tsx
<Button fullWidth loading prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Download All</Button>
```

```tsx
// Basic usage
<Button>Default</Button>
<Button onClick={() => alert('Clicked!')}>With Click</Button>

// Sizes
<Button size="xs">XS</Button>
<Button size="s">Small</Button>
<Button size="m">Medium</Button>
<Button size="l">Large</Button>
<Button size="xl">XL</Button>

// Kinds
<Button kind="primary">Primary</Button>
<Button kind="secondary">Secondary</Button>
<Button kind="tertiary">Tertiary</Button>

// Appearances
<Button appearance="default">Default</Button>
<Button appearance="positive">Positive</Button>
<Button appearance="negative">Negative</Button>
<Button appearance="warning">Warning</Button>
<Button appearance="contrast">Contrast</Button>
<Button appearance="ai">AI</Button>

// Kind + Appearance combinations
<Button kind="primary" appearance="positive">Primary Positive</Button>
<Button kind="primary" appearance="negative">Primary Negative</Button>
<Button kind="primary" appearance="warning">Primary Warning</Button>
<Button kind="primary" appearance="contrast">Primary Contrast</Button>
<Button kind="primary" appearance="ai">Primary AI</Button>
<Button kind="secondary" appearance="positive">Secondary Positive</Button>
<Button kind="secondary" appearance="negative">Secondary Negative</Button>
<Button kind="secondary" appearance="warning">Secondary Warning</Button>
<Button kind="secondary" appearance="contrast">Secondary Contrast</Button>
<Button kind="secondary" appearance="ai">Secondary AI</Button>
<Button kind="tertiary" appearance="positive">Tertiary Positive</Button>
<Button kind="tertiary" appearance="negative">Tertiary Negative</Button>
<Button kind="tertiary" appearance="warning">Tertiary Warning</Button>
<Button kind="tertiary" appearance="contrast">Tertiary Contrast</Button>
<Button kind="tertiary" appearance="ai">Tertiary AI</Button>

// Disabled
<Button disabled>Disabled</Button>
<Button kind="secondary" disabled>Secondary Disabled</Button>
<Button kind="tertiary" appearance="warning" disabled>Tertiary Warning Disabled</Button>

// Loading
<Button loading>Loading</Button>
<Button kind="secondary" loading>Secondary Loading</Button>
<Button kind="tertiary" appearance="negative" loading>Tertiary Negative Loading</Button>

// Full width
<Button fullWidth>Full Width</Button>
<Button fullWidth kind="secondary">Full Width Secondary</Button>
<Button fullWidth kind="tertiary" appearance="ai">Full Width Tertiary AI</Button>

// Prefix (left) icon
<Button prefixIcon={<IcImport />}>Left Icon</Button>
<Button size="l" prefixIcon={<IcImport />}>Large Left Icon</Button>
<Button kind="secondary" prefixIcon={<IcImport />}>Secondary Left Icon</Button>

// Suffix (right) icon
<Button suffixIcon={<IcMoreHorizontal />}>Right Icon</Button>
<Button size="xl" suffixIcon={<IcMoreHorizontal />}>XL Right Icon</Button>
<Button kind="tertiary" suffixIcon={<IcMoreHorizontal />}>Tertiary Right Icon</Button>

// Both prefix and suffix icons
<Button prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Both Icons</Button>
<Button size="s" prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Small Both Icons</Button>
<Button kind="secondary" appearance="contrast" prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Secondary Contrast Both Icons</Button>

// Icon only (aria-label for accessibility)
<Button prefixIcon={<IcImport />} aria-label="Import" />
<Button suffixIcon={<IcMoreHorizontal />} aria-label="More" />
<Button prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />} aria-label="Import and More" />

// Loading with icons
<Button loading prefixIcon={<IcImport />}>Loading Left Icon</Button>
<Button loading suffixIcon={<IcMoreHorizontal />}>Loading Right Icon</Button>
<Button loading prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Loading Both Icons</Button>

// Full width with icons and loading
<Button fullWidth loading prefixIcon={<IcImport />}>Full Width Loading Left Icon</Button>
<Button fullWidth loading suffixIcon={<IcMoreHorizontal />}>Full Width Loading Right Icon</Button>
<Button fullWidth loading prefixIcon={<IcImport />} suffixIcon={<IcMoreHorizontal />}>Full Width Loading Both Icons</Button>

// All props (example)
<Button
  kind="tertiary"
  appearance="warning"
  size="xl"
  prefixIcon={<IcImport />}
  suffixIcon={<IcMoreHorizontal />}
  loading
  disabled
  fullWidth
  className="custom-class"
  iconClassName="icon-class"
  aria-label="All props"
>
  All Props
</Button>