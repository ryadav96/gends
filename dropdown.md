# Dropdown

The Dropdown component is a flexible and feature-rich select menu that enhances user experience through various customization options. It supports single and multi-select functionality, grouped options, searchable options, custom icons, and validation states.

## Features

- ✅ Single & Multi-Select – Allows selecting one or multiple options
- 📂 Grouped Options – Organizes related options under logical groupings
- 🔍 Searchable Dropdown – Enables filtering options through search
- 🎨 Custom Icons & Avatars – Supports custom icons for options
- ⚠️ Validation States – Displays validation feedback (error, warning, success)
- 🚫 Disabled Options – Supports disabling specific options or entire dropdown

## Usage

```tsx
import { Dropdown } from 'gends';

const options = [
  { id: 1, label: "Profile", icon: <UserIcon /> },
  { id: 2, label: "Settings", icon: <SettingsIcon /> }
];

export default function Example() {
  const [selected, setSelected] = useState([]);

  return (
    <Dropdown
      label="Select an option"
      options={options}
      value={selected}
      onChange={setSelected}
    />
  );
}
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| options | DropdownOption[] | [] | Array of options to display in the dropdown |
| placeholder | string | "Search..." | Placeholder text when no option is selected |
| value | DropdownOption[] | [] | Currently selected option(s) |
| onChange | (allSelectedOptions: DropdownOption[], currentSelectedOption?: DropdownOption) => void | - | Callback when selection changes |
| disabled | boolean | false | Disables the entire dropdown |
| validationState | "default" \| "error" \| "warning" \| "success" | "default" | Sets the validation state |
| validationMessage | string | - | Message to display for validation feedback |
| required | boolean | false | Marks the dropdown as required |
| isMultiSelect | boolean | false | Enables selecting multiple options |
| isRadioSelect | boolean | false | Changes to radio button selection mode |
| searchable | boolean | false | Enables search functionality |
| size | "s" \| "m" \| "l" | "l" | Controls the size of the dropdown |
| label | string | - | Label text displayed above the dropdown |
| helperText | string | - | Helper text shown on hover of info icon |
| hideFooterActions | boolean | true | Hides the footer actions (Clear All/Apply) |
| hideCrossIcon | boolean | false | Hides the clear selection icon |

## Types

```typescript
interface DropdownOption {
  id: number | string;
  label: string;
  value: string | number;
  icon?: JSX.Element;
  type?: string;
  helpText?: string;
  groupId?: string | number;
  disabled?: boolean;
}

interface DropdownGroup {
  id: string | number;
  label?: string;
}

type DropdownClassNames = {
  popoverContainerClasses?: string;
  popoverTriggerClasses?: string;
  popoverTriggerChildClasses?: string;
  popoverContentClasses?: string;
  scrollAreaClasses?: string;
  footerClasses?: string;
  inputSearchClasses?: string;
  itemClasses?: string;
};
```

## Variants

### Basic Dropdown
```tsx
<Dropdown
  label="Select an option"
  placeholder="Choose..."
  options={options}
/>
```

### Searchable Dropdown
```tsx
<Dropdown
  label="Searchable Dropdown"
  placeholder="Search or select..."
  searchable={true}
  options={options}
/>
```

### Multi-Select Dropdown
```tsx
<Dropdown
  label="Multi-Select"
  placeholder="Select multiple options"
  isMultiSelect={true}
  options={options}
/>
```

### Radio Select Dropdown
```tsx
<Dropdown
  label="Radio-Select"
  placeholder="Select option"
  isRadioSelect={true}
  options={options}
/>
```

### Grouped Options
```tsx
<Dropdown
  label="Grouped Dropdown"
  options={groupedOptions}
  groups={[
    { id: 1, label: "Group 1" },
    { id: 2, label: "Group 2" }
  ]}
  isMultiSelect={true}
/>
```

### With Validation States
```tsx
// Error State
<Dropdown
  label="Error State"
  options={options}
  validationState="error"
  validationMessage="Something went wrong!"
/>

// Warning State
<Dropdown
  label="Warning State"
  options={options}
  validationState="warning"
  validationMessage="Please be careful!"
/>

// Success State
<Dropdown
  label="Success State"
  options={options}
  validationState="success"
  validationMessage="Looks good!"
/>
```

### Different Sizes
```tsx
// Small
<Dropdown
  size="s"
  label="Small Dropdown"
  options={options}
/>

// Medium
<Dropdown
  size="m"
  label="Medium Dropdown"
  options={options}
/>

// Large
<Dropdown
  size="l"
  label="Large Dropdown"
  options={options}
/>
```

## Styling

The Dropdown component accepts custom classNames for various parts of its structure through the `classNames` prop:

```tsx
<Dropdown
  classNames={{
    popoverContainerClasses: "w-[400px]",
    popoverTriggerClasses: "custom-trigger",
    popoverContentClasses: "custom-content",
    scrollAreaClasses: "custom-scroll",
    itemClasses: "custom-item"
  }}
  // ... other props
/>
```

## Accessibility

- Supports keyboard navigation (arrow keys, Enter, Escape)
- Properly labeled form controls with aria-labels
- ARIA attributes for validation states
- Focus management for better keyboard interaction
- Screen reader friendly option selection

## Best Practices

1. Always provide meaningful labels and placeholders
2. Use validation states and messages appropriately
3. Group related options when the list is long
4. Enable search for dropdowns with many options
5. Keep option labels concise and clear
6. Use appropriate size based on context
7. Include helper text for complex selections