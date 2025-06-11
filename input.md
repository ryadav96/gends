# Input

The Input component is a highly configurable and versatile text and number field that supports labels, validation messaging, prefix & suffix icons, character counters, numeric steppers, and much more. Built with accessibility and flexibility in mind, it provides a unified API for all input types while maintaining the ability to handle complex use cases through composable features.

## Overview

The Input component unifies all form input needs into a single, powerful component. Whether you need a simple text field, a complex phone number input with country selection, or a numeric input with stepper controls, the Input component provides all the necessary features through a clean, consistent API.

## API Reference

### Core Props

| Prop            | Type                                                                        | Default     | Description                                                                         |
| --------------- | --------------------------------------------------------------------------- | ----------- | ----------------------------------------------------------------------------------- |
| `label`         | `string`                                                                    | `undefined` | Field label displayed above the input                                               |
| `placeholder`   | `string`                                                                    | `undefined` | Placeholder text shown when the input is empty                                      |
| `size`          | `'s' \| 'm' \| 'l'`                                                         | `'l'`       | Size of the input field affecting height and typography                             |
| `type`          | `'text' \| 'email' \| 'password' \| 'search' \| 'tel' \| 'url' \| 'number'` | `'text'`    | HTML input type - password type automatically adds lock and visibility toggle icons |
| `value`         | `string \| number`                                                          | `undefined` | Controlled value                                                                    |
| `defaultValue`  | `string \| number`                                                          | `undefined` | Default value for uncontrolled usage                                                |
| `onValueChange` | `(value: string \| number) => void`                                         | `undefined` | Callback fired when the input value changes                                         |
| `onChange`      | `(event: React.ChangeEvent<HTMLInputElement>) => void`                      | `undefined` | Standard React onChange handler                                                     |

### Validation Props

| Prop                | Type                                          | Default     | Description                                                   |
| ------------------- | --------------------------------------------- | ----------- | ------------------------------------------------------------- |
| `validationState`   | `'none' \| 'success' \| 'warning' \| 'error'` | `'none'`    | Validation status affecting border color and ring focus state |
| `validationMessage` | `string`                                      | `undefined` | Helper or error message displayed below the input             |
| `required`          | `boolean`                                     | `false`     | Whether the field is required (adds asterisk to label)        |

### Numeric Props

| Prop            | Type                           | Default     | Description                                                                                        |
| --------------- | ------------------------------ | ----------- | -------------------------------------------------------------------------------------------------- |
| `numberVariant` | `'stepper' \| 'split' \| null` | `null`      | Layout variant for number inputs - stepper groups buttons on right, split places them on each side |
| `min`           | `number`                       | `undefined` | Minimum value for number inputs                                                                    |
| `max`           | `number`                       | `undefined` | Maximum value for number inputs                                                                    |
| `step`          | `number`                       | `1`         | Step increment for number inputs                                                                   |

### Icon & Adornment Props

| Prop                | Type                                                     | Default     | Description                                                     |
| ------------------- | -------------------------------------------------------- | ----------- | --------------------------------------------------------------- |
| `prefix`            | `ReactNode`                                              | `undefined` | Custom element displayed before the input content               |
| `suffix`            | `ReactNode`                                              | `undefined` | Custom element displayed after the input content                |
| `showPrefixDivider` | `boolean`                                                | `false`     | Show divider line between prefix and input                      |
| `showSuffixDivider` | `boolean`                                                | `false`     | Show divider line between input and suffix                      |
| `hideClearIcon`     | `boolean`                                                | `false`     | Hide the default clear (×) icon on text inputs                  |
| `allowCopy`         | `boolean`                                                | `false`     | Show copy-to-clipboard icon when input has value                |
| `onCopy`            | `(value: string \| number \| readonly string[]) => void` | `undefined` | Custom copy handler - if not provided, uses navigator.clipboard |

### Counter Props

| Prop          | Type      | Default     | Description                                     |
| ------------- | --------- | ----------- | ----------------------------------------------- |
| `showCounter` | `boolean` | `false`     | Display character counter when maxLength is set |
| `maxLength`   | `number`  | `undefined` | Maximum number of characters allowed            |

