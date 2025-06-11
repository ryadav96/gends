# Checkbox Component

## Overview

The Checkbox component is a versatile form control that allows users to select one or multiple options from a set. Built on Radix UI primitives with Genesis Design System tokens, it provides comprehensive functionality including multiple sizes, validation states, indeterminate support, and extensive accessibility features. The component handles both controlled and uncontrolled patterns for maximum flexibility.

## Component API

### Checkbox Props

| Prop                | Type                                             | Default        | Description                                               |
| ------------------- | ------------------------------------------------ | -------------- | --------------------------------------------------------- |
| `label`             | `string`                                         | Required       | Text label displayed next to the checkbox                 |
| `size`              | `'s' \| 'm' \| 'l'`                              | `'m'`          | Size variant affecting checkbox and text dimensions       |
| `validationState`   | `'success' \| 'warning' \| 'error' \| undefined` | `undefined`    | Validation state with appropriate styling and icon        |
| `validationMessage` | `string`                                         | `'Alert Text'` | Message displayed when validation state is set            |
| `indeterminate`     | `boolean`                                        | `false`        | Shows indeterminate state (dash instead of checkmark)     |
| `disabled`          | `boolean`                                        | `false`        | Disables the checkbox and applies disabled styling        |
| `defaultChecked`    | `boolean`                                        | `false`        | Sets the initial checked state for uncontrolled usage     |
| `onChange`          | `(checked: boolean) => void`                     | `undefined`    | Callback function triggered when checkbox state changes   |
| `className`         | `string`                                         | `undefined`    | Additional CSS classes to apply to the checkbox container |

### Extended Props

The component also accepts all standard Radix UI Checkbox props for advanced customization.

## Basic Usage

### Import

```tsx
import { Checkbox } from "gends";
```

### Simple Checkbox

```tsx
const BasicCheckbox = () => {
  return <Checkbox label="Accept terms and conditions" />;
};
```

### Controlled Checkbox

```tsx
const ControlledCheckbox = () => {
  const [isChecked, setIsChecked] = useState(false);

  return (
    <Checkbox label="Enable notifications" defaultChecked={isChecked} onChange={setIsChecked} />
  );
};
```

### Uncontrolled Checkbox

```tsx
const UncontrolledCheckbox = () => {
  return (
    <Checkbox
      label="Remember my preferences"
      defaultChecked={true}
      onChange={checked => console.log("Checkbox state:", checked)}
    />
  );
};
```

## Size Variants

The Checkbox component supports three size variants with different dimensions and text styles:

### Size Specifications

| Size | Checkbox Size | Icon Size | Text Style     | Use Case              |
| ---- | ------------- | --------- | -------------- | --------------------- |
| `s`  | 16px × 16px   | 12px      | desktop-body-m | Compact forms, tables |
| `m`  | 20px × 20px   | 12px      | desktop-body-m | Standard forms        |
| `l`  | 24px × 24px   | 16px      | desktop-body-l | Prominent selections  |

### Size Examples

```tsx
// Small checkbox - compact interfaces
<Checkbox
  size="s"
  label="Small checkbox for compact layouts"
/>

// Medium checkbox - default size
<Checkbox
  size="m"
  label="Medium checkbox for standard forms"
/>

// Large checkbox - prominent displays
<Checkbox
  size="l"
  label="Large checkbox for important selections"
/>
```

### Size Comparison

```tsx
const SizeComparison = () => (
  <div className="flex flex-col gap-4">
    <Checkbox size="s" label="Small (16px)" />
    <Checkbox size="m" label="Medium (20px)" />
    <Checkbox size="l" label="Large (24px)" />
  </div>
);
```

## Validation States

The Checkbox component supports three validation states with corresponding colors, icons, and messages:

### Validation State Specifications

| State     | Color  | Icon             | Use Case                       |
| --------- | ------ | ---------------- | ------------------------------ |
| `success` | Green  | IcSuccessColored | Confirmed selections           |
| `warning` | Orange | IcWarningColored | Selections needing review      |
| `error`   | Red    | IcErrorColored   | Invalid or required selections |

### Success State

```tsx
// Success validation
<Checkbox
  label="Data processing consent"
  validationState="success"
  validationMessage="Consent successfully recorded"
/>

// Success with large size
<Checkbox
  size="l"
  label="Account verification complete"
  validationState="success"
  validationMessage="Your account has been verified"
/>
```

### Warning State

