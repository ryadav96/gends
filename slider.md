# Slider

A versatile slider component that supports multiple variants including single value, range, center-point, and tick marks—perfect for numeric input controls and value selection.

---

## 1. Quick start

```tsx
import { Slider } from "gends";

function Example() {
  return (
    <Slider
      variant="single"
      size="small"
      min={0}
      max={100}
      defaultValue={[50]}
      onValueChange={value => console.log(value)}
    />
  );
}
```

---

## 2. Slider variants

| variant             | Description                     | Use case                  |
| ------------------- | ------------------------------- | ------------------------- |
| `single`            | Single thumb slider             | Simple value selection    |
| `range`             | Two thumbs for range selection  | Min/max range picking     |
| `center`            | Single thumb with center point  | Offset from center values |
| `ticks`             | Single thumb with tick marks    | Stepped value selection   |
| `ticks-with-labels` | Single thumb with labeled ticks | Precise stepped selection |

```tsx
<Slider variant="single" defaultValue={[25]} />
<Slider variant="range" defaultValue={[25, 75]} />
<Slider variant="center" defaultValue={[50]} />
<Slider variant="ticks" tickCount={10} />
<Slider variant="ticks-with-labels" tickCount={5} />
```

---

## 3. Sizes

| size    | Track height | Thumb size | Recommended use |
| ------- | ------------ | ---------- | --------------- |
| `small` | 2px          | 16px       | Compact forms   |
| `large` | 4px          | 20px       | Prominent input |

```tsx
<Slider size="small" defaultValue={[50]} />
<Slider size="large" defaultValue={[50]} />
```

---

## 4. Input states

| inputState | Description        | Visual treatment     |
| ---------- | ------------------ | -------------------- |
| `default`  | Normal state       | Standard colors      |
| `success`  | Success validation | Green accent colors  |
| `error`    | Error validation   | Red accent colors    |
| `warning`  | Warning validation | Orange accent colors |
| `focused`  | Focused state      | Enhanced focus ring  |

```tsx
<Slider inputState="default" defaultValue={[50]} />
<Slider inputState="success" defaultValue={[50]} />
<Slider inputState="error" defaultValue={[50]} />
<Slider inputState="warning" defaultValue={[50]} />
```

---

## 5. Value display and units

```tsx
// With value display and custom unit
<Slider
  showValue={true}
  unit="px"
  defaultValue={[100]}
  min={0}
  max={500}
/>

// With label
<Slider
  label="Opacity"
  unit="%"
  defaultValue={[80]}
  min={0}
  max={100}
/>

// Range slider with dual inputs
<Slider
  variant="range"
  showValue={true}
  unit="rem"
  defaultValue={[1, 3]}
  min={0}
  max={5}
/>
```

---

## 6. Tick configuration

```tsx
// Standard ticks
<Slider
  variant="ticks"
  tickCount={10}
  min={0}
  max={100}
  defaultValue={[50]}
/>

// Labeled ticks
<Slider
  variant="ticks-with-labels"
  tickCount={6}
  min={0}
  max={50}
  step={10}
  defaultValue={[20]}
/>
```

---

## 7. States and interaction

```tsx
// Disabled state
<Slider disabled={true} defaultValue={[50]} />;

// Controlled component
const [value, setValue] = useState([25]);

<Slider
  value={value}
  onValueChange={setValue}
  onChangeStart={value => console.log("Start:", value)}
  onChangeEnd={value => console.log("End:", value)}
/>;
```

---

## 8. Full prop reference

### Basic Props

| Prop      | Type                                                                | Default    | Description                 |
| --------- | ------------------------------------------------------------------- | ---------- | --------------------------- |
| `variant` | `'single' \| 'range' \| 'center' \| 'ticks' \| 'ticks-with-labels'` | `'single'` | Slider behavior type        |
| `size`    | `'small' \| 'large'`                                                | `'small'`  | Slider track and thumb size |
| `min`     | `number`                                                            | `0`        | Minimum value               |
| `max`     | `number`                                                            | `100`      | Maximum value               |
| `step`    | `number`                                                            | `1`        | Step increment              |
| `unit`    | `SliderUnit`                                                        | `'px'`     | Display unit for values     |

### Value Props