### Help Props

| Prop                 | Type         | Default     | Description                                           |
| -------------------- | ------------ | ----------- | ----------------------------------------------------- |
| `showHelpIcon`       | `boolean`    | `false`     | Show help icon next to the label                      |
| `helpTooltipMessage` | `string`     | `undefined` | Tooltip message displayed when hovering the help icon |
| `handleHelpClick`    | `() => void` | `undefined` | Custom click handler for help icon instead of tooltip |

### State Props

| Prop       | Type      | Default | Description                                  |
| ---------- | --------- | ------- | -------------------------------------------- |
| `disabled` | `boolean` | `false` | Disable the input, making it non-interactive |
| `readOnly` | `boolean` | `false` | Make the input read-only                     |

### Styling Props

| Prop                  | Type     | Default     | Description                                       |
| --------------------- | -------- | ----------- | ------------------------------------------------- |
| `className`           | `string` | `undefined` | Custom class name for the root container          |
| `containerClassName`  | `string` | `undefined` | Custom class name for the input container element |
| `inputClassName`      | `string` | `undefined` | Custom class name for the input field element     |
| `labelClassName`      | `string` | `undefined` | Custom class name for the label element           |
| `prefixClassName`     | `string` | `undefined` | Custom class name for the prefix container        |
| `suffixClassName`     | `string` | `undefined` | Custom class name for the suffix container        |
| `validationClassName` | `string` | `undefined` | Custom class name for the validation message      |
| `counterClassName`    | `string` | `undefined` | Custom class name for the character counter       |

## Basic Usage

### Simple Text Input

```tsx
import { Input } from "gends";
import { useState } from "react";

function BasicExample() {
  const [value, setValue] = useState("");

  return (
    <Input
      label="Full Name"
      placeholder="Enter your full name"
      value={value}
      onValueChange={setValue}
    />
  );
}
```

### Email Input with Icon

```tsx
import { Input } from "gends";
import { IcMail } from "gends";

function EmailExample() {
  const [email, setEmail] = useState("");

  return (
    <Input
      label="Email Address"
      type="email"
      placeholder="you@example.com"
      value={email}
      onValueChange={setEmail}
      prefix={<IcMail size="24px" />}
    />
  );
}
```

### Password Input

```tsx
import { Input } from "gends";

function PasswordExample() {
  const [password, setPassword] = useState("");

  return (
    <Input
      label="Password"
      type="password"
      placeholder="Enter password"
      value={password}
      onValueChange={setPassword}
      showHelpIcon
      helpTooltipMessage="Must be at least 8 characters with a number and symbol"
    />
  );
}
```

## Size Variants

The Input component supports three size variants that affect both height and typography:

```tsx
// Small (32px height)
<Input
  size="s"
  label="Small Input"
  placeholder="Size s"
/>

// Medium (40px height) - Default
<Input
  size="m"
  label="Medium Input"
  placeholder="Size m"
/>

// Large (48px height)
<Input
  size="l"
  label="Large Input"
  placeholder="Size l"
/>
```

### Size Specifications

| Size | Height | Text Style | Icon Size | Recommended Use              |
| ---- | ------ | ---------- | --------- | ---------------------------- |
| `s`  | 32px   | `body-m`   | 20px      | Compact forms, table cells   |
| `m`  | 40px   | `body-m`   | 24px      | Standard forms, modals       |
| `l`  | 48px   | `body-l`   | 24px      | Primary forms, landing pages |

## Validation States

The Input component supports four validation states that affect border color, focus ring, and message styling:

```tsx
// Default state
<Input
  label="Default"
  placeholder="No validation state"
  validationMessage="Helper text"
/>

// Success state
<Input
  validationState="success"
  label="Success"
  placeholder="Valid input"
  validationMessage="Looks good!"
/>

// Warning state
<Input
  validationState="warning"
  label="Warning"
  placeholder="Warning input"
  validationMessage="Please double-check this value"
/>

// Error state
<Input
  validationState="error"
  label="Error"
  placeholder="Invalid input"
  validationMessage="This field is required"
/>
```

### Validation State Colors

