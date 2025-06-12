# Date Picker Component

## Overview

The DatePicker component is a comprehensive date selection interface that combines a customizable input field with a calendar popover. Built on Radix UI primitives and the Genesis Design System, it supports both single date and date range selection modes, optional time selection, predefined filters, manual input capabilities, and extensive validation states. The component provides seamless integration with forms and offers robust accessibility features for all user interactions.

## Component API

### DatePicker Props

| Prop                  | Type                                                       | Default             | Description                                                     |
| --------------------- | ---------------------------------------------------------- | ------------------- | --------------------------------------------------------------- |
| `type`                | `"single" \| "range"`                                      | `"single"`          | Determines whether to allow single date or date range selection |
| `size`                | `"s" \| "m" \| "l"`                                        | `"m"`               | Controls the size of the date picker and all its elements       |
| `timer`               | `boolean`                                                  | `false`             | Enables/disables time selection with a TimePicker component     |
| `filters`             | `FilterItem[]`                                             | `[]`                | Array of predefined date filter options shown in left panel     |
| `required`            | `boolean`                                                  | `false`             | Makes the date picker required (shows asterisk in label)        |
| `selectedDates`       | `Date[]`                                                   | `[]`                | Array of selected dates (controlled component)                  |
| `onDateChangeHandler` | `Dispatch<SetStateAction<Date[]>>`                         | `() => {}`          | Callback function when dates change                             |
| `validationState`     | `"default" \| "warning" \| "error" \| "success"`           | `"default"`         | Sets the validation state with appropriate styling              |
| `helperText`          | `string`                                                   | `undefined`         | Tooltip information text shown next to label                    |
| `validationMessage`   | `string`                                                   | `undefined`         | Validation message shown below the component using MessageBox   |
| `supportText`         | `string`                                                   | `undefined`         | Additional support text shown below the component               |
| `disabled`            | `boolean`                                                  | `false`             | Disables the entire date picker component                       |
| `width`               | `string`                                                   | `"100%"`            | Custom width for the date picker container                      |
| `label`               | `string`                                                   | `undefined`         | Label text displayed above the date picker                      |
| `placeholder`         | `string`                                                   | `"DD/MM/YYYY"`      | Placeholder text shown in the input field                       |
| `allowManualInput`    | `boolean`                                                  | `true`              | Allows manual date input via typing in DD/MM/YYYY format        |
| `readOnly`            | `boolean`                                                  | `false`             | Makes the date picker read-only (shows values but no editing)   |
| `prefixIcon`          | `React.JSX.Element`                                        | `undefined`         | Custom icon shown at the beginning of the input field           |
| `dateFormatter`       | `(dates: (string \| Date)[], isTime: boolean) => string[]` | `formatDateAndTime` | Custom date formatting function                                 |
| `propsConfig`         | `PropsConfig`                                              | `undefined`         | Configuration object for underlying component props             |
| `classNames`          | `ClassNamesTypes`                                          | `undefined`         | Custom CSS classes for styling various parts                    |

### FilterItem Interface

```typescript
interface FilterItem {
  id: number | string;
  label: string;
  onSelect: (date: Date) => Date[];
}
```

### PropsConfig Interface

```typescript
interface PropsConfig {
  calendarProps?: CalendarProps;
  timePickerProps?: TimePickerProps;
  popoverTriggerProps?: PopoverTriggerProps;
  popoverContentProps?: PopoverContentProps;
  toolTipProps?: TooltipProps;
  toolTipTriggerProps?: TooltipTriggerProps;
  toolTipContentProps?: TooltipContentProps;
}
```

### ClassNamesTypes Interface

```typescript
interface ClassNamesTypes {
  popoverTriggerClasses?: string;
  popoverContentClasses?: string;
  toolTipTriggerClasses?: string;
  toolTipContentClasses?: string;
  inputFeildClasses?: string;
  clearIconClasses?: string;
  prefixIconClasses?: string;
  inBetweenArrowIconClasses?: string;
  buttonClasses?: string;
  filterItemClasses?: string;
}
```

