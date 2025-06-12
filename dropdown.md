# Dropdown Component

## Overview

The Dropdown component is a powerful and flexible select interface built on Radix UI primitives with Genesis Design System tokens. It supports single selection, multi-selection, radio selection modes, searchable options, grouped options, dynamic option addition, extensive validation states, and comprehensive accessibility features. The component provides seamless form integration and offers complete customization through various styling props.

## Component API

### Dropdown Props

| Prop                 | Type                                                                | Default       | Description                                                           |
| -------------------- | ------------------------------------------------------------------- | ------------- | --------------------------------------------------------------------- |
| options              | `DropdownOption[]`                                                  | `[]`          | Array of dropdown options to display                                  |
| placeholder          | `string`                                                            | `"Search..."` | Placeholder text shown when no option is selected                     |
| value                | `DropdownOption[]`                                                  | `[]`          | Currently selected option(s) - always array even for single selection |
| onChange             | `(allSelected: DropdownOption[], current?: DropdownOption) => void` | -             | Callback fired when selection changes                                 |
| onAddOption          | `(option: DropdownOption) => void`                                  | -             | Callback for adding new options dynamically                           |
| showAddButton        | `boolean`                                                           | `false`       | Shows "Add" button when no results found during search                |
| defaultIcon          | `JSX.Element`                                                       | -             | Default icon displayed in the trigger                                 |
| disabled             | `boolean`                                                           | `false`       | Disables the entire dropdown                                          |
| readOnly             | `boolean`                                                           | `false`       | Makes dropdown read-only (shows value but prevents interaction)       |
| validationMessage    | `string`                                                            | -             | Validation message displayed below dropdown                           |
| validationState      | `"default" \| "error" \| "warning" \| "success"`                    | `"default"`   | Visual validation state                                               |
| required             | `boolean`                                                           | `false`       | Marks dropdown as required (adds asterisk to label)                   |
| isMultiSelect        | `boolean`                                                           | `false`       | Enables multiple option selection with checkboxes                     |
| isRadioSelect        | `boolean`                                                           | `false`       | Uses radio buttons for single selection (overridden by isMultiSelect) |
| helperText           | `string`                                                            | -             | Helper text shown on info icon hover                                  |
| label                | `string`                                                            | -             | Label text displayed above dropdown                                   |
| groups               | `DropdownGroup[]`                                                   | `[]`          | Group definitions for organizing options                              |
| searchable           | `boolean`                                                           | `false`       | Enables search functionality with input field                         |
| hideFooterActions    | `boolean`                                                           | `true`        | Hides footer with "Clear All" and "Apply" buttons                     |
| size                 | `"s" \| "m" \| "l"`                                                 | `"l"`         | Controls dropdown dimensions and typography                           |
| classNames           | `DropdownClassNames`                                                | -             | Custom CSS classes for different dropdown parts                       |
| onBlur               | `() => void`                                                        | -             | Callback fired when dropdown loses focus                              |
| hideCrossIcon        | `boolean`                                                           | `false`       | Hides the clear selection 'X' icon                                    |
| inputValidationRegex | `RegExp`                                                            | -             | Regex pattern for validating search input                             |
| supportText          | `string`                                                            | -             | Additional support text displayed below dropdown                      |
| children             | `React.ReactNode`                                                   | -             | Custom trigger content (replaces default trigger)                     |
| onInputChange        | `(e: React.ChangeEvent<HTMLInputElement>) => void`                  | -             | Callback for search input changes                                     |
| inputValue           | `string`                                                            | -             | Controlled search input value                                         |
| isOpen               | `boolean`                                                           | -             | Controlled open state                                                 |
| onOpenChange         | `(isOpen: boolean) => void`                                         | -             | Callback for open state changes                                       |
| hideNoResultsFound   | `boolean`                                                           | `false`       | Hides "No results found" message                                      |
| popoverContainerSize | `string`                                                            | -             | Custom width for dropdown popover                                     |
| extraProps           | `InternalProps`                                                     | -             | Additional props for Radix UI popover components                      |
| hideSelection        | `boolean`                                                           | `false`       | Hides selection indicators (checkboxes/radio buttons)                 |