| State     | Border Color               | Focus Ring                 | Message Color              |
| --------- | -------------------------- | -------------------------- | -------------------------- |
| `none`    | `--gd-neutral-grey-40`     | `--gd-primary-60`          | `--gd-neutral-grey-60`     |
| `success` | `--gd-feedback-success-50` | `--gd-feedback-success-50` | `--gd-feedback-success-50` |
| `warning` | `--gd-feedback-warning-50` | `--gd-feedback-warning-50` | `--gd-feedback-warning-50` |
| `error`   | `--gd-feedback-error-50`   | `--gd-feedback-error-50`   | `--gd-feedback-error-50`   |

## Icons and Adornments

### Prefix and Suffix Icons

```tsx
import { IcSearch, IcMail, IcSettings } from "gends";

// Search with prefix icon
<Input
  label="Search"
  placeholder="Search..."
  prefix={<IcSearch size="24px" />}
/>

// Email with both prefix and suffix
<Input
  label="Email"
  type="email"
  placeholder="you@example.com"
  prefix={<IcMail size="24px" />}
  suffix={<IcSettings size="24px" />}
/>

// With dividers
<Input
  label="Advanced Search"
  placeholder="Enter query"
  prefix={<IcSearch size="24px" />}
  suffix={<IcSettings size="24px" />}
  showPrefixDivider
  showSuffixDivider
/>
```

### Copy to Clipboard

```tsx
function CopyableInput() {
  const [value, setValue] = useState("Copy this text!");

  const handleCopy = copiedValue => {
    console.log("Copied:", copiedValue);
    // Custom copy logic or just use default clipboard API
  };

  return (
    <Input
      label="API Key"
      value={value}
      onValueChange={setValue}
      allowCopy
      onCopy={handleCopy}
      hideClearIcon // Hide clear icon when copy is primary action
    />
  );
}
```

### Password Field Features

Password fields automatically include:

- Lock icon as prefix (can be overridden)
- Eye/eye-off toggle for visibility (can be overridden)
- Proper security attributes

```tsx
// Default password field
<Input
  label="Password"
  type="password"
  placeholder="Enter password"
/>

// Password with custom prefix (overrides default lock icon)
<Input
  label="Custom Password"
  type="password"
  placeholder="Enter password"
  prefix={<IcLock size="24px" />}
/>
```

## Numeric Inputs

### Basic Number Input

```tsx
<Input label="Age" type="number" min={0} max={120} step={1} placeholder="Enter age" />
```

### Number Variants

#### Stepper Variant

Groups increment/decrement buttons on the right side:

```tsx
<Input
  label="Quantity"
  type="number"
  numberVariant="stepper"
  min={0}
  max={10}
  step={1}
  placeholder="Qty"
/>
```

#### Split Variant

Places decrement button on the left and increment button on the right:

```tsx
<Input
  label="Quantity"
  type="number"
  numberVariant="split"
  min={0}
  max={10}
  step={1}
  placeholder="Qty"
/>
```

### Decimal Numbers

```tsx
<Input
  label="Price"
  type="number"
  step={0.01}
  min={0}
  placeholder="0.00"
  validationMessage="Enter price in dollars"
/>
```

### Numeric Limits

When values reach min/max limits, the corresponding buttons are automatically disabled:

```tsx
// At minimum value (0) - decrement button disabled
<Input
  label="At Minimum"
  type="number"
  value={0}
  min={0}
  max={5}
  step={1}
/>

// At maximum value (5) - increment button disabled
<Input
  label="At Maximum"
  type="number"
  value={5}
  min={0}
  max={5}
  step={1}
/>
```

## Character Counter

Display live character count when `maxLength` is specified:

```tsx
<Input
  label="Username"
  placeholder="Choose a username"
  maxLength={20}
  showCounter
  validationMessage="Username must be unique"
/>
```

The counter shows as "current/max" (e.g., "5/20") and updates in real-time as the user types.

## Help and Tooltips

### Help Icon with Tooltip

```tsx
<Input
  label="Password"
  type="password"
  showHelpIcon
  helpTooltipMessage="Password must be at least 8 characters and contain at least one number and one special character"
/>
```

### Custom Help Click Handler