```tsx
// Warning validation
<Checkbox
  label="Beta feature opt-in"
  validationState="warning"
  validationMessage="This feature is experimental"
/>

// Warning with custom message
<Checkbox
  label="External service integration"
  validationState="warning"
  validationMessage="Please review the privacy implications"
/>
```

### Error State

```tsx
// Error validation
<Checkbox
  label="Terms and conditions"
  validationState="error"
  validationMessage="You must accept the terms to continue"
/>

// Error with long message
<Checkbox
  label="Required field"
  validationState="error"
  validationMessage="This selection is required to complete your registration"
/>
```

### Validation Examples by Size

```tsx
const ValidationBySize = () => (
  <div className="flex flex-col gap-6">
    {/* Small size with validation */}
    <div className="space-y-3">
      <h3>Small Size Validation</h3>
      <Checkbox
        size="s"
        label="Small success"
        validationState="success"
        validationMessage="Small success message"
      />
      <Checkbox
        size="s"
        label="Small warning"
        validationState="warning"
        validationMessage="Small warning message"
      />
      <Checkbox
        size="s"
        label="Small error"
        validationState="error"
        validationMessage="Small error message"
      />
    </div>

    {/* Large size with validation */}
    <div className="space-y-3">
      <h3>Large Size Validation</h3>
      <Checkbox
        size="l"
        label="Large success"
        validationState="success"
        validationMessage="Large success message"
      />
      <Checkbox
        size="l"
        label="Large warning"
        validationState="warning"
        validationMessage="Large warning message"
      />
      <Checkbox
        size="l"
        label="Large error"
        validationState="error"
        validationMessage="Large error message"
      />
    </div>
  </div>
);
```

## Indeterminate State

The indeterminate state is useful for hierarchical selections or "select all" functionality:

### Basic Indeterminate

```tsx
// Basic indeterminate state
<Checkbox
  label="Select all items"
  indeterminate={true}
/>

// Indeterminate with validation
<Checkbox
  label="Partial selection"
  indeterminate={true}
  validationState="warning"
  validationMessage="Some items are selected"
/>
```

### Indeterminate Sizes

```tsx
const IndeterminateSizes = () => (
  <div className="flex flex-col gap-4">
    <Checkbox size="s" label="Small indeterminate" indeterminate={true} />
    <Checkbox size="m" label="Medium indeterminate" indeterminate={true} />
    <Checkbox size="l" label="Large indeterminate" indeterminate={true} />
  </div>
);
```

### Hierarchical Selection Example

```tsx
const HierarchicalSelection = () => {
  const [items, setItems] = useState([
    { id: 1, label: "Item 1", checked: false },
    { id: 2, label: "Item 2", checked: true },
    { id: 3, label: "Item 3", checked: false },
  ]);

  const checkedCount = items.filter(item => item.checked).length;
  const isAllChecked = checkedCount === items.length;
  const isIndeterminate = checkedCount > 0 && checkedCount < items.length;

  const handleSelectAll = checked => {
    setItems(items.map(item => ({ ...item, checked })));
  };

  const handleItemChange = (id, checked) => {
    setItems(items.map(item => (item.id === id ? { ...item, checked } : item)));
  };

  return (
    <div className="space-y-3">
      <Checkbox
        label="Select all"
        defaultChecked={isAllChecked}
        indeterminate={isIndeterminate}
        onChange={handleSelectAll}
      />
      <div className="ml-6 space-y-2">
        {items.map(item => (
          <Checkbox
            key={item.id}
            label={item.label}
            defaultChecked={item.checked}
            onChange={checked => handleItemChange(item.id, checked)}
          />
        ))}
      </div>
    </div>
  );
};
```

## Label Variations

### Without Label

```tsx
// Checkbox without label - ensure accessibility
<Checkbox label="" aria-label="Accept terms" />
```

### Long Label

```tsx
// Checkbox with long wrapping label
<Checkbox label="This is a very long checkbox label that demonstrates how the component handles text wrapping for longer content that might span multiple lines in the interface." />
```

### Custom Label Content

```tsx
// Custom label with additional content
const CustomLabelCheckbox = () => (
  <div className="flex items-center gap-2">
    <Checkbox label="" />
    <div className="flex flex-col">
      <span className="text-sm font-medium">Premium Plan</span>
      <span className="text-xs text-gray-600">$9.99/month</span>
    </div>
  </div>
);
```

## Disabled States

### Basic Disabled States

