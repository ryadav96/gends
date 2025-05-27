# Slot

Developer-tooling helper that provides a **drop‐zone** like placeholder. Primarily used inside editors or drag-and-drop builders to visualise empty areas.

---

## 1. Quick start

```tsx
import { Slot } from 'gends';

<Slot />

<Slot placeholder="Drop widget here" />
```

---

## 2. Behaviour

1. If `children` are present ➜ render them.
2. Else if `showPlaceholder` ➜ display `placeholder` text.
3. Background is a subtle primary tint with dashed border; gains solid accent when `isActive`.

---

## 3. Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `showPlaceholder` | `boolean` | `true` | Toggle placeholder when empty |
| `placeholder` | `string` | `'Replace'` | Text shown when empty |
| `isActive` | `boolean` | `false` | You can pass `true` when the user is currently dragging over the slot to highlight it |
| `className` | `string` | – | Extra classes for root |

---

## 4. Recipes

### Drag-and-drop highlight

```tsx
<Slot
  isActive={isOver}
  showPlaceholder={false}
  className={isOver ? 'border-color-primary-60 bg-color-primary-10' : ''}
>
  {children}
</Slot>
```

### Placeholder only on hover

```tsx
<Slot showPlaceholder={false} onMouseEnter={() => setHover(true)} />
```

---