```tsx
function InputWithCustomHelp() {
  const handleHelpClick = () => {
    // Open modal, navigate to help page, etc.
    console.log("Help clicked");
  };

  return <Input label="Complex Field" showHelpIcon handleHelpClick={handleHelpClick} />;
}
```

## State Variants

### Disabled State

```tsx
<Input
  label="Disabled Field"
  value="Cannot edit this"
  disabled
  placeholder="This field is disabled"
/>
```

Disabled inputs:

- Have reduced opacity
- Show `cursor: not-allowed`
- Are not focusable
- Cannot be interacted with

### Read-Only State

```tsx
<Input
  label="Read-Only Field"
  value="This is read-only"
  readOnly
  placeholder="Cannot edit but can copy"
/>
```

Read-only inputs:

- Maintain full visual clarity
- Can be focused and selected
- Allow text selection and copying
- Cannot be edited

## Advanced Examples

### Phone Number with Country Code

```tsx
import { Dropdown } from "gends";
import { CircleFlag } from "react-circle-flags";

function PhoneNumberInput() {
  const [selectedCountry, setSelectedCountry] = useState({
    id: "US",
    value: "US",
    label: "US +1",
    isoCode: "US",
    dialCode: "+1",
  });

  const [phoneNumber, setPhoneNumber] = useState("");

  const countries = [
    { id: "US", value: "US", label: "US +1", isoCode: "US", dialCode: "+1" },
    { id: "GB", value: "GB", label: "GB +44", isoCode: "GB", dialCode: "+44" },
    { id: "IN", value: "IN", label: "IN +91", isoCode: "IN", dialCode: "+91" },
    // ... more countries
  ];

  return (
    <Input
      label="Phone Number"
      type="tel"
      placeholder="Enter phone number"
      value={phoneNumber}
      onValueChange={setPhoneNumber}
      showPrefixDivider
      prefix={
        <div className="w-[100px]">
          <Dropdown
            options={countries}
            value={selectedCountry ? [selectedCountry] : []}
            onChange={selected => {
              if (selected?.[0]) {
                setSelectedCountry(selected[0]);
              }
            }}
            size="m"
            hideFooterActions
          >
            <div className="flex items-center gap-2 justify-between">
              <div className="flex items-center gap-2">
                <CircleFlag
                  countryCode={selectedCountry.isoCode.toLowerCase()}
                  height={24}
                  width={24}
                />
                <Text variant="desktop-body-l">{selectedCountry.dialCode}</Text>
              </div>
              <IcChevronDown size="24px" />
            </div>
          </Dropdown>
        </div>
      }
    />
  );
}
```

### Measurement Input with Units

```tsx
import { IcRuler } from "gends";

function MeasurementInput() {
  const [value, setValue] = useState("");
  const [unit, setUnit] = useState("cm");

  return (
    <Input
      label="Height"
      type="number"
      placeholder="Enter measurement"
      value={value}
      onValueChange={setValue}
      prefix={<IcRuler size="24px" />}
      suffix={
        <select
          value={unit}
          onChange={e => setUnit(e.target.value)}
          className="border-none bg-transparent outline-none"
        >
          <option value="cm">cm</option>
          <option value="in">in</option>
          <option value="ft">ft</option>
        </select>
      }
      showSuffixDivider
    />
  );
}
```

### Currency Input

```tsx
function CurrencyInput() {
  const [amount, setAmount] = useState("");
  const [currency, setCurrency] = useState("USD");

  return (
    <Input
      label="Amount"
      type="number"
      step={0.01}
      placeholder="0.00"
      value={amount}
      onValueChange={setAmount}
      prefix={
        <select
          value={currency}
          onChange={e => setCurrency(e.target.value)}
          className="border-none bg-transparent outline-none"
        >
          <option value="USD">USD</option>
          <option value="EUR">EUR</option>
          <option value="GBP">GBP</option>
        </select>
      }
      showPrefixDivider
      validationMessage="Enter amount in selected currency"
    />
  );
}
```

### Input with Action Buttons