## Basic Usage

### Single Date Selection

```tsx
import React, { useState } from "react";
import { DatePicker } from "gends";

const BasicDatePicker = () => {
  const [selectedDates, setSelectedDates] = useState<Date[]>([]);

  return (
    <DatePicker
      type="single"
      label="Select Date"
      placeholder="Pick a date"
      selectedDates={selectedDates}
      onDateChangeHandler={setSelectedDates}
    />
  );
};
```

### Date Range Selection

```tsx
const DateRangePicker = () => {
  const [dateRange, setDateRange] = useState<Date[]>([]);

  return (
    <DatePicker
      type="range"
      label="Select Date Range"
      placeholder="Select start date ~ Select end date"
      selectedDates={dateRange}
      onDateChangeHandler={setDateRange}
    />
  );
};
```

## Size Variants

The DatePicker component supports three size variants with different dimensions and typography:

### Small (s)

- **Input Height**: 32px
- **Typography**: `text-en-desktop-body-s` (12px)
- **Use Case**: Compact forms, dense layouts

```tsx
<DatePicker size="s" label="Compact Date Picker" type="single" />
```

### Medium (m) - Default

- **Input Height**: 40px
- **Typography**: `text-en-desktop-body-m` (14px)
- **Use Case**: Standard forms, general use

```tsx
<DatePicker size="m" label="Standard Date Picker" type="single" />
```

### Large (l)

- **Input Height**: 48px
- **Typography**: `text-en-desktop-body-l` (16px)
- **Use Case**: Prominent forms, accessibility focus

```tsx
<DatePicker size="l" label="Large Date Picker" type="single" />
```

## Time Selection

### Date with Time Picker

```tsx
const DateTimeExample = () => {
  const [selectedDates, setSelectedDates] = useState<Date[]>([]);

  return (
    <DatePicker
      type="single"
      timer={true}
      label="Select Date & Time"
      placeholder="Pick date and time"
      selectedDates={selectedDates}
      onDateChangeHandler={setSelectedDates}
    />
  );
};
```

### Date Range with Time

```tsx
const DateRangeWithTimeExample = () => {
  const [dateRange, setDateRange] = useState<Date[]>([]);

  return (
    <DatePicker
      type="range"
      timer={true}
      label="Select Date Range & Time"
      selectedDates={dateRange}
      onDateChangeHandler={setDateRange}
    />
  );
};
```

## Predefined Filters

### Basic Filters

```tsx
import { addDays } from "date-fns";

const basicFilters = [
  {
    id: 0,
    label: "Custom",
    onSelect: (date: Date) => [],
  },
  {
    id: 1,
    label: "Today",
    onSelect: (date: Date) => [date],
  },
  {
    id: 2,
    label: "Yesterday",
    onSelect: (date: Date) => [addDays(date, -1)],
  },
  {
    id: 3,
    label: "Tomorrow",
    onSelect: (date: Date) => [addDays(date, 1)],
  },
];

const FilterExample = () => {
  const [dates, setDates] = useState<Date[]>([]);

  return (
    <DatePicker
      type="single"
      filters={basicFilters}
      label="Date with Filters"
      selectedDates={dates}
      onDateChangeHandler={setDates}
    />
  );
};
```

### Advanced Filters with Time

```tsx
const advancedFilters = [
  {
    id: 1,
    label: "Last 7 Days",
    onSelect: (date: Date) => [addDays(date, -7), date],
  },
  {
    id: 2,
    label: "Last 30 Days",
    onSelect: (date: Date) => [addDays(date, -30), date],
  },
  {
    id: 3,
    label: "Next 7 Days",
    onSelect: (date: Date) => [date, addDays(date, 7)],
  },
];

const AdvancedFilterExample = () => {
  const [dates, setDates] = useState<Date[]>([]);

  return (
    <DatePicker
      type="range"
      timer={true}
      filters={advancedFilters}
      label="Advanced Date Range with Time"
      selectedDates={dates}
      onDateChangeHandler={setDates}
    />
  );
};
```

