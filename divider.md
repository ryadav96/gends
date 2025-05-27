# Divider

Horizontal or vertical rule used to separate content and/or present a **label** or **button** inline. Supports dashed style, orientation switch and subtle/intense colour.

---

## 1. Quick start

```tsx
import Divider from '@/components/genesis/atoms/divider/divider';

<Divider />

// With label
<Divider withLabel label="Section" />
```

---

## 2. Orientation

```tsx
<Divider orientation="horizontal" />  // default

<div className="flex h-40 items-center">
  <Divider orientation="vertical" className="h-full" />
</div>
```

---

## 3. Label vs button

| Prop | Behaviour |
|------|-----------|
| `withLabel` | Simply renders text centred between two lines |
| `button`    | Replaces the label with a clickable **Button** – inherits all Button props via `buttonProps` |

```tsx
// Label
<Divider withLabel label="OR" />

// Button (tertiary by default)
<Divider button label="Load more" onButtonClick={fetchMore} />
```

*Choose style through `buttonType` (`primary`, `secondary`, `tertiary`).*

---

## 4. Appearance tweaks

Option | Effect | Default
------ | ------ | -------
`dashed` | 4-px dash pattern instead of solid | `false`
`subtle` | Lighter grey tone | `true`
`bold`   | Sets label / button font-weight 600 | `false`

---

## 5. Styling hooks

* `className` – wrapper div
* `lineClassName` – `<Separator>` elements
* `labelClassName` – `<span>` or Button

---

## 6. Prop reference

| Prop | Type | Default |
|------|------|---------|
| `orientation` | `'horizontal' \| 'vertical'` | `'horizontal'` |
| `withLabel` | `boolean` | `false` |
| `label` | `string` | `'label'` |
| `button` | `boolean` | `false` |
| `buttonType` | `'primary' \| 'secondary' \| 'tertiary'` | `'tertiary'` |
| `onButtonClick` | `() => void` | – |
| `prefixIcon` / `suffixIcon` | `ReactNode` | – |
| `dashed` | `boolean` | `false` |
| `subtle` | `boolean` | `true` |
| Styling hooks | `className`, `labelClassName`, `lineClassName` |

---

## 7. Recipes

### Form section divider

```tsx
<Divider withLabel label="Billing information" bold />
```

### Infinite scroll sentinel

```tsx
<Divider
  button
  label="Load older messages"
  buttonType="secondary"
  onButtonClick={loadMore}
  prefixIcon={<IcArrowDown />}
/>
```

---