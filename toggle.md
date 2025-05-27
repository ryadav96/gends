# Toggle

A customizable toggle switch component that supports various sizes, states, validation states, and helper text.

## 1. Quick start

```tsx
import { Toggle } from 'gends';

// Basic usage
<Toggle label="Toggle switch" onChange={checked => console.log(checked)} />

// Controlled
const [checked, setChecked] = useState(false);
<Toggle label="Toggle switch" checked={checked} onChange={setChecked} />
```

## 2. Sizes

```tsx
// Small
<Toggle size="sm" label="Small toggle" />

// Medium (default)
<Toggle size="md" label="Medium toggle" />

// Large
<Toggle size="lg" label="Large toggle" />
```

## 3. Label Positions

```tsx
// Left (default)
<Toggle label="Left label" labelPosition="left" />

// Right
<Toggle label="Right label" labelPosition="right" />

// No label
<Toggle labelPosition="none" />

// With icon
<Toggle
  label="With icon"
  icon={<IcInfo className="h-gd-16 w-gd-16" />}
/>
```

## 4. States

```tsx
// Default
<Toggle label="Default" />

// Checked
<Toggle label="Checked" defaultChecked />

// Disabled
<Toggle label="Disabled" disabled />

// Disabled and checked
<Toggle label="Disabled checked" disabled defaultChecked />
```

## 5. Validation States

```tsx
// Success
<Toggle
  label="Success"
  validationState="success"
  validationMessage="Success Text"
  helperIcon={<IcSuccess className="h-gd-16 w-gd-16" />}
/>

// Warning
<Toggle
  label="Warning"
  validationState="warning"
  validationMessage="Warning Text"
  helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
/>

// Error
<Toggle
  label="Error"
  validationState="error"
  validationMessage="Error Text"
  helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
/>

// Helper text only
<Toggle
  label="With helper"
  validationMessage="Helper Text"
/>
```

## 6. Full prop reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `defaultChecked` | `boolean` | `false` | Initial checked state |
| `checked` | `boolean` | – | Controlled checked state |
| `onChange` | `(checked: boolean) => void` | – | Change handler |
| `disabled` | `boolean` | `false` | Disable the toggle |
| `label` | `string` | – | Label text |
| `icon` | `ReactNode` | – | Icon next to label |
| `labelPosition` | `'left' \| 'right' \| 'none'` | `'left'` | Label position |
| `validationState` | `'default' \| 'success' \| 'warning' \| 'error'` | `'default'` | Visual state |
| `validationMessage` | `string` | – | Helper/validation text |
| `helperIcon` | `ReactNode` | – | Icon next to helper text |
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` | Toggle size |
| `id` | `string` | – | HTML ID |
| `name` | `string` | – | Form field name |

## 7. Common Use Cases

### Form Field
```tsx
<form onSubmit={handleSubmit}>
  <Toggle
    name="notifications"
    label="Enable notifications"
    defaultChecked
  />
</form>
```

### Settings Toggle
```tsx
<Toggle
  label="Dark mode"
  icon={<IcMoon />}
  checked={isDarkMode}
  onChange={setIsDarkMode}
/>
```

### Feature Flag
```tsx
<Toggle
  label="Beta features"
  validationState="warning"
  validationMessage="Experimental features may be unstable"
  helperIcon={<IcWarning />}
/>
```

### Disabled State with Reason
```tsx
<Toggle
  label="Premium feature"
  disabled
  validationState="error"
  validationMessage="Upgrade to access this feature"
  helperIcon={<IcLock />}
/>
```

## 8. Best Practices

1. **Clear Labels**
```tsx
// Good
<Toggle label="Enable notifications" />

// Better
<Toggle
  label="Enable notifications"
  validationMessage="You'll receive updates about your account"
/>
```

2. **Meaningful Icons**
```tsx
<Toggle
  label="Dark mode"
  icon={<IcMoon />}
  validationState="success"
  validationMessage="Theme will change automatically"
  helperIcon={<IcSuccess />}
/>
```

3. **Proper Validation**
```tsx
<Toggle
  label="Delete account"
  validationState="error"
  validationMessage="This action cannot be undone"
  helperIcon={<IcWarning />}
/>
```