```tsx
import { Button } from "gends";

function InputWithActions() {
  const [value, setValue] = useState("");

  const handleApply = () => {
    console.log("Applied:", value);
  };

  const handleSync = () => {
    console.log("Syncing...");
  };

  return (
    <Input
      label="Configuration Value"
      placeholder="Enter value"
      value={value}
      onValueChange={setValue}
      suffix={
        <div className="flex gap-2">
          <Button size="s" variant="outline" onClick={handleSync}>
            Sync
          </Button>
          <Button size="s" onClick={handleApply}>
            Apply
          </Button>
        </div>
      }
    />
  );
}
```

## Form Integration

### React Hook Form

```tsx
import { useForm, Controller } from "react-hook-form";
import { Input } from "gends";

function FormExample() {
  const { control, handleSubmit } = useForm({
    defaultValues: {
      email: "",
      password: "",
      age: 0,
    },
  });

  const onSubmit = data => {
    console.log("Form data:", data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <Controller
        name="email"
        control={control}
        rules={{ required: "Email is required" }}
        render={({ field, fieldState }) => (
          <Input
            {...field}
            label="Email"
            type="email"
            placeholder="you@example.com"
            validationState={fieldState.error ? "error" : "none"}
            validationMessage={fieldState.error?.message}
            prefix={<IcMail size="24px" />}
          />
        )}
      />

      <Controller
        name="password"
        control={control}
        rules={{
          required: "Password is required",
          minLength: { value: 8, message: "Password must be at least 8 characters" },
        }}
        render={({ field, fieldState }) => (
          <Input
            {...field}
            label="Password"
            type="password"
            validationState={fieldState.error ? "error" : "none"}
            validationMessage={fieldState.error?.message}
            showHelpIcon
            helpTooltipMessage="Password must be at least 8 characters"
          />
        )}
      />

      <Controller
        name="age"
        control={control}
        rules={{
          required: "Age is required",
          min: { value: 18, message: "Must be at least 18 years old" },
        }}
        render={({ field, fieldState }) => (
          <Input
            {...field}
            label="Age"
            type="number"
            min={0}
            max={120}
            validationState={fieldState.error ? "error" : "none"}
            validationMessage={fieldState.error?.message}
          />
        )}
      />

      <Button type="submit">Submit</Button>
    </form>
  );
}
```

### Uncontrolled Usage

```tsx
import { useRef } from "react";

function UncontrolledExample() {
  const inputRef = useRef<HTMLInputElement>(null);

  const handleSubmit = () => {
    const value = inputRef.current?.value;
    console.log("Input value:", value);
  };

  return (
    <div>
      <Input
        ref={inputRef}
        label="Uncontrolled Input"
        defaultValue="Initial value"
        placeholder="Type here..."
        onValueChange={value => {
          console.log("Value changed:", value);
        }}
      />
      <Button onClick={handleSubmit}>Get Value</Button>
    </div>
  );
}
```

## Accessibility Features

The Input component includes comprehensive accessibility support:

### Keyboard Navigation

- **Tab**: Focus the input field
- **Shift + Tab**: Focus previous element
- **Enter**: Submit form (if inside form)
- **Escape**: Clear field (when clear icon is visible)
- **Arrow Up/Down**: Increment/decrement numeric values (when focused)
- **Arrow Keys**: Navigate help tooltips

### Screen Reader Support

- Proper labeling with `htmlFor` associations
- ARIA attributes for validation states
- Descriptive error messages linked with `aria-describedby`
- Button labels for icon-only actions (copy, clear, visibility toggle)
- Live regions for dynamic content updates

### Focus Management

- Clear focus indicators with appropriate color contrast
- Focus ring uses validation state colors
- Logical tab order through prefix, input, and suffix elements
- Focus preservation during state changes

```tsx
// Example with full accessibility features
<Input
  label="Accessible Input"
  placeholder="Type here"
  validationState="error"
  validationMessage="This field is required"
  showHelpIcon
  helpTooltipMessage="Enter a valid email address"
  required
  aria-label="Email address input with validation"
  aria-describedby="email-help email-error"
/>
```

## Styling and Customization

### CSS Custom Properties

The Input component uses Genesis Design System tokens:

