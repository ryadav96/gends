# Scrollbar

Wrapper around `@radix-ui/react-scroll-area` that provides beautifully themed scrollbars in both orientations. Useful for tables, panels, sidebars – anywhere you need overflow control without default browser ugliness.

---

## 1. Quick start

```tsx
import Scrollbar from '@/components/genesis/atoms/scrollbar/scrollbar';

<Scrollbar style={{ maxHeight: 240 }}>
  {/** long content here */}
</Scrollbar>
```

The component auto-detects scroll direction and renders thumb(s) accordingly.

---

## 2. Orientation

| orientation | Rendered bars |
|-------------|---------------|
| `vertical`  | Y only (default) |
| `horizontal`| X only |
| `both`      | X + Y |

```tsx
<Scrollbar orientation="horizontal" maxWidth="400px">
  …
</Scrollbar>
```

---

## 3. Sizes

| size | Thumb thickness | Track thickness |
|------|-----------------|------------------|
| `small` | 4 px | 12 px |
| `large` | 8 px | 16 px |

Both orientations inherit this value.

---

## 4. Dimensions

Prop | Effect
---- | ------
`height` / `width` | Force viewport dimensions
`maxHeight` / `maxWidth` | Clamp viewport size (most common)

```tsx
<Scrollbar height="300px" width="100%">…</Scrollbar>
```

---

## 5. Styling hooks

| Hook | Targets |
|------|---------|
| `className` | Root `<ScrollArea>` |
| `classNames.viewport` | Content viewport |
| `classNames.container` | Scrollbar container |
| `classNames.scrollbar` | Thumb |

---

## 6. Prop reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `size` | `'small' \| 'large'` | `'small'` |
| `orientation` | `'vertical' \| 'horizontal' \| 'both'` | `'vertical'` |
| `height` / `width` | `string` | – | Fixed viewport dimensions |
| `maxHeight` / `maxWidth` | `string` | – | Max viewport dimensions |
| `style` | `React.CSSProperties` | – | Inline styles on root |
| `className` | `string` | – | Root class |
| `classNames` | See hooks table | – |

All other props are forwarded to Radix `ScrollArea.Root`.

---

## 7. Recipes

### Table with fixed header & scrollable body

```tsx
<div className="flex flex-col h-80">
  <TableHeader />
  <Scrollbar orientation="vertical" className="flex-1">
    <TableBody rows={rows} />
  </Scrollbar>
</div>
```

### Horizontal scroll gallery

```tsx
<Scrollbar orientation="horizontal" size="large" maxWidth="600px">
  <div className="flex gap-16">{images}</div>
</Scrollbar>
```

---