### DropdownOption Interface

```typescript
interface DropdownOption {
  id: number | string; // Unique identifier for the option
  label: string; // Display text for the option
  value: string | number; // Value associated with the option
  icon?: JSX.Element; // Optional icon displayed next to label
  type?: string; // Optional type classification
  helpText?: string; // Optional help text shown on hover
  groupId?: string | number; // Group ID for grouped options
  disabled?: boolean; // Whether option is disabled
}
```

### DropdownGroup Interface

```typescript
interface DropdownGroup {
  id: string | number; // Unique identifier for the group
  label?: string; // Optional group label displayed above options
}
```

### DropdownClassNames Interface

```typescript
type DropdownClassNames = {
  popoverContainerClasses?: string; // Container wrapper classes
  popoverTriggerClasses?: string; // Trigger button classes
  popoverTriggerChildClasses?: string; // Child elements within trigger
  popoverContentClasses?: string; // Popover content container classes
  scrollAreaClasses?: string; // Scroll area classes
  footerClasses?: string; // Footer action area classes
  inputSearchClasses?: string; // Search input field classes
  itemClasses?: string; // Individual option item classes
};
```

### InternalProps Interface

```typescript
type InternalProps = {
  popoverProps?: Partial<PopoverProps>;
  popoverTriggerProps?: Partial<PopoverTriggerProps & { className?: string }>;
  popoverContentProps?: Partial<
    PopoverContentProps & {
      className?: string;
      sticky?: "partial" | "always" | "never";
      align?: "start" | "center" | "end";
      style?: React.CSSProperties;
    }
  >;
};
```

## Size Variants

### Large Size (Default)

```tsx
<Dropdown
  size="l"
  label="Large Dropdown"
  placeholder="Select an option"
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

- **Dimensions**: 48px height
- **Typography**: `text-en-desktop-body-l` (16px)
- **Use Cases**: Primary forms, desktop applications, main content areas

### Medium Size

```tsx
<Dropdown size="m" label="Medium Dropdown" placeholder="Select an option" options={options} />
```

- **Dimensions**: 40px height
- **Typography**: `text-en-desktop-body-m` (14px)
- **Use Cases**: Secondary forms, modal dialogs, compact layouts

### Small Size

```tsx
<Dropdown size="s" label="Small Dropdown" placeholder="Select an option" options={options} />
```

- **Dimensions**: 32px height
- **Typography**: `text-en-desktop-body-s` (12px)
- **Use Cases**: Table cells, filter bars, space-constrained interfaces

## Selection Modes

### Single Selection (Default)

```tsx
const [selected, setSelected] = useState([]);

<Dropdown
  label="Single Select"
  placeholder="Choose one option"
  options={options}
  value={selected}
  onChange={allSelected => setSelected(allSelected)}
/>;
```

### Multi-Select Mode

```tsx
const [multiSelected, setMultiSelected] = useState([]);

<Dropdown
  label="Multi-Select"
  placeholder="Select multiple options"
  isMultiSelect={true}
  options={options}
  value={multiSelected}
  onChange={allSelected => setMultiSelected(allSelected)}
  hideFooterActions={false} // Show Clear All/Apply buttons
/>;
```

### Radio Select Mode

```tsx
const [radioSelected, setRadioSelected] = useState([]);

<Dropdown
  label="Radio-Select"
  placeholder="Select option"
  isRadioSelect={true}
  options={options}
  value={radioSelected}
  onChange={allSelected => setRadioSelected(allSelected)}
/>;
```

## Search Functionality

### Basic Searchable Dropdown

```tsx
<Dropdown
  label="Searchable Dropdown"
  placeholder="Search or select..."
  searchable={true}
  options={options}
/>
```

### Multi-Select with Search

```tsx
<Dropdown
  label="Multi-Select with Search"
  placeholder="Select multiple options"
  searchable={true}
  isMultiSelect={true}
  options={options}
