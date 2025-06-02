# Radio Button

A flexible radio button component that supports multiple sizes, validation states, support text, and customizable styling—perfect for single-selection options in forms and interactive interfaces.

---

## 1. Quick start

```tsx
import { RadioButtons } from "gends";

function Example() {
  const options = [
    { label: "Option 1", value: "1" },
    { label: "Option 2", value: "2" },
    { label: "Option 3", value: "3" },
  ];

  return (
    <RadioButtons
      options={options}
      defaultVal="1"
      onChange={option => console.log("Selected:", option)}
    />
  );
}
```

Wrap **nothing else**—`RadioButtons` is self-contained and manages its own state. For form libraries, just forward the `onChange` handler.

---

## 2. Sizes

| Size | Height | Radio Size | Text Scale |
| ---- | ------ | ---------- | ---------- |
| `s`  | 16px   | 16×16px    | `body-m`   |
| `m`  | 20px   | 20×20px    | `body-m`   |
| `l`  | 24px   | 24×24px    | `body-l`   |

```tsx
<RadioButtons size="s" options={options} />
<RadioButtons size="m" options={options} />
<RadioButtons size="l" options={options} />
```

---

## 3. Validation states

| alertType | Icon Color       | Text Color      | Use Case            |
| --------- | ---------------- | --------------- | ------------------- |
| `success` | Green (#25AB21)  | Success subdued | Positive feedback   |
| `warning` | Orange (#F06D0F) | Warning subdued | Cautionary feedback |
| `error`   | Red (#F50031)    | Error subdued   | Error indication    |

```tsx
<RadioButtons
  options={options}
  alertType="success"
  renderAlert={(type) => <div>Custom success message</div>}
/>

<RadioButtons
  options={options}
  alertType="warning"
  renderAlert={(type) => <div>Custom warning message</div>}
/>

<RadioButtons
  options={options}
  alertType="error"
  renderAlert={(type) => <div>Custom error message</div>}
/>
```

---

## 4. Support text

Add additional context below each radio option:

```tsx
<RadioButtons options={options} supportText="Additional information about this option" />
```

Support text inherits the size variant's text scale and uses a subdued color.

---

## 5. States

| State    | Visual feedback              | Behavior        |
| -------- | ---------------------------- | --------------- |
| Default  | Normal appearance            | Clickable       |
| Hover    | Text color change            | Cursor pointer  |
| Selected | Filled radio + text emphasis | Current choice  |
| Disabled | 30% opacity                  | Not interactive |

```tsx
<RadioButtons options={options} />
<RadioButtons options={options} disabled />
```

---

## 6. Full prop reference

### Basic

| Prop         | Type                            | Default | Description                 |
| ------------ | ------------------------------- | ------- | --------------------------- |
| `size`       | `'s' \| 'm' \| 'l'`             | `'m'`   | Component size variant      |
| `options`    | `RadioOption[]`                 | `[]`    | Array of options to display |
| `defaultVal` | `string`                        | -       | Initial selected value      |
| `disabled`   | `boolean`                       | `false` | Disable all options         |
| `onChange`   | `(option: RadioOption) => void` | -       | Selection change handler    |

### Validation & Support

| Prop          | Type                                | Default | Description              |
| ------------- | ----------------------------------- | ------- | ------------------------ |
| `alertType`   | `'success' \| 'warning' \| 'error'` | -       | Validation state         |
| `renderAlert` | `(alertType: string) => ReactNode`  | -       | Custom alert renderer    |
| `supportText` | `string`                            | -       | Helper text below option |

### Styling

| Prop                     | Type     | Default | Description            |
| ------------------------ | -------- | ------- | ---------------------- |
| `containerClassName`     | `string` | -       | Root container styles  |
| `optionWrapperClassName` | `string` | -       | Option wrapper styles  |
| `labelClassName`         | `string` | -       | Label text styles      |
| `radioClassName`         | `string` | -       | Radio button styles    |
| `alertClassName`         | `string` | -       | Alert container styles |
| `supportClassName`       | `string` | -       | Support text styles    |

---

## 7. Recipes

### Basic form field

```tsx
function FormField({ label, options, onChange }) {
  return (
    <div className="space-y-2">
      <label className="text-sm font-medium">{label}</label>
      <RadioButtons options={options} onChange={onChange} size="m" />
    </div>
  );
}
```

### With validation

```tsx
function ValidatedRadio({ options, value, error }) {
  return (
    <RadioButtons
      options={options}
      defaultVal={value}
      alertType={error ? "error" : undefined}
      renderAlert={type => <div className="text-error-500 text-sm">{error}</div>}
    />
  );
}
```

### With support text

```tsx
function RadioWithSupport({ options }) {
  const optionsWithSupport = options.map(option => ({
    ...option,
    supportText: `Additional details about ${option.label}`,
  }));

  return <RadioButtons options={optionsWithSupport} size="l" supportText />;
}
```

### Custom styling

```tsx
function StyledRadio({ options }) {
  return (
    <RadioButtons
      options={options}
      containerClassName="space-y-4"
      optionWrapperClassName="hover:bg-gray-50 p-2 rounded"
      labelClassName="font-medium"
      radioClassName="border-2"
    />
  );
}
```

### Disabled state with message

```tsx
function DisabledRadio({ options, message }) {
  return (
    <div className="opacity-75">
      <RadioButtons options={options} disabled supportText={message} />
    </div>
  );
}
```

---

## 8. Accessibility considerations

- Uses semantic HTML with proper ARIA attributes
- Supports keyboard navigation (Tab, Space)
- Maintains proper focus states
- Provides clear visual feedback
- Includes disabled state handling

```tsx
<RadioButtons options={options} aria-label="Select an option" aria-required="true" />
```

---

## 9. Design patterns

### Layout patterns

- Consistent vertical spacing
- Proper text alignment
- Clear visual hierarchy
- Responsive width handling

### Content patterns

- Clear label text
- Concise support text
- Meaningful validation messages
- Icon alignment

### Interaction patterns

- Hover state feedback
- Focus state indication
- Selection state clarity
- Disabled state handling

---

## 10. Related components

Consider using RadioButtons with:

- **Checkbox** — For multiple selection
- **Select** — For many options
- **Toggle** — For binary choices
- **FormField** — For labeled inputs
- **FormControl** — For form organization

---

## 11. Storybook playground

Run `pnpm storybook` and open **Atoms / RadioButton** to experiment with all configurations.

The underlying file is

```
src/components/genesis/atoms/radio-button/radio-button.stories.tsx
```

which you can use as reference for advanced patterns and implementation examples.
