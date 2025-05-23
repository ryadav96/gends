# Input Label

A flexible and reusable label component designed for form inputs with support for required indicators, help tooltips, and character counters.

## Features

- Label text with optional required indicator
- Tooltip help icon with customizable message
- Character counter support
- Flexible styling options
- Accessibility-friendly

## Installation

```tsx
import { InputLabel } from 'gends';
```

## Usage

### Basic Label

```tsx
<InputLabel 
  htmlFor="email-input"
  label="Email Address"
/>
```

### Required Field Label

```tsx
<InputLabel 
  htmlFor="email-input"
  label="Email Address"
  required={true}
/>
```

### Label with Help Icon

```tsx
<InputLabel 
  htmlFor="password-input"
  label="Password"
  required={true}
  showHelpIcon={true}
  helpTooltipMessage="Password must be at least 8 characters long"
/>
```

### Label with Character Counter

```tsx
<InputLabel 
  htmlFor="description-input"
  label="Description"
  showCounter={true}
  currentCount={50}
  maxCount={100}
/>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| htmlFor | string | required | ID of the input element this label is tied to |
| label | string | required | The text content of the label |
| required | boolean | false | Whether to show a required field indicator (*) |
| showHelpIcon | boolean | false | Whether to show the help icon |
| helpTooltipMessage | string | undefined | Content to show in the help tooltip |
| handleHelpClick | () => void | undefined | Callback when help icon is clicked |
| className | string | undefined | Additional CSS classes to apply to the label container |
| showCounter | boolean | false | Whether to show the character counter |
| currentCount | number | 0 | Current character count |
| maxCount | number | undefined | Maximum character count |

## Examples

### Basic Required Field

```tsx
<InputLabel
  htmlFor="name"
  label="Full Name"
  required={true}
/>
```

### With Help Icon and Tooltip

```tsx
<InputLabel
  htmlFor="password"
  label="Password"
  required={true}
  showHelpIcon={true}
  helpTooltipMessage="Password must contain at least 8 characters, including uppercase, lowercase, numbers and special characters"
/>
```

### With Character Counter

```tsx
<InputLabel
  htmlFor="bio"
  label="Bio"
  showCounter={true}
  currentCount={50}
  maxCount={200}
/>
```

### Full Featured Example

```tsx
<InputLabel
  htmlFor="description"
  label="Description"
  required={true}
  showHelpIcon={true}
  helpTooltipMessage="Provide a detailed description of your product"
  showCounter={true}
  currentCount={75}
  maxCount={500}
  className="w-full"
/>
```

## Styling

The InputLabel component uses Tailwind CSS classes for styling and can be customized using the `className` prop. The default styling includes:

- Flex container layout
- Gap between elements
- Proper text color for labels and required indicators
- Hover effects for the help icon
- Right-aligned character counter

## Accessibility

The InputLabel component follows accessibility best practices:

- Uses semantic HTML `<label>` elements
- Properly associates labels with form controls using `htmlFor`
- Provides tooltip content for help icons
- Uses ARIA attributes where appropriate

## Best Practices

1. Always provide a meaningful `htmlFor` attribute that matches the ID of the input it labels
2. Use clear and concise label text
3. Only mark fields as required when they are truly mandatory
4. Provide helpful tooltip content that adds value beyond the label text
5. Use character counters for fields with specific length requirements