/>
```

### Input Validation with Regex

```tsx
<Dropdown
  label="Input Search Validation (Alphanumeric)"
  placeholder="Enter text"
  searchable={true}
  inputValidationRegex={/^[a-zA-Z0-9\s]*$/}
  options={options}
/>
```

## Grouped Options

### Basic Grouped Options

```tsx
const groupedOptions = [
  { id: 1, label: "Profile", value: "profile", groupId: "user" },
  { id: 2, label: "Settings", value: "settings", groupId: "user" },
  { id: 3, label: "Reports", value: "reports", groupId: "admin" },
  { id: 4, label: "Analytics", value: "analytics", groupId: "admin" },
];

const groups = [
  { id: "user", label: "User Options" },
  { id: "admin", label: "Admin Options" },
];

<Dropdown label="Grouped Dropdown" options={groupedOptions} groups={groups} isMultiSelect={true} />;
```

## Validation States

### Error State

```tsx
<Dropdown
  label="Error State"
  options={options}
  validationState="error"
  validationMessage="Please select at least one option"
  required={true}
/>
```

### Warning State

```tsx
<Dropdown
  label="Warning State"
  options={options}
  validationState="warning"
  validationMessage="This selection may affect other settings"
/>
```

### Success State

```tsx
<Dropdown
  label="Success State"
  options={options}
  validationState="success"
  validationMessage="Selection validated successfully"
/>
```

## Dynamic Options

### Add New Options

```tsx
const [dynamicOptions, setDynamicOptions] = useState(baseOptions);

<Dropdown
  label="Dropdown with Add Option"
  options={dynamicOptions}
  showAddButton={true}
  searchable={true}
  onAddOption={newOption => {
    setDynamicOptions([...dynamicOptions, newOption]);
  }}
/>;
```

## Custom Icons and Styling

### With Custom Default Icon

```tsx
import { IcFavorite } from "gends";

<Dropdown
  label="Custom Icon Dropdown"
  defaultIcon={<IcFavorite size="20" />}
  options={options}
  size="m"
/>;
```

### With Option Icons

```tsx
const iconOptions = [
  {
    id: 1,
    label: "Home",
    value: "home",
    icon: <IcHome size="16" />,
  },
  {
    id: 2,
    label: "Profile",
    value: "profile",
    icon: <IcUser size="16" />,
  },
];

<Dropdown label="Options with Icons" options={iconOptions} />;
```

### Custom Styling

```tsx
<Dropdown
  label="Custom Styled Dropdown"
  options={options}
  classNames={{
    popoverContainerClasses: "w-[400px]",
    popoverTriggerClasses: "border-2 border-blue-500",
    popoverContentClasses: "shadow-2xl",
    itemClasses: "hover:bg-blue-50",
  }}
/>
```

## Advanced Usage

### Custom Trigger

```tsx
<Dropdown
  options={options}
  hideSelection={true}
  popoverContainerSize="200px"
  classNames={{
    popoverTriggerClasses: "w-[60px]",
  }}
  extraProps={{
    popoverContentProps: {
      align: "end",
    },
  }}
>
  <div className="text-color-neutral-grey-60 w-[100px] text-sm border inline p-2 rounded-md cursor-pointer">
    Select
  </div>
</Dropdown>
```

### Controlled State

```tsx
const [isOpen, setIsOpen] = useState(false);
const [searchValue, setSearchValue] = useState("");

<Dropdown
  label="Controlled Dropdown"
  options={options}
  isOpen={isOpen}
  onOpenChange={setIsOpen}
  inputValue={searchValue}
  onInputChange={e => setSearchValue(e.target.value)}
  searchable={true}
/>;
```

### Read-Only Mode

```tsx
<Dropdown
  label="Read-Only Dropdown"
  placeholder="Can't interact"
  options={options}
  readOnly={true}
  value={[options[0]]}
