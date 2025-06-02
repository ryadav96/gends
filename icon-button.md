# IconButton

A versatile icon-only button component that supports multiple types, appearances, sizes, and states—perfect for compact UI actions and toolbar buttons.

---

## 1. Quick start

```tsx
import { IconButton } from "gends";
import { IcClose } from "../../Icons/Icons";

function Example() {
  return (
    <IconButton
      type="primary"
      appearance="default"
      size="md"
      icon={<IcClose />}
      onClick={() => console.log("Clicked")}
    />
  );
}
```

---

## 2. Sizes

| size | Dimensions | Icon size | Recommended use       |
| ---- | ---------- | --------- | --------------------- |
| `xs` | 16px       | 12px      | Ultra compact actions |
| `sm` | 20px       | 16px      | Compact toolbars      |
| `md` | 24px       | 20px      | Standard usage        |
| `lg` | 32px       | 24px      | Prominent actions     |
| `xl` | 40px       | 28px      | Hero/featured actions |

```tsx
<IconButton size="xs" icon={<IcClose />} />
<IconButton size="sm" icon={<IcClose />} />
<IconButton size="md" icon={<IcClose />} />
<IconButton size="lg" icon={<IcClose />} />
<IconButton size="xl" icon={<IcClose />} />
```

---

## 3. Button types

The component supports three distinct button styles:

| type        | Description                          | Use case              |
| ----------- | ------------------------------------ | --------------------- |
| `primary`   | Filled background with solid colors  | Main actions, CTAs    |
| `secondary` | Outlined style with transparent fill | Secondary actions     |
| `tertiary`  | Text-only with optional background   | Subtle actions, tools |

```tsx
<IconButton type="primary" icon={<IcClose />} />
<IconButton type="secondary" icon={<IcClose />} />
<IconButton type="tertiary" icon={<IcClose />} />
```

---

## 4. Appearance variants

| appearance | Primary colors       | Secondary colors    | Tertiary colors | Use case            |
| ---------- | -------------------- | ------------------- | --------------- | ------------------- |
| `default`  | Blue backgrounds     | Blue outline/text   | Blue text       | Standard actions    |
| `positive` | Green backgrounds    | Green outline/text  | Green text      | Success actions     |
| `negative` | Red backgrounds      | Red outline/text    | Red text        | Destructive actions |
| `warning`  | Orange backgrounds   | Orange outline/text | Orange text     | Warning actions     |
| `ai`       | Gradient (teal/blue) | Gradient outline    | Gradient icon   | AI-powered features |

```tsx
<IconButton appearance="default" icon={<IcClose />} />
<IconButton appearance="positive" icon={<IcClose />} />
<IconButton appearance="negative" icon={<IcClose />} />
<IconButton appearance="warning" icon={<IcClose />} />
<IconButton appearance="ai" icon={<IcClose />} />
```

---

## 5. States

```tsx
// Selected state
<IconButton selected={true} icon={<IcClose />} />

// Disabled state
<IconButton disabled={true} icon={<IcClose />} />

// Inverse colors (for dark backgrounds)
<IconButton inverse={true} icon={<IcClose />} />
```

---

## 6. AI appearance special features

The AI appearance has special behavior and sizing:

```tsx
// AI appearance automatically uses gradient icons
<IconButton appearance="ai" type="secondary" size="md" />

// AI buttons have larger dimensions for better visual impact
<IconButton appearance="ai" type="primary" size="lg" />
```

---

## 7. Custom styling

```tsx
// Custom button classes
<IconButton
  icon={<IcClose />}
  classNames={{
    button: "custom-button-class",
    icon: "custom-icon-class",
    container: "custom-container-class"
  }}
/>

// Custom styles
<IconButton
  icon={<IcClose />}
  style={{ margin: "10px" }}
/>
```

---

## 8. Full prop reference

### Basic Props