```tsx
const DisabledStates = () => (
  <div className="flex flex-col gap-4">
    {/* Disabled unchecked */}
    <Checkbox label="Disabled checkbox" disabled={true} />

    {/* Disabled checked */}
    <Checkbox label="Disabled and checked" disabled={true} defaultChecked={true} />

    {/* Disabled indeterminate */}
    <Checkbox
      label="Disabled and indeterminate"
      disabled={true}
      indeterminate={true}
      defaultChecked={true}
    />

    {/* Normal for comparison */}
    <Checkbox label="Normal checkbox (for comparison)" />
  </div>
);
```

### Disabled with Validation

```tsx
// Disabled checkbox with validation state
<Checkbox
  label="Disabled with error"
  disabled={true}
  validationState="error"
  validationMessage="This field cannot be modified"
/>
```

## Interactive States

### Hover and Focus States

The component automatically handles interactive states:

- **Hover**: Border color changes to primary-40
- **Focus**: Ring with primary-60 color and proper focus management
- **Active**: Background changes to primary-60
- **Checked**: Background becomes primary-50 with white checkmark

### Custom State Handling

```tsx
const InteractiveCheckbox = () => {
  const [isChecked, setIsChecked] = useState(false);
  const [interactionCount, setInteractionCount] = useState(0);

  const handleChange = checked => {
    setIsChecked(checked);
    setInteractionCount(prev => prev + 1);
  };

  return (
    <div className="space-y-2">
      <Checkbox
        label={`Interactive checkbox (${interactionCount} interactions)`}
        defaultChecked={isChecked}
        onChange={handleChange}
      />
      <p className="text-sm text-gray-600">State: {isChecked ? "Checked" : "Unchecked"}</p>
    </div>
  );
};
```

## Advanced Usage

### Form Integration

```tsx
const CheckboxForm = () => {
  const [formData, setFormData] = useState({
    newsletter: false,
    terms: false,
    marketing: false,
  });

  const [errors, setErrors] = useState({});

  const handleSubmit = e => {
    e.preventDefault();
    const newErrors = {};

    if (!formData.terms) {
      newErrors.terms = "You must accept the terms and conditions";
    }

    setErrors(newErrors);

    if (Object.keys(newErrors).length === 0) {
      console.log("Form submitted:", formData);
    }
  };

  const handleCheckboxChange = (field, checked) => {
    setFormData(prev => ({ ...prev, [field]: checked }));
    if (errors[field]) {
      setErrors(prev => ({ ...prev, [field]: "" }));
    }
  };

  return (
    <form onSubmit={handleSubmit} className="space-y-4">
      <Checkbox
        label="Subscribe to newsletter"
        defaultChecked={formData.newsletter}
        onChange={checked => handleCheckboxChange("newsletter", checked)}
      />

      <Checkbox
        label="Accept marketing communications"
        defaultChecked={formData.marketing}
        onChange={checked => handleCheckboxChange("marketing", checked)}
        validationState={formData.marketing ? "success" : undefined}
        validationMessage={formData.marketing ? "Thank you for opting in" : undefined}
      />

      <Checkbox
        label="I accept the terms and conditions"
        defaultChecked={formData.terms}
        onChange={checked => handleCheckboxChange("terms", checked)}
        validationState={errors.terms ? "error" : undefined}
        validationMessage={errors.terms}
      />

      <button type="submit" className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600">
        Submit
      </button>
    </form>
  );
};
```

### Checkbox Group

```tsx
const CheckboxGroup = () => {
  const [selectedOptions, setSelectedOptions] = useState([]);

  const options = [
    { id: "email", label: "Email notifications", recommended: true },
    { id: "sms", label: "SMS notifications", recommended: false },
    { id: "push", label: "Push notifications", recommended: true },
    { id: "newsletter", label: "Weekly newsletter", recommended: false },
  ];

  const handleOptionChange = (optionId, checked) => {
    setSelectedOptions(prev =>
      checked ? [...prev, optionId] : prev.filter(id => id !== optionId)
    );
  };

  return (
    <div className="space-y-4">
      <h3 className="text-lg font-semibold">Notification Preferences</h3>
      {options.map(option => (
        <Checkbox
          key={option.id}
          label={option.label}
          defaultChecked={selectedOptions.includes(option.id)}
          onChange={checked => handleOptionChange(option.id, checked)}
          validationState={option.recommended ? "success" : undefined}
          validationMessage={option.recommended ? "Recommended" : undefined}
        />
      ))}
      <div className="mt-4 p-3 bg-gray-50 rounded">
        <p className="text-sm">
          Selected: {selectedOptions.length > 0 ? selectedOptions.join(", ") : "None"}
        </p>
      </div>
    </div>
  );
};
```

### Dynamic Validation

