# Link

A flexible link component that provides consistent styling, hover states, and accessibility features for navigation and external links.

---

## 1. Quick start

```tsx
import { Link } from "gends";

function Example() {
  return <Link label="Click here" link="https://example.com" size="md" subtle={true} />;
}
```

---

## 2. Sizes

| size | Font size | Font weight | Recommended use  |
| ---- | --------- | ----------- | ---------------- |
| `sm` | 14px      | 500         | Small text links |
| `md` | 16px      | 500         | Standard usage   |
| `lg` | 18px      | 500         | Prominent links  |

```tsx
<Link label="Small link" size="sm" link="#" />
<Link label="Medium link" size="md" link="#" />
<Link label="Large link" size="lg" link="#" />
```

---

## 3. Link styles

The component supports two distinct visual styles:

| style    | Description                      | Use case          |
| -------- | -------------------------------- | ----------------- |
| `subtle` | Subdued text color, no underline | Inline text links |
| `bold`   | Primary color with underline     | Standalone links  |

```tsx
// Subtle link (default)
<Link label="Subtle link" subtle={true} link="#" />

// Bold/prominent link
<Link label="Prominent link" subtle={false} link="#" />
```

---

## 4. States

```tsx
// Normal link
<Link label="Normal link" link="https://example.com" />

// Disabled link
<Link label="Disabled link" link="#" disabled={true} />

// External link (opens in new tab)
<Link label="External link" link="https://external.com" target="_blank" />
```

---

## 5. Custom styling

```tsx
// Custom CSS classes
<Link
  label="Custom styled link"
  link="#"
  className="custom-link-class hover:text-blue-600"
/>

// Inline styles
<Link
  label="Styled link"
  link="#"
  style={{ fontWeight: 'bold', textDecoration: 'none' }}
/>
```

---

## 6. Full prop reference

### Basic Props

| Prop     | Type                   | Default  | Description                     |
| -------- | ---------------------- | -------- | ------------------------------- |
| `label`  | `string`               | `"link"` | Link text content (required)    |
| `link`   | `string`               | `""`     | URL or href destination         |
| `size`   | `'sm' \| 'md' \| 'lg'` | `'md'`   | Link size affecting font size   |
| `subtle` | `boolean`              | `true`   | Use subtle styling vs prominent |

### States

| Prop       | Type      | Default | Description               |
| ---------- | --------- | ------- | ------------------------- |
| `disabled` | `boolean` | `false` | Disable link interactions |

### Styling

| Prop        | Type     | Description            |
| ----------- | -------- | ---------------------- |
| `className` | `string` | Additional CSS classes |

### Standard Anchor Props

The Link component accepts all standard HTML anchor element props including:

| Prop     | Type     | Description                     |
| -------- | -------- | ------------------------------- |
| `target` | `string` | Where to open the linked doc    |
| `rel`    | `string` | Relationship to linked resource |

---

## 7. Recipes

### Inline text link

```tsx
<p>
  Please read our <Link label="terms of service" link="/terms" size="sm" subtle={true} /> before
  continuing.
</p>
```

### Standalone navigation link

```tsx
<Link label="View all products" link="/products" size="md" subtle={false} />
```

### External link with security

```tsx
<Link
  label="Visit our GitHub"
  link="https://github.com/company/repo"
  target="_blank"
  rel="noopener noreferrer"
  subtle={false}
/>
```

### Disabled link state

```tsx
<Link label="Coming soon" link="#" disabled={true} size="md" />
```

### Custom styled link

```tsx
<Link
  label="Custom link"
  link="/custom"
  className="text-purple-600 hover:text-purple-800 underline-offset-4"
  subtle={false}
/>
```

### Large prominent call-to-action link

```tsx
<Link label="Get started today" link="/signup" size="lg" subtle={false} className="font-bold" />
```

---

## 8. Accessibility

The Link component includes several accessibility features:

- Proper semantic anchor element usage
- Keyboard navigation support (Enter key)
- Focus management with visible focus rings
- Disabled state prevents interaction and keyboard focus
- Proper visited state styling

```tsx
<Link
  label="Accessible link"
  link="/help"
  aria-describedby="help-description"
  title="Get help and support"
/>
```

---

## 9. Design Tokens

The Link component uses the following design system tokens:

**Typography:**

- Font sizes: `14px` (sm), `16px` (md), `18px` (lg)
- Font weight: `500` (medium)
- Text decoration: `underline` (for non-subtle links)
- Underline offset: `4px`

**Colors:**

- Subtle text: `text-color-text-subdued-1`
- Prominent text: `text-color-primary-60`
- Hover state: `text-color-primary-50`
- Active state: `text-color-primary-60`
- Visited state: `text-color-text-subdued-1`
- Disabled state: `text-color-text-subdued-2` with 30% opacity

**Focus rings:**

- `focus-visible:outline-gd-2`
- `focus-visible:outline-color-primary-60`

---

Consider using Link with:

- **Typography** — For text integration
- **Navigation** — For menu items
- **Card** — For clickable areas
- **Button** — For action alternatives
- **Icon** — For external link indicators
