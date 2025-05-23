# Input

Highly-configurable text / number field that supports labels, validation messaging, prefix & suffix icons, character counter, numeric steppers and more—all in one composable component.

---

## 1. Quick start

```tsx
import { Input } from 'gends';

function Example() {
  const [value, setValue] = useState('');

  return (
    <Input
      label="Email"
      placeholder="you@example.com"
      type="email"
      value={value}
      onValueChange={setValue}
      prefix={<IcMail size="24px" />}
    />
  );
}
```

Wrap **nothing else**—`Input` is self-contained. For form libraries (React-Hook-Form, Formik, usw.) just forward `value` / `onChange` (or use the provided `onValueChange`).

---

## 2. Sizes

| size | Height | Recommended type scale |
|------|--------|------------------------|
| `s`  | 32 px  | `body-m`               |
| `m`  | 40 px  | `body-m`               |
| `l`  | 48 px  | `body-l`               |

```tsx
<Input size="s" label="Small" placeholder="…" />
<Input size="m" label="Medium" placeholder="…" />
<Input size="l" label="Large" placeholder="…" />
```

---

## 3. Validation states

| validationState | Border colour | Helper-text colour |
|-----------------|---------------|--------------------|
| `none` (default)| Neutral-40    | Neutral-60         |
| `success`       | Success-50    | Success-50         |
| `warning`       | Warning-50    | Warning-50         |
| `error`         | Error-50      | Error-50           |

```tsx
<Input validationState="success" validationMessage="Looks good!" />
<Input validationState="warning" validationMessage="Hmm, double-check this." />
<Input validationState="error"   validationMessage="Required field" />
```

Focus state shows a 2px ring with the same colour.

---

## 4. Numeric helpers

`type="number"` unlocks additional features:

* **Stepper variant** — Up/Down buttons grouped on the right.
* **Split variant** — Up button on the right, Down button on the left.
* Respect `min`, `max`, `step` attributes; buttons auto-disable at limits.

```tsx
// Standard number field
<Input label="Age" type="number" min={0} max={120} />

// Stepper (buttons together)
<Input label="Qty" type="number" numberVariant="stepper" min={0} max={10} />

// Split (buttons each side)
<Input label="Qty" type="number" numberVariant="split" min={0} max={10} />
```

---

## 5. Icons & adornments

Property | Purpose
---------|---------
`prefix` | React node rendered at the left (e.g. icon, currency code)
`suffix` | React node rendered at the right (e.g. units, icon)
`showPrefixDivider` / `showSuffixDivider` | Render a 1px grey divider between the adornment and the text field

Password fields (`type="password"`) automatically get **lock**, **eye** and **eye-off** icons—you can always override by supplying your own `prefix` / `suffix`.

Clear (`×`) and copy-to-clipboard icons are shown contextually:

```tsx
// Hide clear icon (×)
<Input hideClearIcon />

// Enable copy icon when field has value
<Input allowCopy onCopy={v => console.log('copied', v)} />
```

---

## 6. Character counter

```tsx
<Input
  label="Username"
  maxLength={20}
  showCounter
  placeholder="max 20 chars"
/>
```

Counter appears bottom-right and updates live.

---

## 7. Help tooltip

```tsx
<Input
  label="Password"
  type="password"
  showHelpIcon
  helpTooltipMessage="Must be at least 8 characters and contain a symbol."
/>
```

Use `handleHelpClick` to provide a custom action instead of tooltip.

---

## 8. Disabled & read-only

```tsx
<Input label="Disabled" value="can't touch this" disabled />
<Input label="Read-only" value="immutable" readOnly />
```

Disabled = greyed-out + `cursor: not-allowed`. Read-only keeps full opacity but uses a neutral background.

---

## 9. Full prop reference

### Basic

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `label` | `string` | – | Text displayed above the field |
| `placeholder` | `string` | – | Placeholder when empty |
| `size` | `'s' \| 'm' \| 'l'` | `'l'` | Component height & typography |
| `type` | standard HTML types | `'text'` | All native input types work (`password`, `email`, `number`, …) |
| `value` | `string \| number` | – | Controlled value |
| `defaultValue` | `string \| number` | – | Uncontrolled initial value |
| `onValueChange` | `(val) => void` | – | Fires on every change (works for controlled or uncontrolled) |

### Validation

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `validationState` | `'none' \| 'success' \| 'warning' \| 'error'` | `'none'` | Border / ring colour |
| `validationMessage` | `string` | – | Helper / error text under the field |

### Numeric-only

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `numberVariant` | `'stepper' \| 'split' \| null` | `null` | Layout of increment / decrement buttons |
| `min` / `max` / `step` | `number` | – | Same as native input attributes |

### Adornments & Icons

| Prop | Type | Description |
|------|------|-------------|
| `prefix` / `suffix` | `ReactNode` | Element before / after the field |
| `showPrefixDivider` / `showSuffixDivider` | `boolean` | Show grey divider |
| `hideClearIcon` | `boolean` | Remove `×` icon (text inputs only) |
| `allowCopy` | `boolean` | Show copy icon when field has value |
| `onCopy` | `(val) => void` | Custom copy handler |

### Counter

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `showCounter` | `boolean` | `false` | Display live `value.length / maxLength` |
| `maxLength` | `number` | – | Required to calculate counter |

### Help

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `showHelpIcon` | `boolean` | `false` | Display help icon next to label |
| `helpTooltipMessage` | `string` | – | Tooltip text (shown on hover) |
| `handleHelpClick` | `() => void` | – | Custom click handler instead of tooltip |

### States

`disabled`, `readOnly`, `required` → same semantics as native inputs.

### Styling hooks

| Prop | Area |
|------|------|
| `className` | Root wrapper |
| `containerClassName` | Flex container holding icons + input |
| `inputClassName` | `<input>` element itself |
| `labelClassName`, `validationClassName`, `counterClassName` |
| `prefixClassName`, `suffixClassName` |

---

## 10. Recipes

### Email with prefix + copy-to-clipboard

```tsx
<Input
  label="Email"
  type="email"
  placeholder="you@example.com"
  prefix={<IcMail size="20px" />}
  allowCopy
/>
```

### Password field with helper tooltip

```tsx
<Input
  label="Password"
  type="password"
  required
  showHelpIcon
  helpTooltipMessage="Minimum 8 characters, include a number or symbol."
/>
```

### Number (split buttons) with validation

```tsx
<Input
  label="Quantity"
  type="number"
  numberVariant="split"
  min={1}
  max={5}
  step={1}
  validationState="error"
  validationMessage="Between 1 and 5 only"
/>
```

---

## 11. Related components

The **Input bundle** also exports:

* **OTPInput** – fixed-width multi-digit input for one-time passwords.
* **TextArea** – auto-grows multi-line field with the same API (`size`, `validationState`, counters, etc.).

Refer to their respective Storybook stories under `Forms / Input` for examples.

---

## 12. Storybook playground

Run `pnpm storybook` and open **Forms / Input** to experiment with every knob.

The underlying file is

```
src/components/genesis/molecules/input/input.stories.tsx
```

which you can also use as reference for advanced patterns.
