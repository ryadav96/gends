# Date Picker

The Date Picker component allows users to select a date or date range using a calendar interface. It supports various features like time selection, date ranges, manual input, and filtering options.

## Features

- Single date and date range selection
- Optional time picker
- Custom date filters
- Manual date input
- Multiple size variants
- Validation states
- Tooltip support
- Disabled and readonly states

## Installation

```tsx
import { DatePicker } from '@genesis/components';
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `type` | `"single" \| "range"` | `"single"` | Determines whether to allow single date or date range selection |
| `size` | `"s" \| "m" \| "l"` | `"m"` | Controls the size of the date picker |
| `timer` | `boolean` | `false` | Enables/disables time selection |
| `filters` | `FilterItem[]` | `[]` | Array of predefined date filter options |
| `required` | `boolean` | `false` | Makes the date picker required |
| `selectedDates` | `Date[]` | `[]` | Array of selected dates |
| `onDateChangeHandler` | `(dates: Date[]) => void` | - | Callback function when dates change |
| `validationState` | `"default" \| "warning" \| "error" \| "success"` | `"default"` | Sets the validation state |
| `helperText` | `string` | `""` | Tooltip information text |
| `validationMessage` | `string` | `""` | Validation message shown below the component |
| `supportText` | `string` | `""` | Additional support text |
| `disabled` | `boolean` | `false` | Disables the date picker |
| `width` | `string` | - | Custom width for the date picker |
| `label` | `string` | `""` | Label text for the date picker |
| `placeholder` | `string` | `"DD/MM/YYYY"` | Placeholder text |
| `allowManualInput` | `boolean` | `true` | Allows manual date input |
| `readOnly` | `boolean` | `false` | Makes the date picker read-only |

## Examples

### Basic Single Date Picker

```tsx
import { DatePicker } from '@genesis/components';
import { useState } from 'react';

const BasicExample = () => {
  const [selectedDates, setSelectedDates] = useState<Date[]>([]);

  return (
    <DatePicker 
      type="single"
      selectedDates={selectedDates}
      onDateChangeHandler={setSelectedDates}
      label="Select Date"
      placeholder="Pick a date"
    />
  );
};
```

### Date Range Picker with Time

```tsx
const RangeExample = () => {
  const [dateRange, setDateRange] = useState<Date[]>([]);

  return (
    <DatePicker 
      type="range"
      timer={true}
      selectedDates={dateRange}
      onDateChangeHandler={setDateRange}
      label="Select Date Range"
      placeholder="Select start date ~ Select end date"
    />
  );
};
```

### With Filters

```tsx
const filters = [
  {
    id: 1,
    label: "Today",
    onSelect: (date: Date) => [date]
  },
  {
    id: 2,
    label: "Yesterday",
    onSelect: (date: Date) => [addDays(date, -1)]
  },
  // ... more filters
];

const FilterExample = () => {
  const [dates, setDates] = useState<Date[]>([]);

  return (
    <DatePicker 
      type="single"
      filters={filters}
      selectedDates={dates}
      onDateChangeHandler={setDates}
      label="Select Date"
      placeholder="Pick a date"
    />
  );
};
```

### With Validation

```tsx
const ValidationExample = () => {
  return (
    <DatePicker 
      type="single"
      validationState="error"
      validationMessage="Please select a valid date"
      label="Select Date"
      placeholder="Pick a date"
    />
  );
};
```

## Size Variants

The date picker comes in three sizes:

- Small (`s`): Compact version
- Medium (`m`): Default size
- Large (`l`): Larger version with more prominent elements

```tsx
// Small
<DatePicker size="s" />

// Medium (default)
<DatePicker size="m" />

// Large
<DatePicker size="l" />
```

## FilterItem Interface

```tsx
interface FilterItem {
  id: number | string;
  label: string;
  onSelect: (date: Date) => Date[];
}
```

## Custom Styling

The date picker supports custom styling through the `classNames` prop:

```tsx
<DatePicker
  classNames={{
    popoverTriggerClasses: "custom-trigger",
    popoverContentClasses: "custom-content",
    toolTipTriggerClasses: "custom-tooltip-trigger",
    toolTipContentClasses: "custom-tooltip-content",
    inputFeildClasses: "custom-input",
    clearIconClasses: "custom-clear-icon",
    prefixIconClasses: "custom-prefix-icon",
    inBetweenArrowIconClasses: "custom-arrow-icon",
    buttonClasses: "custom-button",
    filterItemClasses: "custom-filter-item"
  }}
/>
```

## Best Practices

1. Always provide meaningful labels and placeholders
2. Use validation states to provide clear feedback
3. Consider using filters for common date selections
4. Provide helper text for complex date requirements
5. Use appropriate size variant based on the context
6. Consider mobile users when implementing manual input
7. Implement proper error handling for invalid dates