```css
/* Color tokens */
--gd-primary-60              /* Focus ring and active states */
--gd-neutral-grey-40         /* Default border */
--gd-neutral-grey-60         /* Placeholder text */
--gd-neutral-grey-80         /* Input text */
--gd-feedback-success-50     /* Success state */
--gd-feedback-warning-50     /* Warning state */
--gd-feedback-error-50       /* Error state */

/* Spacing tokens */
--gd-4                       /* Gap between elements */
--gd-8, --gd-12              /* Internal padding */
--gd-32, --gd-40, --gd-48    /* Component heights */
```

### Custom Styling

```tsx
// Custom input with styled components
<Input
  label="Custom Styled Input"
  placeholder="Styled placeholder"
  className="my-custom-input"
  containerClassName="custom-container"
  inputClassName="custom-input-field"
  labelClassName="custom-label"
  prefix={<IcMail className="text-blue-500" size="24px" />}
  prefixClassName="custom-prefix"
/>
```

```css
/* Custom styles */
.my-custom-input {
  /* Root container styles */
}

.custom-container {
  /* Input container styles */
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.custom-input-field {
  /* Input field styles */
  font-family: "Custom Font", sans-serif;
}

.custom-label {
  /* Label styles */
  font-weight: 600;
  color: #333;
}

.custom-prefix {
  /* Prefix container styles */
  background: #f5f5f5;
  border-radius: 4px;
}
```

## Performance Considerations

### Controlled vs Uncontrolled

```tsx
// Controlled - re-renders on every change
function ControlledInput() {
  const [value, setValue] = useState("");

  return <Input value={value} onValueChange={setValue} label="Controlled" />;
}

// Uncontrolled - better performance for simple cases
function UncontrolledInput() {
  return (
    <Input
      defaultValue=""
      onValueChange={value => {
        // Only fires when you need to react to changes
        console.log("Changed:", value);
      }}
      label="Uncontrolled"
    />
  );
}
```

### Debounced Input

```tsx
import { useMemo } from "react";
import { debounce } from "lodash";

function DebouncedInput() {
  const [value, setValue] = useState("");
  const [debouncedValue, setDebouncedValue] = useState("");

  const debouncedSetValue = useMemo(
    () =>
      debounce((val: string) => {
        setDebouncedValue(val);
        // Expensive operation here
      }, 300),
    []
  );

  const handleChange = (newValue: string) => {
    setValue(newValue); // Immediate UI update
    debouncedSetValue(newValue); // Debounced side effect
  };

  return (
    <Input
      label="Search"
      value={value}
      onValueChange={handleChange}
      placeholder="Type to search..."
    />
  );
}
```

## Common Patterns

### Search Input

```tsx
function SearchInput() {
  const [query, setQuery] = useState("");

  return (
    <Input
      label="Search"
      type="search"
      placeholder="Search products..."
      value={query}
      onValueChange={setQuery}
      prefix={<IcSearch size="24px" />}
      allowCopy
      size="l"
    />
  );
}
```

### Required Field Indicator

```tsx
function RequiredInput() {
  return (
    <Input
      label="Email Address"
      type="email"
      required
      placeholder="you@example.com"
      validationMessage="This field is required"
      showHelpIcon
      helpTooltipMessage="We'll use this to send you important updates"
    />
  );
}
```

### Multi-Step Validation

```tsx
function ValidatedInput() {
  const [value, setValue] = useState("");
  const [validationState, setValidationState] = useState<ValidationState>("none");
  const [message, setMessage] = useState("");

  const validateEmail = (email: string) => {
    if (!email) {
      setValidationState("none");
      setMessage("Enter your email address");
      return;
    }

    if (!email.includes("@")) {
      setValidationState("error");
      setMessage("Please enter a valid email address");
      return;
    }

    if (email.endsWith("@gmail.com")) {
      setValidationState("warning");
      setMessage("Consider using your work email");
      return;
    }

    setValidationState("success");
    setMessage("Email looks good!");
  };

  const handleChange = (newValue: string) => {
    setValue(newValue);
    validateEmail(newValue);
  };

  return (
    <Input
      label="Work Email"
      type="email"
      value={value}
      onValueChange={handleChange}
      validationState={validationState}
      validationMessage={message}
      prefix={<IcMail size="24px" />}
    />
  );
}
```

