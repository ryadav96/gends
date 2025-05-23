# Radio Button Component

The Radio Button component provides a set of selectable options where users can choose one option from a group. It supports different sizes, states, and validation messages.

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | `"s" \| "m" \| "l"` | `"m"` | Controls the size of the radio buttons |
| alertType | `"success" \| "warning" \| "error" \| undefined` | `undefined` | Sets the validation state with appropriate styling and icon |
| options | `RadioOption[]` | `[]` | Array of options to display as radio buttons |
| defaultVal | `string` | `undefined` | Sets the initially selected option |
| onChange | `(value: RadioOption) => void` | `undefined` | Callback function when selection changes |
| disabled | `boolean` | `false` | Disables all radio buttons in the group |
| containerClassName | `string` | `undefined` | Custom class for the radio group container |
| optionWrapperClassName | `string` | `undefined` | Custom class for each radio option wrapper |
| labelClassName | `string` | `undefined` | Custom class for radio button labels |
| radioClassName | `string` | `undefined` | Custom class for radio button inputs |
| alertClassName | `string` | `undefined` | Custom class for alert message container |
| supportClassName | `string` | `undefined` | Custom class for support text container |

## RadioOption Type

```typescript
interface RadioOption {
  label: string;    // Text displayed next to the radio button
  value: string;    // Unique value for the option
}
```

## Examples

### Basic Usage

```tsx
const options = [
  { label: "Option 1", value: "1" },
  { label: "Option 2", value: "2" },
  { label: "Option 3", value: "3" }
];

<RadioButtons 
  options={options} 
  onChange={(selected) => console.log("Selected:", selected)} 
/>
```

### Different Sizes

```tsx
// Small radio buttons
<RadioButtons 
  size="s"
  options={options} 
/>

// Medium radio buttons (default)
<RadioButtons 
  size="m"
  options={options} 
/>

// Large radio buttons
<RadioButtons 
  size="l"
  options={options} 
/>
```

### With Validation States

```tsx
// Success state
<RadioButtons 
  options={options}
  alertType="success"
/>

// Warning state
<RadioButtons 
  options={options}
  alertType="warning"
/>

// Error state
<RadioButtons 
  options={options}
  alertType="error"
/>
```

### Disabled State

```tsx
<RadioButtons 
  options={options}
  disabled={true}
/>
```

### With Default Selection

```tsx
<RadioButtons 
  options={options}
  defaultVal="2"  // Will select Option 2 by default
/>
```

## Features

- Three size variants: small (s), medium (m), and large (l)
- Support for validation states with appropriate styling
- Disabled state with reduced opacity
- Custom styling support through className props
- Keyboard navigation support
- React Hooks compatibility
- Customizable option labels and values

## Accessibility

The radio button component is built on top of @radix-ui/react-radio-group primitives, ensuring:
- Proper ARIA attributes
- Keyboard navigation support
- Screen reader compatibility
- Focus management

## Design Tokens

The component uses the following design tokens:
- Sizes:
  - Small: `h-gd-16 w-gd-16`
  - Medium: `h-gd-20 w-gd-20`
  - Large: `h-gd-24 w-gd-24`
- Colors:
  - Text: `text-color-text-default`
  - Neutral: `text-color-neutral-grey-80`
  - Border: `border-color-neutral-grey-80`
  - Hover: `border-color-primary-40`
  - Active: `border-color-primary-60`
  - Checked: `border-color-primary-50`