| Prop            | Type                        | Description                |
| --------------- | --------------------------- | -------------------------- |
| `value`         | `number[]`                  | Controlled value           |
| `defaultValue`  | `number[]`                  | Initial uncontrolled value |
| `onValueChange` | `(value: number[]) => void` | Value change handler       |

### Display Props

| Prop        | Type      | Default | Description                 |
| ----------- | --------- | ------- | --------------------------- |
| `showValue` | `boolean` | `true`  | Show value input field(s)   |
| `label`     | `string`  | -       | Slider label text           |
| `disabled`  | `boolean` | `false` | Disable slider interactions |

### State Props

| Prop         | Type                                                          | Default     | Description            |
| ------------ | ------------------------------------------------------------- | ----------- | ---------------------- |
| `inputState` | `'default' \| 'success' \| 'error' \| 'warning' \| 'focused'` | `'default'` | Validation/focus state |

### Tick Props

| Prop        | Type     | Default | Description                     |
| ----------- | -------- | ------- | ------------------------------- |
| `tickCount` | `number` | `10`    | Number of tick marks to display |

### Event Handlers

| Prop            | Type                        | Description             |
| --------------- | --------------------------- | ----------------------- |
| `onChangeStart` | `(value: number[]) => void` | Called when drag starts |
| `onChangeEnd`   | `(value: number[]) => void` | Called when drag ends   |

### Styling

| Prop        | Type     | Description            |
| ----------- | -------- | ---------------------- |
| `className` | `string` | Additional CSS classes |

---

## 9. Recipes

### Basic value slider

```tsx
<Slider
  label="Volume"
  min={0}
  max={100}
  defaultValue={[75]}
  unit="%"
  onValueChange={value => setVolume(value[0])}
/>
```

### Range selection

```tsx
<Slider
  label="Price Range"
  variant="range"
  min={0}
  max={1000}
  defaultValue={[100, 500]}
  unit="$"
  onValueChange={range => setPriceRange(range)}
/>
```

### Center-point adjustment

```tsx
<Slider
  label="Balance"
  variant="center"
  min={-100}
  max={100}
  defaultValue={[0]}
  showValue={true}
  onValueChange={value => setBalance(value[0])}
/>
```

### Stepped slider with ticks

```tsx
<Slider
  label="Font Size"
  variant="ticks-with-labels"
  min={12}
  max={72}
  step={4}
  tickCount={16}
  unit="px"
  defaultValue={[16]}
/>
```

### Disabled state

```tsx
<Slider label="Read-only Value" disabled={true} defaultValue={[60]} showValue={true} />
```

### Success validation state

```tsx
<Slider
  label="Valid Range"
  variant="range"
  inputState="success"
  defaultValue={[20, 80]}
  min={0}
  max={100}
/>
```

---

## 10. Accessibility

The Slider component includes comprehensive accessibility features:

- Proper ARIA attributes for screen readers
- Keyboard navigation support (Arrow keys, Home, End)
- Focus management with visible focus rings
- Value announcements for screen readers
- Disabled state handling

```tsx
<Slider
  label="Accessible slider"
  defaultValue={[50]}
  aria-label="Volume control"
  onValueChange={value => announceValue(value)}
/>
```

---

## 11. Design Tokens

The Slider component uses the following design system tokens:

**Sizing:**

- Small track height: `2px`
- Large track height: `4px`
- Small thumb: `16px` diameter
- Large thumb: `20px` diameter
- Input field: `80px` width, `32px` height

**Colors:**

- Track background: `color-neutral-grey-40`
- Active track: `color-primary-50`
- Thumb: `color-primary-50`
- Thumb hover: `color-primary-20` border
- Focus ring: `color-primary-70`
- Disabled: `color-neutral-grey-60`

**Spacing:**

- Label margin: `gd-1`
- Value input margin: `gd-2`
- Tick spacing: Calculated based on `tickCount`

**Typography:**

- Label: `text-sm font-small`
- Value inputs: `text-sm`
- Unit labels: `text-muted-foreground`

---

Consider using Slider with:

- **Form** — For numeric input controls
- **Settings** — For preference adjustments
- **Filters** — For range selection
- **Media** — For volume/progress controls
- **Design tools** — For property adjustments