## Migration Guide

### From Native HTML Input

```tsx
// Before: Native HTML input
<div>
  <label htmlFor="email">Email</label>
  <input
    id="email"
    type="email"
    placeholder="you@example.com"
    onChange={(e) => setValue(e.target.value)}
  />
</div>

// After: Genesis Input
<Input
  label="Email"
  type="email"
  placeholder="you@example.com"
  onValueChange={setValue}
/>
```

### From Other Component Libraries

```tsx
// Before: Material-UI TextField
<TextField
  label="Email"
  variant="outlined"
  error={hasError}
  helperText={errorMessage}
  InputProps={{
    startAdornment: <IcMail />
  }}
/>

// After: Genesis Input
<Input
  label="Email"
  validationState={hasError ? "error" : "none"}
  validationMessage={errorMessage}
  prefix={<IcMail size="24px" />}
/>
```

### Legacy Props Mapping

| Legacy Prop      | Genesis Input Prop        | Notes                           |
| ---------------- | ------------------------- | ------------------------------- |
| `error`          | `validationState="error"` | Use validation state enum       |
| `helperText`     | `validationMessage`       | Supports all validation states  |
| `startAdornment` | `prefix`                  | More flexible ReactNode support |
| `endAdornment`   | `suffix`                  | More flexible ReactNode support |
| `variant`        | `size`                    | Different sizing approach       |
| `InputProps`     | Various className props   | More granular styling control   |

## Troubleshooting

### Common Issues

**Input not responding to value changes**

```tsx
// ❌ Problem: Missing onValueChange or onChange
<Input value={value} />

// ✅ Solution: Provide change handler
<Input value={value} onValueChange={setValue} />
```

**Icons not properly sized**

```tsx
// ❌ Problem: Inconsistent icon sizes
<Input prefix={<IcMail />} size="s" />

// ✅ Solution: Match icon size to input size
<Input
  prefix={<IcMail size="20px" />}
  size="s"
/>
```

**Clear icon not appearing**

```tsx
// ❌ Problem: Clear icon hidden
<Input hideClearIcon />

// ✅ Solution: Enable clear icon for text inputs
<Input
  type="text"
  hideClearIcon={false}
/>
```

**Number buttons not working**

```tsx
// ❌ Problem: No number variant specified
<Input type="number" />

// ✅ Solution: Specify number variant
<Input
  type="number"
  numberVariant="stepper"
/>
```

### Debug Helpers

```tsx
// Debug input state
function DebugInput() {
  const [value, setValue] = useState("");

  return (
    <div>
      <Input
        label="Debug Input"
        value={value}
        onValueChange={val => {
          console.log("Value changed:", val, typeof val);
          setValue(val);
        }}
        onChange={e => {
          console.log("Raw event:", e.target.value);
        }}
      />
      <pre>Current value: {JSON.stringify(value)}</pre>
    </div>
  );
}
```

## Best Practices

### Do's ✅

- Use semantic input types (`email`, `tel`, `url`, etc.)
- Provide clear, descriptive labels
- Include helpful validation messages
- Use appropriate size for context
- Implement proper error handling
- Test with keyboard navigation
- Provide loading states for async validation
- Use debouncing for expensive operations
- Follow accessibility guidelines

### Don'ts ❌

- Don't use placeholder as the primary label
- Don't make required fields without clear indication
- Don't use cryptic error messages
- Don't forget to handle edge cases (empty, null values)
- Don't ignore keyboard users
- Don't use inconsistent validation patterns
- Don't overcomplicate simple inputs
- Don't forget to test with screen readers

## Related Components

- **[TextArea](./textarea.md)** - Multi-line text input
- **[Dropdown](./dropdown.md)** - Selection input for options
- **[Button](./button.md)** - Action triggers for forms
- **[Checkbox](./checkbox.md)** - Boolean input selections
- **[Radio Button](./radio-button.md)** - Single choice selections
- **[Date Picker](./date-picker.md)** - Date and time inputs
- **[File Uploader](./file-uploader.md)** - File selection input
