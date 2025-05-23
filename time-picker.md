# Time Picker

A flexible time picker component that supports both 12-hour and 24-hour formats with validation states and various styling options.

## Features

- 12-hour and 24-hour time format support
- Three size variants (small, medium, large)
- Validation states with customizable messages
- Tooltip support
- Required field support
- Auto-close timer
- Support text
- Disabled state
- Customizable styling

## Installation

```tsx
import { TimePicker } from 'gends';
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| label | string | - | Label text for the time picker |
| required | boolean | false | Makes the time picker required |
| value | string | - | Current time value (format: "HH:MM AM/PM") |
| time24Format | boolean | false | Use 24-hour time format |
| validationState | `"error" \| "warning" \| "success" \| "default"` | `"default"` | Sets the validation state |
| placeholder | string | "HH:MM" | Placeholder text |
| helperText | string | - | Tooltip helper text |
| size | `"s" \| "m" \| "l"` | `"m"` | Size of the time picker |
| disabled | boolean | false | Disables the time picker |
| validationMessage | string | - | Validation message to display |
| onChange | `(time: string) => void` | - | Callback when time changes |
| tooltipText | string | - | Text to show in the tooltip |
| supportText | string | - | Additional support text below the picker |
| autoCloseTimer | number | 0 | Auto-close delay in milliseconds |

## Examples

### Basic Time Picker

```tsx
<TimePicker 
  label="Select Time"
  placeholder="HH:MM"
  onChange={(time) => console.log('Selected time:', time)}
/>
```

### With 24-Hour Format

```tsx
<TimePicker 
  label="Select Time (24h)"
  time24Format={true}
  placeholder="HH:MM"
  tooltipText="Enter time in 24-hour format"
/>
```

### With Validation

```tsx
<TimePicker 
  label="Appointment Time"
  required={true}
  validationState="error"
  validationMessage="Please select a valid time"
  helperText="Business hours: 9 AM to 5 PM"
/>
```

### Different Sizes

```tsx
// Small
<TimePicker size="s" label="Small" />

// Medium (default)
<TimePicker size="m" label="Medium" />

// Large
<TimePicker size="l" label="Large" />
```

### With Support Text

```tsx
<TimePicker 
  label="Meeting Time"
  supportText="All times are in your local timezone"
  tooltipText="Click to select meeting time"
/>
```

### Disabled State

```tsx
<TimePicker 
  label="Closed Hours"
  disabled={true}
  value="10:00 PM"
  helperText="Time selection not available"
/>
```

### With Auto-close Timer

```tsx
<TimePicker 
  label="Quick Select"
  autoCloseTimer={3000}
  tooltipText="Selection will auto-confirm after 3 seconds"
/>
```

## Styling

The TimePicker component can be customized using the classNames prop which accepts:

```tsx
classNames?: {
  containerclass?: string;
  toolTipTriggerClass?: string;
  toolTipContentClass?: string;
  selectorContainerClass?: string;
  selectorItemClass?: string;
}
```

## Best Practices

1. Always provide a clear label that indicates what the time is being selected for
2. Use tooltipText to provide additional context when needed
3. Choose appropriate size based on the form context
4. Include validation messages that clearly explain any time restrictions
5. Use 24-hour format when working in professional or international contexts
6. Consider timezone implications and communicate them via support text
7. Ensure the component is keyboard accessible for better usability
8. Match the time format (12/24h) with your users' preferences