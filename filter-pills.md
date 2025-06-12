# Filter Pills Component

## Overview

The Filter Pills component is a versatile and accessible filter interface built with Genesis Design System tokens. It provides a flexible way to filter data through multiple variants including multi-checkbox, single-radio, single select, and calendar-based filters. The component supports both controlled and uncontrolled states, with comprehensive customization options for layout, behavior, and appearance.

## Component API

### FilterPill Props

| Prop                       | Type                                                                                       | Default              | Description                                                       |
| -------------------------- | ------------------------------------------------------------------------------------------ | -------------------- | ----------------------------------------------------------------- |
| options                    | `Array<{ label: string; value: string }>`                                                  | Required             | Array of filter options with labels and values                    |
| selectedValues             | `string[] \| Date[]`                                                                       | Required             | Currently selected values (strings or dates depending on variant) |
| onChange                   | `(values: string[] \| Date[]) => void`                                                     | Required             | Callback when selected values change                              |
| placeholder                | `string`                                                                                   | `"Select"`           | Text shown when no value is selected                              |
| variant                    | `"multi-checkbox" \| "single-radio" \| "single" \| "calendar-single" \| "calendar-range"`  | `"multi-checkbox"`   | Type of filter interface                                          |
| triggerValue               | `JSX.Element \| string`                                                                    | `undefined`          | Custom content to display in the trigger button                   |
| open                       | `boolean`                                                                                  | `undefined`          | Controls open state in controlled component setup                 |
| onOpenChange               | `(value: boolean) => void`                                                                 | `undefined`          | Callback when open state changes                                  |
| onOptionClick              | `(value: any) => void`                                                                     | `undefined`          | Callback when an option is clicked (before applying)              |
| hideFooter                 | `boolean`                                                                                  | `undefined`          | Hides action buttons in footer for multi-checkbox or calendar     |
| hideExpandedIcon           | `boolean`                                                                                  | `false`              | Hides the expand arrow icon in the trigger                        |
| calendarProps              | `CalendarProps`                                                                            | `{ type: "single" }` | Props for internal calendar component                             |
| popoverContentProps        | `PopoverContentProps`                                                                      | `{}`                 | Props for PopoverContent component                                |
| popoverProps               | `PopoverProps`                                                                             | `{}`                 | Props for Popover component                                       |
| triggerButtonProps         | `PopoverTriggerProps`                                                                      | `{}`                 | Props for trigger button element                                  |
| buttonProps                | `Partial<{ clearButton: ButtonProps; applyButton: ButtonProps; doneButton: ButtonProps }>` | `{}`                 | Props for action buttons                                          |
| buttonText                 | `Partial<{ clearButton: string; applyButton: string; doneButton: string }>`                | `{}`                 | Custom text for action buttons                                    |
| menuItemProps              | `CommandItemProps`                                                                         | `{}`                 | Props for menu items                                              |
| noResultsProps             | `CommandEmptyProps`                                                                        | `{}`                 | Props for no results component                                    |
| searchInputProps           | `CommandInputProps`                                                                        | `{}`                 | Props for search input                                            |
| hideTriggerSelectionStatus | `boolean`                                                                                  | `false`              | Hides the selection status in trigger button                      |

### Import Statement

```typescript
import { FilterPill } from "gends";
```

## Filter Variants

### Multi-Checkbox Filter

The default variant that allows multiple selections with checkboxes.

**Key Features:**

- Multiple selection support
- Checkbox indicators
- Search functionality
- Apply/Clear actions
- Selection count display

```tsx
// Basic multi-checkbox filter
<FilterPill
  options={[
    { label: "Option 1", value: "option1" },
    { label: "Option 2", value: "option2" },
    { label: "Option 3", value: "option3" }
  ]}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  placeholder="Select Options"
  variant="multi-checkbox"
/>

// With custom trigger
<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  triggerValue={
    <div className="flex items-center gap-2">
      <IcFilter />
      <span>Filter Options</span>
      {selectedValues.length > 0 && (
        <Badge>{selectedValues.length}</Badge>
      )}
    </div>
  }
/>
```

### Single-Radio Filter

Variant that allows only one selection with radio buttons.

**Key Features:**

- Single selection only
- Radio button indicators
- Immediate selection
- No footer actions

```tsx
// Single-radio filter
<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  variant="single-radio"
  placeholder="Select One Option"
/>

// With custom styling
<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  variant="single-radio"
  menuItemProps={{
    className: "hover:bg-primary-50"
  }}
/>
```

### Single Select Filter

Simplified variant for single selection without radio buttons.

**Key Features:**

- Single selection
- Immediate selection
- No footer actions
- Clean interface

```tsx
// Single select filter
<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  variant="single"
  placeholder="Choose an option"
/>

// With search
<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  variant="single"
  searchInputProps={{
    placeholder: "Search options..."
  }}
/>
```

### Calendar Filters

Two variants for date-based filtering: single date and date range.

**Key Features:**

- Date picker integration
- Single or range selection
- Custom date formatting
- Clear/Apply actions

```tsx
// Single date filter
<FilterPill
  selectedValues={selectedDate}
  onChange={setSelectedDate}
  variant="calendar-single"
  placeholder="Select Date"
  calendarProps={{
    type: "single",
    disabled: (date) => date < new Date()
  }}
/>

// Date range filter
<FilterPill
  selectedValues={dateRange}
  onChange={setDateRange}
  variant="calendar-range"
  placeholder="Select Date Range"
  calendarProps={{
    type: "range",
    numberOfMonths: 2
  }}
/>
```

