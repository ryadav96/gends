# ProgressBar

A versatile progress indicator component that supports both linear and circular variants, multiple sizes, colors, and customization options.

---

## 1. Quick start

```tsx
import { ProgressBar } from "gends";

function Example() {
  return (
    <ProgressBar value={75} max={100} color="default" showLabel={true} label="Upload Progress" />
  );
}
```

---

## 2. Variants

The ProgressBar component supports two variants:

| Variant  | Description                 | Use case                    |
| -------- | --------------------------- | --------------------------- |
| `line`   | Horizontal progress bar     | File uploads, form progress |
| `circle` | Circular progress indicator | Loading states, metrics     |

```tsx
// Linear progress
<ProgressBar
  variant="line"
  value={75}
  max={100}
  showLabel={true}
  label="Linear Progress"
/>

// Circular progress
<ProgressBar
  variant="circle"
  value={75}
  max={100}
  showValue={true}
/>
```

---

## 3. Colors

The ProgressBar component supports four color variants:

| Color     | Description   | Use case         |
| --------- | ------------- | ---------------- |
| `default` | Primary color | General progress |
| `success` | Green color   | Success states   |
| `error`   | Red color     | Error states     |
| `warning` | Orange color  | Warning states   |

```tsx
<ProgressBar color="default" value={75} />
<ProgressBar color="success" value={75} />
<ProgressBar color="error" value={75} />
<ProgressBar color="warning" value={75} />
```

---

## 4. Sizes

The ProgressBar component supports four size variants:

| Size | Description              | Use case                    |
| ---- | ------------------------ | --------------------------- |
| `xs` | Extra small (2px height) | Compact UI, inline progress |
| `sm` | Small (4px height)       | Dense layouts               |
| `md` | Medium (6px height)      | Standard usage              |
| `lg` | Large (8px height)       | Prominent progress          |

```tsx
<ProgressBar size="xs" value={75} />
<ProgressBar size="sm" value={75} />
<ProgressBar size="md" value={75} />
<ProgressBar size="lg" value={75} />
```

---

## 5. Custom Styling

Apply custom styles to different parts of the progress bar:

```tsx
<ProgressBar
  value={75}
  max={100}
  className="custom-progress"
  textStyle={{ color: "#666" }}
  valueStyle={{ fontWeight: "bold" }}
  circleRadius={50}
  strokeWidth={4}
/>
```

---

## 6. Full Prop Reference

### Basic Props

| Prop      | Type                                             | Default     | Description                      |
| --------- | ------------------------------------------------ | ----------- | -------------------------------- |
| `value`   | `number`                                         | `0`         | Current progress value           |
| `max`     | `number`                                         | `100`       | Maximum progress value           |
| `color`   | `'default' \| 'success' \| 'error' \| 'warning'` | `'default'` | Progress color variant           |
| `variant` | `'line' \| 'circle'`                             | `'line'`    | Progress bar variant             |
| `size`    | `'xs' \| 'sm' \| 'md' \| 'lg'`                   | `'md'`      | Size variant of the progress bar |

### Display Props

| Prop        | Type      | Default | Description                  |
| ----------- | --------- | ------- | ---------------------------- |
| `showLabel` | `boolean` | `true`  | Show/hide the progress label |
| `showValue` | `boolean` | `true`  | Show/hide the progress value |
| `label`     | `string`  | `""`    | Custom label text            |

### Styling Props

| Prop           | Type     | Default | Description                                 |
| -------------- | -------- | ------- | ------------------------------------------- |
| `className`    | `string` | -       | Additional CSS classes for the progress bar |
| `textStyle`    | `object` | `{}`    | Custom styles for the text                  |
| `valueStyle`   | `object` | `{}`    | Custom styles for the value                 |
| `circleRadius` | `number` | -       | Custom radius for circle variant            |
| `strokeWidth`  | `number` | -       | Custom stroke width for circle variant      |

---

## 7. Recipes

### File Upload Progress

```tsx
<ProgressBar
  variant="line"
  value={uploadProgress}
  max={100}
  color="default"
  showLabel={true}
  label="Uploading file..."
  showValue={true}
  size="md"
/>
```

### Circular Loading Indicator

```tsx
<ProgressBar
  variant="circle"
  value={loadingProgress}
  max={100}
  color="default"
  showValue={true}
  size="lg"
  circleRadius={40}
  strokeWidth={4}
/>
```

### Error State Progress

```tsx
<ProgressBar
  variant="line"
  value={errorProgress}
  max={100}
  color="error"
  showLabel={true}
  label="Failed to complete"
  showValue={true}
  size="md"
/>
```

---

## 8. Accessibility

The ProgressBar component includes several accessibility features:

- Proper ARIA attributes:
  - `role="progressbar"` for progress indication
  - `aria-valuenow` for current value
  - `aria-valuemin` for minimum value
  - `aria-valuemax` for maximum value
- Color contrast compliance
- Clear visual hierarchy
- Screen reader support

```tsx
<ProgressBar value={75} max={100} role="progressbar" aria-label="Download progress" />
```

---

## 9. Design Tokens

The ProgressBar component uses the following design system tokens:

**Colors:**

- Default: `primary-50`
- Success: `feedback-success-50`
- Error: `feedback-error-50`
- Warning: `feedback-warning-50`

**Text Colors:**

- Default: `var(--gd-primary-60)`
- Success: `var(--gd-feedback-success-80)`
- Error: `var(--gd-feedback-error-80)`
- Warning: `var(--gd-feedback-warning-80)`

**Sizes:**

- XS: `h-gd-2`
- SM: `h-gd-4`
- MD: `h-[6px]`
- LG: `h-gd-8`

**Typography:**

- XS: `text-en-desktop-body-s`
- SM: `text-en-desktop-body-xs`
- MD: `text-en-desktop-body-m`
- LG: `text-en-desktop-heading-xl`

**Layout:**

- Border radius: `rounded-full`
- Overflow: `overflow-hidden`

**Transitions:**

- Progress animation: `transition-all duration-300 ease-in-out`

---

Consider using ProgressBar with:

- **Button** — For action triggers
- **Text** — For labels and values
- **Icon** — For status indicators
- **Form** — For form progress
- **Modal** — For loading states
- **Card** — For progress cards
