# Radio Button Component

## Overview

The Radio Button component is a form control that allows users to select a single option from a list of choices. Built with Genesis Design System tokens, it provides a comprehensive set of features including multiple size variants, alert states, support text, and extensive customization options. The component is fully accessible and supports keyboard navigation, screen readers, and proper ARIA attributes.

## Component API

### RadioButton Props

| Prop                   | Type                                | Default     | Description                                 |
| ---------------------- | ----------------------------------- | ----------- | ------------------------------------------- |
| size                   | `"s" \| "m" \| "l"`                 | `"m"`       | Size variant of the radio buttons           |
| alertType              | `"success" \| "warning" \| "error"` | `undefined` | Type of alert to display below options      |
| options                | `RadioOption[]`                     | `[]`        | Array of radio options with label and value |
| defaultVal             | `string`                            | `undefined` | Initially selected option value             |
| onChange               | `(value: RadioOption) => void`      | `() => {}`  | Callback when selection changes             |
| containerClassName     | `string`                            | `undefined` | Custom class for the radio group container  |
| optionWrapperClassName | `string`                            | `undefined` | Custom class for each option wrapper        |
| labelClassName         | `string`                            | `undefined` | Custom class for option labels              |
| radioClassName         | `string`                            | `undefined` | Custom class for radio input elements       |
| alertClassName         | `string`                            | `undefined` | Custom class for alert message container    |
| supportClassName       | `string`                            | `undefined` | Custom class for support text container     |
| renderAlert            | `(alertType: string) => ReactNode`  | `undefined` | Custom render function for alert messages   |
| disabled               | `boolean`                           | `false`     | Whether the radio group is disabled         |
| supportText            | `string`                            | `undefined` | Support text to display below options       |

### RadioOption Interface

```typescript
interface RadioOption {
  label: string;
  value: string;
}
```

### Import Statement

```typescript
import { RadioButtons } from "gends";
```

## Basic Usage

### Default Radio Group

```tsx
import { RadioButtons } from "gends";

function MyComponent() {
  const handleChange = selectedOption => {
    console.log("Selected:", selectedOption);
  };

  return (
    <RadioButtons
      options={[
        { label: "Option 1", value: "1" },
        { label: "Option 2", value: "2" },
        { label: "Option 3", value: "3" },
      ]}
      defaultVal="1"
      onChange={handleChange}
    />
  );
}
```

## Variants

### Size Variants

#### Small (s)

```tsx
<RadioButtons
  size="s"
  options={[
    { label: "Small Option 1", value: "1" },
    { label: "Small Option 2", value: "2" },
  ]}
/>
```

#### Medium (m) - Default

```tsx
<RadioButtons
  size="m"
  options={[
    { label: "Medium Option 1", value: "1" },
    { label: "Medium Option 2", value: "2" },
  ]}
/>
```

#### Large (l)

```tsx
<RadioButtons
  size="l"
  options={[
    { label: "Large Option 1", value: "1" },
    { label: "Large Option 2", value: "2" },
  ]}
/>
```

### Alert Variants

#### Success Alert

```tsx
<RadioButtons
  alertType="success"
  options={[
    { label: "Option 1", value: "1" },
    { label: "Option 2", value: "2" },
  ]}
/>
```

#### Warning Alert

```tsx
<RadioButtons
  alertType="warning"
  options={[
    { label: "Option 1", value: "1" },
    { label: "Option 2", value: "2" },
  ]}
/>
```

#### Error Alert

```tsx
<RadioButtons
  alertType="error"
  options={[
    { label: "Option 1", value: "1" },
    { label: "Option 2", value: "2" },
  ]}
/>
```

### Support Text

```tsx
<RadioButtons
  options={[
    { label: "Option 1", value: "1" },
    { label: "Option 2", value: "2" },
  ]}
  supportText="This is additional information about the options"
/>
```

## Advanced Features

### Custom Styling

```tsx
<RadioButtons
  options={[
    { label: "Custom Option 1", value: "1" },
    { label: "Custom Option 2", value: "2" },
  ]}
  containerClassName="bg-gray-50 p-2 rounded-lg shadow-md"
  optionWrapperClassName="border-b border-gray-200 pb-2 mb-2"
  labelClassName="text-gray-700 font-medium"
  radioClassName="border border-gray-400"
  alertClassName="mt-1"
/>
```