```tsx
const DynamicValidationCheckbox = () => {
  const [isChecked, setIsChecked] = useState(false);
  const [isValid, setIsValid] = useState(true);

  useEffect(() => {
    // Simulate validation after 2 seconds
    const timer = setTimeout(() => {
      setIsValid(isChecked);
    }, 2000);

    return () => clearTimeout(timer);
  }, [isChecked]);

  const getValidationState = () => {
    if (!isValid && isChecked) return "error";
    if (isValid && isChecked) return "success";
    return undefined;
  };

  const getValidationMessage = () => {
    if (!isValid && isChecked) return "Validation failed";
    if (isValid && isChecked) return "Validation successful";
    return undefined;
  };

  return (
    <Checkbox
      label="Dynamic validation checkbox"
      defaultChecked={isChecked}
      onChange={setIsChecked}
      validationState={getValidationState()}
      validationMessage={getValidationMessage()}
    />
  );
};
```

## Complete Example

```tsx
const CompleteCheckboxExample = () => {
  return (
    <div className="space-y-6 p-6 max-w-md">
      <h2 className="text-xl font-bold">Account Settings</h2>

      {/* Basic checkbox */}
      <Checkbox label="Enable two-factor authentication" size="m" />

      {/* Checkbox with success validation */}
      <Checkbox
        label="Backup email verified"
        size="m"
        validationState="success"
        validationMessage="Email verification complete"
        defaultChecked={true}
      />

      {/* Checkbox with warning */}
      <Checkbox
        label="Beta features"
        size="m"
        validationState="warning"
        validationMessage="These features are experimental"
      />

      {/* Required checkbox with error */}
      <Checkbox
        label="Privacy policy acceptance"
        size="m"
        validationState="error"
        validationMessage="Required to continue"
      />

      {/* Indeterminate state */}
      <Checkbox
        label="Select notification types"
        size="m"
        indeterminate={true}
        validationState="warning"
        validationMessage="Some notifications are enabled"
      />

      {/* Disabled checkbox */}
      <Checkbox
        label="Admin features"
        size="m"
        disabled={true}
        validationMessage="Contact administrator to enable"
      />
    </div>
  );
};
```

## Design Tokens & Styling

### Color Specifications

| State           | Background                      | Border            | Text              | Icon  |
| --------------- | ------------------------------- | ----------------- | ----------------- | ----- |
| Default         | Transparent                     | `neutral-grey-80` | `neutral-grey-80` | N/A   |
| Hover           | Transparent                     | `primary-40`      | `text-default`    | N/A   |
| Focus           | Transparent                     | `neutral-grey-80` | `text-default`    | N/A   |
| Active          | `primary-60`                    | `primary-60`      | White             | White |
| Checked         | `primary-50`                    | `primary-50`      | `text-default`    | White |
| Checked + Hover | `primary-40`                    | `primary-40`      | `text-default`    | White |
| Disabled        | 30% opacity on entire component |

### Validation Colors

| State   | Icon Color | Text Color             | Background  |
| ------- | ---------- | ---------------------- | ----------- |
| Success | `#25AB21`  | `text-success-subdued` | Transparent |
| Warning | `#F06D0F`  | `text-warning-subdued` | Transparent |
| Error   | `#F50031`  | `text-error-subdued`   | Transparent |

### Spacing & Layout

| Size | Checkbox | Icon | Gap (checkbox-label) | Gap (label-validation) | Text Style     |
| ---- | -------- | ---- | -------------------- | ---------------------- | -------------- |
| `s`  | 16px     | 12px | 8px                  | 4px + 24px offset      | desktop-body-m |
| `m`  | 20px     | 12px | 8px                  | 4px + 28px offset      | desktop-body-m |
| `l`  | 24px     | 16px | 8px                  | 8px + 32px offset      | desktop-body-l |

### Border Radius

- Checkbox: `rounded-checkbox` (custom design token)
- Focus ring: 4px with `primary-60` color

## Accessibility Features

The Checkbox component provides comprehensive accessibility support:

### ARIA Attributes

- `role="checkbox"` on the input element
- `aria-checked` reflects the current state
- `aria-disabled` when disabled prop is true
- `aria-describedby` connects validation messages
- `id` and `htmlFor` association between label and checkbox

### Keyboard Navigation

- **Space**: Toggle checkbox state
- **Enter**: Toggle checkbox state (custom implementation)
- **Tab**: Move focus to/from checkbox
- **Shift + Tab**: Move focus in reverse

### Screen Reader Support