## Validation States

### Success State

```tsx
<DatePicker
  type="single"
  validationState="success"
  validationMessage="Date selected successfully"
  label="Valid Date"
  supportText="Great choice for the event date"
/>
```

### Warning State

```tsx
<DatePicker
  type="single"
  validationState="warning"
  validationMessage="Please confirm this date selection"
  label="Date Needs Confirmation"
  supportText="This date falls on a weekend"
/>
```

### Error State

```tsx
<DatePicker
  type="single"
  validationState="error"
  validationMessage="Please select a valid date"
  label="Invalid Date"
  supportText="Date must be within the allowed range"
/>
```

### Default State

```tsx
<DatePicker
  type="single"
  validationState="default"
  label="Regular Date Picker"
  supportText="Select any date from the calendar"
/>
```

## Disabled and Read-only States

### Disabled Single Date Picker

```tsx
<DatePicker
  type="single"
  disabled={true}
  label="Disabled Date Picker"
  placeholder="Cannot select date"
  supportText="Date selection is currently disabled"
/>
```

### Disabled Range Date Picker

```tsx
<DatePicker
  type="range"
  disabled={true}
  label="Disabled Range Picker"
  placeholder="Cannot select date range"
/>
```

### Read-only Single Date Picker

```tsx
<DatePicker
  type="single"
  readOnly={true}
  label="Read-only Date Picker"
  selectedDates={[new Date()]}
  supportText="This date cannot be modified"
/>
```

### Read-only Range Date Picker

```tsx
const [startDate, endDate] = [new Date(), addDays(new Date(), 5)];

<DatePicker
  type="range"
  readOnly={true}
  label="Read-only Range Picker"
  selectedDates={[startDate, endDate]}
  supportText="This date range is fixed"
/>;
```

## Manual Input Features

### Enabled Manual Input (Default)

```tsx
<DatePicker
  type="single"
  allowManualInput={true}
  label="Manual Input Enabled"
  placeholder="Type DD/MM/YYYY or pick from calendar"
  supportText="You can type the date directly or use the calendar"
/>
```

### Disabled Manual Input

```tsx
<DatePicker
  type="single"
  allowManualInput={false}
  label="Calendar Only"
  placeholder="Use calendar to select date"
  supportText="Date can only be selected from the calendar"
/>
```

## Helper Text and Tooltips

### With Helper Text Tooltip

```tsx
<DatePicker
  type="single"
  label="Event Date"
  helperText="Select the date when the event will take place. This cannot be changed after confirmation."
  placeholder="Pick event date"
  supportText="Choose carefully as this affects all attendees"
/>
```

### Required Field

```tsx
<DatePicker
  type="single"
  required={true}
  label="Mandatory Date"
  placeholder="This field is required"
  validationMessage="Date selection is required to proceed"
  validationState="error"
/>
```

## Custom Styling

### Basic Custom Styling

```tsx
<DatePicker
  type="single"
  label="Custom Styled Date Picker"
  classNames={{
    inputFeildClasses: "border-blue-500 focus:border-blue-600",
    popoverContentClasses: "shadow-2xl border-blue-200",
    buttonClasses: "bg-blue-500 hover:bg-blue-600 text-white",
  }}
/>
```

### Advanced Custom Styling

```tsx
<DatePicker
  type="range"
  timer={true}
  label="Fully Customized Date Picker"
  classNames={{
    popoverTriggerClasses: "rounded-lg shadow-md",
    popoverContentClasses: "rounded-xl shadow-2xl border-gray-200",
    toolTipTriggerClasses: "text-blue-500 hover:text-blue-600",
    toolTipContentClasses: "bg-gray-900 text-white border-gray-700",
    inputFeildClasses: "border-2 border-gray-300 focus:border-blue-500",
    clearIconClasses: "text-red-500 hover:text-red-600",
    prefixIconClasses: "text-blue-500",
    buttonClasses:
      "bg-gradient-to-r from-blue-500 to-purple-600 hover:from-blue-600 hover:to-purple-700 text-white rounded-lg",
    filterItemClasses: "hover:bg-blue-50 text-blue-700 border-blue-200",
  }}
/>
```