### Custom Alert Rendering

```tsx
<RadioButtons
  alertType="success"
  options={[
    { label: "Option 1", value: "1" },
    { label: "Option 2", value: "2" },
  ]}
  renderAlert={type => (
    <div className="flex items-center gap-2">
      <span className="text-sm text-green-600">Custom {type} message</span>
    </div>
  )}
/>
```

### Disabled State

```tsx
<RadioButtons
  options={[
    { label: "Disabled Option 1", value: "1" },
    { label: "Disabled Option 2", value: "2" },
  ]}
  defaultVal="1"
  disabled
/>
```

## Real-World Usage Examples

### Form Integration

```tsx
function FormExample() {
  const [selectedOption, setSelectedOption] = useState(null);

  const handleSubmit = e => {
    e.preventDefault();
    console.log("Selected option:", selectedOption);
  };

  return (
    <form onSubmit={handleSubmit}>
      <RadioButtons
        options={[
          { label: "Yes", value: "yes" },
          { label: "No", value: "no" },
        ]}
        onChange={setSelectedOption}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### Conditional Alert

```tsx
function ConditionalAlertExample() {
  const [selectedOption, setSelectedOption] = useState(null);

  return (
    <RadioButtons
      options={[
        { label: "Option 1", value: "1" },
        { label: "Option 2", value: "2" },
      ]}
      onChange={setSelectedOption}
      alertType={selectedOption?.value === "2" ? "warning" : undefined}
      supportText={
        selectedOption?.value === "2" ? "This option requires additional setup" : undefined
      }
    />
  );
}
```

### Dynamic Options

```tsx
function DynamicOptionsExample() {
  const [options, setOptions] = useState([
    { label: "Option 1", value: "1" },
    { label: "Option 2", value: "2" },
  ]);

  const addOption = () => {
    setOptions([
      ...options,
      { label: `Option ${options.length + 1}`, value: String(options.length + 1) },
    ]);
  };

  return (
    <div>
      <RadioButtons options={options} onChange={option => console.log("Selected:", option)} />
      <button onClick={addOption}>Add Option</button>
    </div>
  );
}
```

## Accessibility Features

### Keyboard Navigation

- **Focus Management**: Proper focus handling for radio options
- **ARIA Attributes**: Appropriate roles and labels
- **Keyboard Shortcuts**: Arrow keys for navigation
- **Focus Indicators**: Clear visual feedback

### Screen Reader Support

- **ARIA Labels**: Clear identification of radio group purpose
- **Live Regions**: Dynamic content updates announced
- **Role Descriptions**: Proper semantic structure

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Focus Indicators**: Clear visual feedback
- **Motion**: Respects reduced motion preferences

## Design System Integration

### Genesis Design Tokens

**Typography:**

- Small: `text-en-desktop-body-m`
- Medium: `text-en-desktop-body-m`
- Large: `text-en-desktop-body-l`

**Spacing:**

- Small: `h-gd-16 w-gd-16`
- Medium: `h-gd-20 w-gd-20`
- Large: `h-gd-24 w-gd-24`

**Colors:**

- Success: `text-color-text-success-subdued`
- Warning: `text-color-text-warning-subdued`
- Error: `text-color-text-error-subdued`

## Best Practices

### Performance

- Use controlled components when needed
- Optimize re-renders
- Handle cleanup properly

### User Experience

- Keep options concise and clear
- Provide meaningful labels
- Consider mobile interactions
- Handle edge cases gracefully

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle errors appropriately

## Troubleshooting

### Common Issues

**Selection:**

- Check value matching
- Verify onChange handling
- Review default values

**Styling:**

- Check custom styles
- Verify design tokens
- Review responsive behavior

**Accessibility:**

- Verify ARIA attributes
- Test keyboard navigation
- Check screen reader support

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Radio Button component provides a flexible and accessible way to handle single-option selection. Choose the appropriate configuration based on your specific use case and requirements.