```tsx
// Proper labeling for screen readers
<Checkbox
  label="Enable dark mode"
  aria-describedby="dark-mode-help"
/>
<div id="dark-mode-help">
  Changes the interface to use darker colors
</div>

// Required field indication
<Checkbox
  label="Terms and conditions (required)"
  validationState="error"
  validationMessage="This field is required"
  aria-required={true}
/>
```

## Best Practices

### Labeling

```tsx
// Good: Clear, descriptive labels
<Checkbox label="Send me weekly newsletter updates" />

// Good: Action-oriented labels
<Checkbox label="Enable automatic backups" />

// Avoid: Vague labels
<Checkbox label="Option 1" />
```

### Validation Messaging

```tsx
// Good: Specific, actionable messages
<Checkbox
  label="Email notifications"
  validationState="error"
  validationMessage="Please enable at least one notification method"
/>

// Good: Helpful success messages
<Checkbox
  label="Two-factor authentication"
  validationState="success"
  validationMessage="Your account is now more secure"
/>
```

### Form Integration

```tsx
// Good: Proper form structure
<fieldset>
  <legend>Notification Preferences</legend>
  <Checkbox label="Email updates" />
  <Checkbox label="SMS alerts" />
  <Checkbox label="Push notifications" />
</fieldset>

// Good: Required field handling
<Checkbox
  label="I agree to the terms of service"
  validationState={!agreed ? "error" : undefined}
  validationMessage={!agreed ? "Required to continue" : undefined}
  onChange={setAgreed}
/>
```

## Troubleshooting

### Common Issues

**Checkbox not changing state:**

- Verify `onChange` handler is properly connected
- Check if component is controlled vs uncontrolled
- Ensure `defaultChecked` is used for uncontrolled components

**Label not clickable:**

- Verify `label` prop is provided
- Check that `htmlFor` and `id` are properly associated
- Ensure no CSS is preventing label interaction

**Validation message not showing:**

- Confirm `validationState` is set
- Verify `validationMessage` is provided
- Check for CSS conflicts hiding the message

**Focus states not working:**

- Ensure component is not disabled
- Check for CSS overrides affecting focus styles
- Verify keyboard navigation is not prevented

### Performance Considerations

```tsx
// Good: Memoize expensive computations
const CheckboxList = ({ items }) => {
  const memoizedItems = useMemo(
    () =>
      items.map(item => ({
        ...item,
        validation: validateItem(item),
      })),
    [items]
  );

  return (
    <>
      {memoizedItems.map(item => (
        <Checkbox
          key={item.id}
          label={item.label}
          validationState={item.validation.state}
          validationMessage={item.validation.message}
        />
      ))}
    </>
  );
};
```

## Migration Guide

### From Basic HTML Checkbox

```tsx
// Before: HTML checkbox
<label>
  <input type="checkbox" name="terms" />
  Accept terms and conditions
</label>

// After: Genesis Checkbox
<Checkbox
  label="Accept terms and conditions"
  onChange={(checked) => setTermsAccepted(checked)}
/>
```

### From Other Checkbox Components

```tsx
// Before: Custom checkbox
<CustomCheckbox
  text="Enable feature"
  isChecked={checked}
  onToggle={setChecked}
  variant="primary"
  hasError={error}
  errorText={errorMessage}
/>

// After: Genesis Checkbox
<Checkbox
  label="Enable feature"
  defaultChecked={checked}
  onChange={setChecked}
  validationState={error ? "error" : undefined}
  validationMessage={errorMessage}
/>
```

## Integration Examples

### With Form Libraries

```tsx
// React Hook Form integration
const FormWithCheckbox = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Checkbox
        label="Subscribe to newsletter"
        {...register("newsletter")}
        validationState={errors.newsletter ? "error" : undefined}
        validationMessage={errors.newsletter?.message}
      />
    </form>
  );
};

// Formik integration
const FormikCheckbox = () => {
  return (
    <Formik initialValues={{ terms: false }} onSubmit={onSubmit}>
      <Field name="terms">
        {({ field, meta }) => (
          <Checkbox
            label="Accept terms"
            defaultChecked={field.value}
            onChange={field.onChange}
            validationState={meta.error ? "error" : undefined}
            validationMessage={meta.error}
          />
        )}
      </Field>
    </Formik>
  );
};
```

---

Consider using Checkbox with:

- **Form** — For form submissions and user preferences
- **Modal** — For confirmation dialogs and settings
- **Card** — For selectable content items
- **List** — For multi-selection interfaces
- **Settings** — For configuration toggles
- **Filters** — For search and filtering options