## Custom Width and Layout

### Fixed Width

```tsx
<DatePicker type="single" width="300px" label="Fixed Width Date Picker" />
```

### Responsive Width

```tsx
<DatePicker
  type="range"
  width="100%"
  label="Full Width Date Range Picker"
  className="max-w-md mx-auto"
/>
```

## Prefix Icons

### With Custom Prefix Icon

```tsx
import { IcCalendar } from "gends";
<DatePicker
  type="single"
  label="Date with Custom Icon"
  prefixIcon={<IcCalendar className="h-4 w-4 text-blue-500" />}
  placeholder="Select date"
/>;
```

## Advanced Configuration

### Custom Props Configuration

```tsx
<DatePicker
  type="range"
  timer={true}
  label="Advanced Configuration"
  propsConfig={{
    calendarProps: {
      size: "l",
      // Additional calendar props
    },
    timePickerProps: {
      size: "m",
      // Additional time picker props
    },
    popoverContentProps: {
      side: "bottom",
      align: "start",
    },
    toolTipProps: {
      delayDuration: 500,
    },
  }}
/>
```

### Custom Date Formatter

```tsx
const customDateFormatter = (dates: (string | Date)[], isTime: boolean): string[] => {
  return dates.map(date => {
    if (date instanceof Date) {
      const formatted = date.toLocaleDateString("en-US", {
        year: "numeric",
        month: "short",
        day: "numeric",
      });

      if (isTime) {
        const time = date.toLocaleTimeString("en-US", {
          hour: "2-digit",
          minute: "2-digit",
        });
        return `${formatted} at ${time}`;
      }

      return formatted;
    }
    return String(date);
  });
};

<DatePicker
  type="single"
  timer={true}
  label="Custom Format Date Picker"
  dateFormatter={customDateFormatter}
/>;
```

## Integration Examples

### Form Integration

```tsx
import { useForm, Controller } from "react-hook-form";

const DatePickerForm = () => {
  const {
    control,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = data => {
    console.log("Selected dates:", data.dates);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <Controller
        name="dates"
        control={control}
        rules={{ required: "Date selection is required" }}
        render={({ field: { onChange, value } }) => (
          <DatePicker
            type="single"
            label="Event Date"
            selectedDates={value || []}
            onDateChangeHandler={onChange}
            validationState={errors.dates ? "error" : "default"}
            validationMessage={errors.dates?.message}
            required={true}
          />
        )}
      />

      <button type="submit" className="px-4 py-2 bg-blue-500 text-white rounded">
        Submit
      </button>
    </form>
  );
};
```

### Real-world Application Example

```tsx
const BookingDatePicker = () => {
  const [checkInOut, setCheckInOut] = useState<Date[]>([]);
  const [guests, setGuests] = useState(1);

  const hotelFilters = [
    {
      id: 1,
      label: "This Weekend",
      onSelect: (date: Date) => {
        const saturday = addDays(date, 6 - date.getDay());
        const sunday = addDays(saturday, 1);
        return [saturday, sunday];
      },
    },
    {
      id: 2,
      label: "Next Weekend",
      onSelect: (date: Date) => {
        const nextSaturday = addDays(date, 13 - date.getDay());
        const nextSunday = addDays(nextSaturday, 1);
        return [nextSaturday, nextSunday];
      },
    },
  ];

  return (
    <div className="bg-white p-6 rounded-lg shadow-lg max-w-md">
      <h2 className="text-xl font-semibold mb-4">Book Your Stay</h2>

      <DatePicker
        type="range"
        filters={hotelFilters}
        label="Check-in / Check-out"
        placeholder="Select your stay dates"
        selectedDates={checkInOut}
        onDateChangeHandler={setCheckInOut}
        supportText={`${
          checkInOut.length === 2
            ? `${Math.ceil((checkInOut[1].getTime() - checkInOut[0].getTime()) / (1000 * 60 * 60 * 24))} nights`
            : "Select your check-in and check-out dates"
        }`}
        size="l"
      />

      <div className="mt-4 pt-4 border-t">
        <p className="text-sm text-gray-600">
          {checkInOut.length === 2
            ? `Selected: ${checkInOut[0].toLocaleDateString()} - ${checkInOut[1].toLocaleDateString()}`
            : "Please select your travel dates"}
        </p>
      </div>
    </div>
  );
};
```