/>
```

### Disabled State

```tsx
<Dropdown label="Disabled Dropdown" placeholder="Can't select" options={options} disabled={true} />
```

## Integration Examples

### Form Integration

```tsx
import { useForm, Controller } from "react-hook-form";

const FormExample = () => {
  const { control, handleSubmit } = useForm();

  const onSubmit = data => {
    console.log("Selected options:", data.dropdown);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Controller
        name="dropdown"
        control={control}
        rules={{ required: "Please select an option" }}
        render={({ field, fieldState }) => (
          <Dropdown
            label="Required Selection"
            options={options}
            value={field.value || []}
            onChange={field.onChange}
            validationState={fieldState.error ? "error" : "default"}
            validationMessage={fieldState.error?.message}
            required={true}
          />
        )}
      />
      <button type="submit">Submit</button>
    </form>
  );
};
```

### Filter System

```tsx
const FilterDropdown = () => {
  const [filters, setFilters] = useState([]);

  return (
    <Dropdown
      label="Filter Options"
      placeholder="Select filters"
      isMultiSelect={true}
      hideFooterActions={false}
      options={filterOptions}
      value={filters}
      onChange={setFilters}
      onBlur={() => console.log("Filters applied:", filters)}
    />
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Arrow Keys**: Navigate through options
- **Enter/Space**: Select highlighted option
- **Escape**: Close dropdown
- **Home/End**: Jump to first/last option
- **Type-ahead**: Quick navigation by typing

### Screen Reader Support

- Proper ARIA labels and descriptions
- Role-based announcements
- Selection state communication
- Group structure announcements

### Focus Management

- Maintains focus within dropdown when open
- Returns focus to trigger when closed
- Visual focus indicators throughout

## Design Tokens

### Colors

- **Default**: Uses Genesis neutral color palette
- **Success**: `--gd-feedback-success-*` tokens
- **Warning**: `--gd-feedback-warning-*` tokens
- **Error**: `--gd-feedback-error-*` tokens
- **Primary**: `--gd-primary-*` tokens for selections

### Typography

- **Large**: `text-en-desktop-body-l` (16px/24px)
- **Medium**: `text-en-desktop-body-m` (14px/20px)
- **Small**: `text-en-desktop-body-s` (12px/16px)

### Spacing

- **Padding**: Uses `gd-*` spacing tokens
- **Gaps**: Consistent `gd-8`, `gd-12`, `gd-16` spacing
- **Margins**: Standard Genesis spacing scale

### Border Radius

- **Large**: `rounded-[16px]`
- **Medium/Small**: `rounded-[12px]`
- **Component tokens**: Uses Genesis border radius system

### Shadows

- **Popover**: `0px 4px 16px 0px #00000029`
- **Footer**: `0 -4px 16px -5px rgba(0,0,0,0.08)`

## Best Practices

### Performance

- Use `React.memo` for option lists with many items
- Implement virtual scrolling for 500+ options
- Debounce search input to limit API calls
- Use stable option IDs to prevent unnecessary re-renders

### UX Guidelines

- Provide clear labels and helpful placeholder text
- Use validation messages for guidance
- Group related options logically
- Consider default selections for better usability
- Test with keyboard-only navigation

### Accessibility

- Always provide labels for screen readers
- Use semantic HTML structure
- Ensure sufficient color contrast
- Test with assistive technologies
- Provide clear error messages

## Troubleshooting

### Common Issues

**Options not updating**: Ensure option objects have stable IDs and proper referential equality.

**Search not working**: Verify `searchable={true}` is set and options have searchable `label` fields.

**Styling not applied**: Check CSS specificity and ensure classNames are properly applied.

**Keyboard navigation failing**: Verify proper focus management and ARIA attributes.

**Performance issues**: Implement virtual scrolling for large option lists and optimize re-render patterns.

### Migration Notes

When upgrading from v1.x:

- `onChange` callback signature changed to provide all selected options
- `isMultiSelect` and `isRadioSelect` are now separate props
- `classNames` prop structure has been updated
- Footer actions are now hidden by default
