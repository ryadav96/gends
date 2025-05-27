# Badge

Small label used to highlight status, category or numeric value. Comes in four sizes, five semantic colour palettes and two visual intensities (*standard* and *subtle*). Optional icon support.

---

## 1. Quick start

```tsx
import Badge from 'gends';

<Badge appearance="Success">Live</Badge>
```

---

## 2. Sizes

| size | Height | Text scale |
|------|--------|------------|
| `xs` | 20 px | `body-s` |
| `s`  | 24 px | `body-s` |
| `m`  | 28 px | `body-m` (default) |
| `l`  | 32 px | `body-l` |

```tsx
<Badge size="xs">XS</Badge>
<Badge size="s">S</Badge>
<Badge size="m">M</Badge>
<Badge size="l">L</Badge>
```

---

## 3. Appearances

| appearance | BG | Text |
|------------|----|------|
| `Default` | Primary-20 | Primary-60 |
| `Success` | Success-20 | Success-80 |
| `Error` | Error-20 | Error-80 |
| `Warning` | Warning-20 | Warning-80 |
| `Neutral` | Grey-40 | Grey-80 |

Set `subtle={false}` (default) for an **intense** style (solid background). Pass `subtle` for pastel variant.

```tsx
// Subtle warning
<Badge appearance="Warning" subtle>Low stock</Badge>
```

---

## 4. Icons

```tsx
import { IcFavorite } from '@/components/genesis/atoms/Icons/Icons';

<Badge icon={<IcFavorite />} appearance="Neutral">Starred</Badge>
```

Icon automatically sizes according to `size` and inherits colour.

---

## 5. Custom styles

For extreme cases supply `customStyles` to override paddings / colours / radius.

```tsx
<Badge
  customStyles={{
    backgroundColor: '#111',
    textColor: '#fff',
    borderRadius: '0',
    padding: '4px 12px',
  }}
>
  Dark
</Badge>
```

---

## 6. Full prop reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `size` | `'xs' \| 's' \| 'm' \| 'l'` | `'m'` | Dimensions & typography |
| `appearance` | `'Default' \| 'Success' \| 'Error' \| 'Warning' \| 'Neutral'` | `'Default'` | Colour palette |
| `subtle` | `boolean` | `false` | Pastel background |
| `text` | `string` | `'label'` | Simple text (overridden by `children`) |
| `icon` | `ReactNode` | – | Leading icon |
| `classNames` | `{ badgeContainerClasses; iconContainerClasses; textClasses }` | – | Internal style hooks |
| `customStyles` | `{ backgroundColor; textColor; padding; height; borderRadius; iconColor }` | – | Inline overrides |

---

## 7. Recipes

### Status chip with icon

```tsx
<Badge size="s" appearance="Error" icon={<IcError />}>Failed</Badge>
```

### Pill-shaped category label

```tsx
<Badge subtle customStyles={{ borderRadius: '9999px', padding: '2px 10px' }}>
  Finance
</Badge>
```

---