## Accessibility Features

The DatePicker component includes comprehensive accessibility support:

### Keyboard Navigation

- **Tab**: Navigate between input field, calendar, and controls
- **Enter/Space**: Open calendar popover and select dates
- **Escape**: Close calendar popover
- **Arrow Keys**: Navigate calendar dates when focused

### Screen Reader Support

- Proper ARIA labels and descriptions
- Date selection announcements
- Validation state communication
- Helper text accessibility

### Focus Management

- Clear focus indicators throughout the component
- Logical tab order through all interactive elements
- Focus trapping within the calendar popover

## Best Practices

### Do's ✅

- Always provide clear labels for form context
- Use appropriate size variants for your layout
- Implement proper validation with helpful error messages
- Consider using predefined filters for common date selections
- Provide helper text for complex date requirements
- Test with keyboard navigation and screen readers
- Use semantic validation states (success, warning, error)

### Don'ts ❌

- Don't disable manual input unless absolutely necessary
- Don't use overly complex filter logic that confuses users
- Don't forget to handle edge cases like leap years
- Don't implement custom date parsing without proper validation
- Don't use placeholder text as the only instruction
- Don't ignore mobile usability considerations

## Design Tokens

The DatePicker component uses Genesis Design System tokens:

### Colors

- **Border Colors**: `--gd-border` for default, validation state colors for validation
- **Background**: `--gd-background-surface-0` for inputs and popover
- **Text Colors**: `--gd-text-default`, `--gd-text-subdued-1`

### Typography

- **Small**: `text-en-desktop-body-s` (12px, 16px line height)
- **Medium**: `text-en-desktop-body-m` (14px, 20px line height)
- **Large**: `text-en-desktop-body-l` (16px, 24px line height)

### Spacing

- **Padding**: `gd-12`, `gd-16` for various component areas
- **Margins**: `gd-8`, `gd-12` for spacing between elements
- **Border Radius**: Component-specific radius from Genesis tokens

### Shadows

- **Popover Shadow**: `0px 4px 16px 0px #00000029` for calendar popover elevation

## Migration Guide

### From v1.x to v2.x

```tsx
// v1.x (deprecated)
<DatePicker
  mode="single"
  onChange={handleChange}
  showTime={true}
/>

// v2.x (current)
<DatePicker
  type="single"
  onDateChangeHandler={handleChange}
  timer={true}
/>
```

### Key Changes

- `mode` prop renamed to `type`
- `onChange` renamed to `onDateChangeHandler`
- `showTime` renamed to `timer`
- Added support for `filters`, `validationState`, and `classNames`
- Enhanced accessibility and keyboard navigation

## Troubleshooting

### Common Issues

**Date not updating**: Ensure you're using the controlled pattern with `selectedDates` and `onDateChangeHandler`.

**Manual input not working**: Check that `allowManualInput` is `true` and date format matches DD/MM/YYYY.

**Validation not showing**: Verify `validationState` and `validationMessage` are both provided.

**Calendar not opening**: Ensure component is not `disabled` or `readOnly` when interaction is expected.

**Time picker missing**: Confirm `timer={true}` is set for time selection functionality.

Remember: The DatePicker component is designed for flexible date selection with comprehensive features. Always test across different scenarios and user interaction patterns to ensure optimal user experience.