## Advanced Features

### Search Functionality

Built-in search with debouncing for filtering options.

```tsx
// Custom search input
<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  searchInputProps={{
    placeholder: "Search...",
    className: "custom-search-input",
  }}
/>
```

### Custom Trigger Content

Flexible trigger button content with selection status.

```tsx
// Custom trigger with selection status
<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  triggerValue={
    <div className="flex items-center gap-2">
      <span>Filter</span>
      {selectedValues.length > 0 && (
        <span className="text-primary-50">{selectedValues.length} selected</span>
      )}
    </div>
  }
/>
```

### Controlled State

Support for controlled open state and selection.

```tsx
// Controlled filter
const [isOpen, setIsOpen] = useState(false);
const [selectedValues, setSelectedValues] = useState([]);

<FilterPill
  options={options}
  selectedValues={selectedValues}
  onChange={setSelectedValues}
  open={isOpen}
  onOpenChange={setIsOpen}
  onOptionClick={values => {
    // Handle option click before applying
    console.log("Option clicked:", values);
  }}
/>;
```

## Real-World Usage Examples

### Data Table Filters

```tsx
const DataTableFilters = ({ columns, onFilterChange }) => {
  const [filters, setFilters] = useState({});

  const handleFilterChange = (column, values) => {
    const newFilters = { ...filters, [column]: values };
    setFilters(newFilters);
    onFilterChange(newFilters);
  };

  return (
    <div className="flex gap-2">
      {columns.map(column => (
        <FilterPill
          key={column.id}
          options={column.filterOptions}
          selectedValues={filters[column.id] || []}
          onChange={values => handleFilterChange(column.id, values)}
          placeholder={column.filterPlaceholder}
          variant={column.filterVariant}
        />
      ))}
    </div>
  );
};
```

### Form Field Filters

```tsx
const FormFieldFilter = ({ field, form }) => {
  return (
    <FilterPill
      options={field.options}
      selectedValues={field.value}
      onChange={values => {
        form.setFieldValue(field.name, values);
      }}
      variant={field.variant}
      placeholder={field.placeholder}
      onOptionClick={values => {
        // Validate before applying
        if (field.validate) {
          field.validate(values);
        }
      }}
    />
  );
};
```

### Date Range Filter

```tsx
const DateRangeFilter = ({ onRangeChange }) => {
  const [dateRange, setDateRange] = useState([]);

  const handleRangeChange = dates => {
    setDateRange(dates);
    onRangeChange(dates);
  };

  return (
    <FilterPill
      selectedValues={dateRange}
      onChange={handleRangeChange}
      variant="calendar-range"
      placeholder="Select Date Range"
      calendarProps={{
        type: "range",
        numberOfMonths: 2,
        disabled: date => date < new Date(),
      }}
      buttonText={{
        clearButton: "Reset",
        applyButton: "Apply Range",
      }}
    />
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab Navigation**: Focus management through trigger, search, options, and actions
- **Arrow Keys**: Navigate between options
- **Enter/Space**: Select focused option
- **Escape**: Close popover

### Screen Reader Support

- **ARIA Attributes**: Proper roles and states for all interactive elements
- **Live Regions**: Announcements for selection changes
- **Focus Management**: Maintains focus within popover when open

### Visual Accessibility

- **Focus Indicators**: Clear focus states for all interactive elements
- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Text Scaling**: Supports text size adjustments

## Design System Integration

### Genesis Design Tokens

**Colors:**

- `var(--gd-primary-50)`: Selection indicators and focus states
- `var(--gd-neutral-grey-20)`: Background colors
- `var(--gd-text-subdued-2)`: Placeholder and secondary text

**Spacing:**

- `gd-8`: Standard padding and gaps
- `gd-12`: Larger spacing for sections
- `gd-16`: Maximum spacing for major sections

**Typography:**

- `text-en-desktop-body-s`: Option text and metadata
- `text-en-desktop-body-m`: Trigger text and headings

**Border Radius:**

- `rounded-[8px]`: Standard border radius
- `rounded-[12px]`: Popover container
- `rounded-[16px]`: Calendar container

## Best Practices

### Performance

- Use debounced search for large option sets
- Implement virtualization for long option lists
- Optimize re-renders with proper state management

### User Experience

- Provide clear placeholder text
- Show selection status in trigger
- Use appropriate variant for the use case
- Implement proper loading states

### Integration

- Handle controlled and uncontrolled states properly
- Implement proper form integration
- Consider mobile responsiveness
- Test with screen readers

## Troubleshooting

### Common Issues

**Selection Not Updating:**

- Check if component is controlled or uncontrolled
- Verify onChange handler implementation
- Ensure proper value types for variant

**Calendar Issues:**

- Verify date format consistency
- Check calendar props configuration
- Ensure proper date object handling

**Search Not Working:**

- Verify option label format
- Check search input configuration
- Ensure proper debouncing

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test keyboard navigation
- Verify accessibility features

Remember: The Filter Pills component provides a flexible and accessible way to implement various filter interfaces. Choose the appropriate variant and configuration based on your specific use case and requirements.