| Prop         | Type                                                         | Default     | Description                      |
| ------------ | ------------------------------------------------------------ | ----------- | -------------------------------- |
| `size`       | `'xs' \| 'sm' \| 'md' \| 'lg' \| 'xl'`                       | `'md'`      | Button size affecting dimensions |
| `type`       | `'primary' \| 'secondary' \| 'tertiary'`                     | `'primary'` | Button style variant             |
| `appearance` | `'default' \| 'positive' \| 'negative' \| 'warning' \| 'ai'` | `'default'` | Color scheme variant             |
| `icon`       | `ReactNode`                                                  | -           | Icon to display (required)       |

### States

| Prop       | Type      | Default | Description                             |
| ---------- | --------- | ------- | --------------------------------------- |
| `selected` | `boolean` | `false` | Show selected state styling             |
| `disabled` | `boolean` | `false` | Disable button interactions             |
| `inverse`  | `boolean` | `false` | Use inverse colors for dark backgrounds |

### Events & Styling

| Prop         | Type                                                     | Description         |
| ------------ | -------------------------------------------------------- | ------------------- |
| `onClick`    | `(ev: MouseEvent<HTMLButtonElement>) => void`            | Click event handler |
| `classNames` | `{ button?: string; icon?: string; container?: string }` | Custom CSS classes  |
| `style`      | `React.CSSProperties`                                    | Inline styles       |
| `id`         | `string`                                                 | Element ID          |

### Advanced

| Prop           | Type          | Description                       |
| -------------- | ------------- | --------------------------------- |
| `buttonProps`  | `ButtonProps` | Props passed to underlying Button |
| `counterbadge` | `boolean`     | Show counter badge (deprecated)   |
| `iconName`     | `string`      | Icon name (deprecated)            |

---

## 9. Recipes

### Close button for modals

```tsx
<IconButton
  type="tertiary"
  appearance="default"
  size="sm"
  icon={<IcClose />}
  onClick={handleClose}
/>
```

### Delete action button

```tsx
<IconButton
  type="primary"
  appearance="negative"
  size="md"
  icon={<IcTrash />}
  onClick={handleDelete}
/>
```

### AI feature button

```tsx
<IconButton type="secondary" appearance="ai" size="lg" onClick={handleAIAction} />
```

### Toolbar button with selected state

```tsx
<IconButton
  type="secondary"
  appearance="default"
  size="md"
  icon={<IcBold />}
  selected={isBold}
  onClick={toggleBold}
/>
```

### Inverse button for dark backgrounds

```tsx
<div className="bg-gray-900 p-4">
  <IconButton type="primary" appearance="default" size="md" icon={<IcSettings />} inverse={true} />
</div>
```

### Custom styled button

```tsx
<IconButton
  icon={<IcHeart />}
  classNames={{
    button: "hover:scale-110 transition-transform",
    icon: "text-red-500",
  }}
  style={{ borderRadius: "8px" }}
/>
```

---

## 10. Accessibility

The IconButton component includes several accessibility features:

- Proper ARIA attributes for screen readers
- Focus management with visible focus rings
- Keyboard navigation support (Enter and Space keys)
- Disabled state prevents interaction and keyboard focus

```tsx
<IconButton
  icon={<IcClose />}
  onClick={handleClose}
  disabled={!canClose}
  aria-label="Close dialog"
/>
```

---

## 11. Design Tokens

The IconButton component uses the following design system tokens:

**Sizing:**

- Button dimensions: `16px`, `20px`, `24px`, `32px`, `40px`
- Icon sizes: `12px`, `16px`, `20px`, `24px`, `28px`
- Border radius: `rounded-full` (fully rounded)

**Colors:**

- Primary: `#3535F3` (blue) family
- Success: `#25AB21` (green) family
- Error: `#F50031` (red) family
- Warning: `#F06D0F` (orange) family
- AI gradient: `#1ECCB0` to `#3535F3`

**Focus rings:**

- `ring-[4px]` with color matching appearance
- `focus-visible:ring-offset-0`

---

Consider using IconButton with:

- **Tooltip** — For action descriptions
- **Modal** — For close actions
- **Toolbar** — For tool actions
- **Card** — For quick actions
- **Navigation** — For menu toggles
