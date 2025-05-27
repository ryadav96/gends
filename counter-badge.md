# CounterBadge

Numeric badge specialised for counts (notifications, cart items…). Wraps the standard **Badge** component and adds sizes, circular pill shape and optional click behaviour.

---

## 1. Quick start

```tsx
import CounterBadge from 'gends';

<CounterBadge value="8" />
```

---

## 2. Sizes

| size | Height | Min-width | Text scale |
|------|--------|----------|------------|
| `xxs` | 16 px | 22 px | `body-xs` |
| `xs`  | 18 px | 24 px | `body-s` |
| `s`   | 24 px | 34 px | `body-m` |
| `m`   | 28 px | 38 px | `body-m` (default) |
| `l`   | 32 px | 45 px | `body-l` |

CounterBadge auto-horizontal pads to keep numbers centred.

---

## 3. Colours

| colour | Palette |
|--------|---------|
| `default` | Primary |
| `success` | Success |
| `error`   | Error |
| `warning` | Warning |

Pass `subtle` for pastel background, same as Badge.

---

## 4. Actionable mode

Set `actionable` to render a `<button>` wrapper, enabling keyboard focus, hover and `onClick` behaviour.

```tsx
<CounterBadge actionable onClick={() => console.log('open inbox')} />
```

Disabled styles are applied automatically when `actionable={false}` and the parent button is disabled.

---

## 5. Full prop reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `value` | `string` | `'99'` | Text rendered inside (keeps width fixed) |
| `size` | `'xxs' \| 'xs' \| 's' \| 'm' \| 'l'` | `'m'` | Dimensions |
| `color` | `'default' \| 'success' \| 'error' \| 'warning'` | `'default'` | Semantic colour |
| `subtle` | `boolean` | `false` | Pastel variant |
| `actionable` | `boolean` | `false` | Render button wrapper |
| `onClick` | `(e) => void` | – | Click handler (only when actionable) |
| `classNames` | `{ badgeProps; className }` | – | Forwarded style overrides |

---

## 6. Recipes

### Notification icon with badge

```tsx
<button className="relative">
  <IcBell />
  <span className="absolute -top-1 -right-1">
    <CounterBadge size="xxs" value="3" />
  </span>
</button>
```

### Clickable pill in table row

```tsx
<CounterBadge actionable size="s" value="15" color="success" />
```

---