# Checkbox Component

The Checkbox component is a form control that allows users to select one or multiple options. It supports different sizes, states, and validation messages.

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | `"s" \| "m" \| "l"` | `"m"` | Controls the size of the checkbox |
| validationState | `"warning" \| "error" \| "success" \| undefined` | `undefined` | Sets the validation state with appropriate styling and icon |
| validationMessage | `string` | `"Alert Text"` | Message displayed when validation state is set |
| label | `string` | `""` | Text label displayed next to the checkbox |
| indeterminate | `boolean` | `false` | Shows an indeterminate state (dash instead of checkmark) |
| disabled | `boolean` | `false` | Disables the checkbox |
| defaultChecked | `boolean` | `false` | Sets the initial checked state |
| onChange | `(checked: boolean) => void` | `undefined` | Callback function triggered when checkbox state changes |

## Examples

### Basic Usage

```tsx
<Checkbox label="Accept terms and conditions" />
```

### Different Sizes

```tsx
// Small checkbox
<Checkbox size="s" label="Small checkbox" />

// Medium checkbox (default)
<Checkbox size="m" label="Medium checkbox" />

// Large checkbox
<Checkbox size="l" label="Large checkbox" />
```

### Validation States

```tsx
// Success state
<Checkbox 
  label="Valid selection"
  validationState="success"
  validationMessage="Selection confirmed"
/>

// Warning state
<Checkbox 
  label="Review needed"
  validationState="warning"
  validationMessage="Please review this selection"
/>

// Error state
<Checkbox 
  label="Invalid selection"
  validationState="error"
  validationMessage="This selection is invalid"
/>
```

### Indeterminate State

```tsx
<Checkbox 
  label="Select all items"
  indeterminate={true}
/>
```

### Disabled States

```tsx
// Disabled unchecked
<Checkbox 
  label="Disabled checkbox"
  disabled={true}
/>

// Disabled checked
<Checkbox 
  label="Disabled and checked"
  disabled={true}
  defaultChecked={true}
/>

// Disabled indeterminate
<Checkbox 
  label="Disabled and indeterminate"
  disabled={true}
  indeterminate={true}
/>
```

## Features

- Three size variants: small (s), medium (m), and large (l)
- Support for validation states with customizable messages
- Indeterminate state support
- Disabled state styling
- Hover and focus states
- Accessible through keyboard navigation
- Custom styling support through className prop
- React Hooks compatibility

## Accessibility

The checkbox component is built on top of @radix-ui/react-checkbox primitives, ensuring proper accessibility features:
- Supports keyboard navigation
- Proper ARIA attributes
- Focus management
- Screen reader compatibility

## Design Tokens

The component uses the following design tokens:
- Border radius: `rounded-checkbox`
- Spacing: `gap-gd-4`, `gap-gd-8`, `gap-gd-16`
- Colors:
  - Primary: `color-primary-40`, `color-primary-50`, `color-primary-60`
  - Text: `color-text-default`
  - Neutral: `color-neutral-grey-80`