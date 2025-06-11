# Calendar Component

## Overview

The Calendar component is a flexible date selection interface that supports single dates, multiple dates, and date ranges. Built with Genesis Design System tokens, it features three distinct views (date, month, year), multiple sizes, comprehensive date constraints, and extensive customization options. The component provides smooth navigation between different time periods and accessibility-compliant interactions.

## Component API

### Calendar Props

| Prop               | Type                                | Default  | Description                                            |
| ------------------ | ----------------------------------- | -------- | ------------------------------------------------------ |
| `type`             | `'single' \| 'multiple' \| 'range'` | Required | Date selection mode                                    |
| `size`             | `'s' \| 'm' \| 'l'`                 | `'m'`    | Visual size of the calendar                            |
| `handleDateChange` | `(selectedDates: Date[]) => void`   | -        | Callback function when dates are selected/changed      |
| `selectedDates`    | `Date[]`                            | `[]`     | Currently selected date(s)                             |
| `disableMinDate`   | `string`                            | -        | Minimum selectable date (ISO string format)            |
| `disableMaxDate`   | `string`                            | -        | Maximum selectable date (ISO string format)            |
| `excludeConfig`    | `DPExcludeConfig`                   | -        | Configuration for excluding specific dates or patterns |
| `classNames`       | `CustomClasses`                     | -        | Custom CSS classes for styling different parts         |

### Date Selection Types

```typescript
type DPDatesMode = "single" | "multiple" | "range";

type SelectedDates = Date[];

type DPDisableDateRange = {
  minDate?: Date;
  maxDate?: Date;
};
```

### Custom Classes Interface

```typescript
type CustomClasses = {
  container?: string; // Main calendar container
  actionableIcon?: string; // Navigation arrow buttons
  headingButton?: string; // Month/year header buttons
  dayGridContainer?: string; // Date grid layout
  monthGridContainer?: string; // Month selection grid
  yearGridContainer?: string; // Year selection grid
  weekGridContainer?: string; // Week headers container
  dayCell?: string; // Individual day cells
  monthCell?: string; // Individual month cells
  yearCell?: string; // Individual year cells
  weekCell?: string; // Weekday header cells
};
```

## Basic Usage

### Import Statement

```tsx
import { Calendar } from "gends";
```

### Single Date Selection

```tsx
const [selectedDate, setSelectedDate] = useState<Date[]>([]);

<Calendar type="single" selectedDates={selectedDate} handleDateChange={setSelectedDate} size="m" />;
```

### Multiple Date Selection

```tsx
const [selectedDates, setSelectedDates] = useState<Date[]>([]);

<Calendar
  type="multiple"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  size="m"
/>;
```

### Date Range Selection

```tsx
const [dateRange, setDateRange] = useState<Date[]>([]);

<Calendar type="range" selectedDates={dateRange} handleDateChange={setDateRange} size="m" />;
```

## Size Variants

### Small Calendar

```tsx
<Calendar
  type="single"
  size="s"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
/>
```

**Specifications:**

- **Container Width:** 272px
- **Font Size:** Small text scale
- **Button Size:** 20px navigation buttons
- **Use Cases:** Compact interfaces, mobile views, sidebar widgets

### Medium Calendar (Default)

```tsx
<Calendar
  type="single"
  size="m"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
/>
```

**Specifications:**

- **Container Width:** 308px
- **Font Size:** Medium text scale
- **Button Size:** 24px navigation buttons
- **Use Cases:** Standard date pickers, forms, modal dialogs

### Large Calendar

```tsx
<Calendar
  type="single"
  size="l"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
/>
```

**Specifications:**

- **Container Width:** 340px
- **Font Size:** Large text scale
- **Button Size:** 28px navigation buttons
- **Use Cases:** Dashboard views, desktop applications, prominent date selection

## Date Constraints & Validation

### Minimum and Maximum Dates

```tsx
<Calendar
  type="single"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  disableMinDate="2024-01-01"
  disableMaxDate="2024-12-31"
/>
```

### Exclude Specific Dates

```tsx
const excludeConfig = {
  excludeDates: ["2024-01-01", "2024-12-25"], // Holidays
  excludeWeekdays: [0, 6], // Exclude weekends (Sunday = 0, Saturday = 6)
};

<Calendar
  type="single"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  excludeConfig={excludeConfig}
/>;
```

### Business Days Only

```tsx
const businessDaysOnly = {
  excludeWeekdays: [0, 6], // Exclude weekends
  excludeDates: [
    "2024-01-01", // New Year
    "2024-07-04", // Independence Day
    "2024-12-25", // Christmas
  ],
};

<Calendar
  type="multiple"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  excludeConfig={businessDaysOnly}
/>;
```

## Navigation Views

### Date View (Default)

The primary view showing the calendar grid with individual dates.

```tsx
<Calendar type="single" selectedDates={selectedDates} handleDateChange={setSelectedDates} />
```

**Features:**

- Monthly grid layout with 7-day weeks
- Current month highlighting
- Previous/next month navigation
- Today indicator
- Selected date highlighting

### Month Selection View

Click on the month header to access month selection.

**Features:**

- 3x4 grid of month options
- Current month highlighting
- Direct month navigation
- Automatic switch to date view after selection

### Year Selection View

Click on the year header to access year selection.

**Features:**

- Scrollable year list
- 10-year range display
- Current year highlighting
- Direct year navigation
- Automatic switch to month view after selection

## Advanced Use Cases

### Event Booking Calendar

```tsx
const [bookingDates, setBookingDates] = useState<Date[]>([]);

const unavailableDates = [
  "2024-02-14", // Valentine's Day - fully booked
  "2024-02-15", // Following day - maintenance
];

<Calendar
  type="range"
  selectedDates={bookingDates}
  handleDateChange={setBookingDates}
  disableMinDate={new Date().toISOString().split("T")[0]} // No past dates
  excludeConfig={{ excludeDates: unavailableDates }}
  size="l"
  classNames={{
    container: "shadow-lg border border-gray-200",
    dayCell: "hover:bg-blue-50 transition-colors",
  }}
/>;
```

### Multi-Event Selection

```tsx
const [eventDates, setEventDates] = useState<Date[]>([]);

const handleEventSelection = (dates: Date[]) => {
  // Limit to maximum 5 events
  if (dates.length <= 5) {
    setEventDates(dates);
  }
};

<Calendar
  type="multiple"
  selectedDates={eventDates}
  handleDateChange={handleEventSelection}
  size="m"
  classNames={{
    dayCell: eventDates.length >= 5 ? "opacity-50" : "",
  }}
/>;

{
  eventDates.length >= 5 && (
    <p className="text-sm text-orange-600 mt-2">Maximum 5 events can be selected</p>
  );
}
```

### Vacation Planner

```tsx
const [vacationPeriod, setVacationPeriod] = useState<Date[]>([]);

const workingDays = {
  excludeWeekdays: [0, 6], // No weekends for vacation planning
};

<Calendar
  type="range"
  selectedDates={vacationPeriod}
  handleDateChange={setVacationPeriod}
  excludeConfig={workingDays}
  disableMinDate={new Date().toISOString().split("T")[0]}
  classNames={{
    container: "border-2 border-green-200",
    dayCell: "data-[selected]:bg-green-100",
  }}
/>;

{
  vacationPeriod.length === 2 && (
    <div className="mt-4 p-3 bg-green-50 rounded-lg">
      <p className="text-green-800">Vacation Period: {vacationPeriod.length} days selected</p>
    </div>
  );
}
```

### Appointment Scheduler

```tsx
const [appointmentDate, setAppointmentDate] = useState<Date[]>([]);

const availableSlots = {
  excludeWeekdays: [0], // No Sunday appointments
  excludeDates: getUnavailableDates(), // Function returning busy dates
};

<Calendar
  type="single"
  selectedDates={appointmentDate}
  handleDateChange={setAppointmentDate}
  disableMinDate={new Date().toISOString().split("T")[0]}
  disableMaxDate={getMaxBookingDate()} // 3 months in advance
  excludeConfig={availableSlots}
  size="l"
  classNames={{
    container: "bg-white shadow-xl rounded-lg",
    dayCell: "hover:bg-blue-50 focus:ring-2 focus:ring-blue-500",
  }}
/>;
```

## Custom Styling

### Theme Customization

```tsx
<Calendar
  type="single"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  classNames={{
    container: "bg-gradient-to-br from-blue-50 to-indigo-50 rounded-xl shadow-lg",
    actionableIcon: "text-indigo-600 hover:bg-indigo-100 rounded-full",
    headingButton: "text-indigo-800 hover:text-indigo-600 font-semibold",
    dayGridContainer: "gap-1",
    dayCell: cn(
      "rounded-lg transition-all duration-200",
      "hover:bg-indigo-100 hover:scale-105",
      "data-[selected]:bg-indigo-500 data-[selected]:text-white",
      "data-[today]:ring-2 data-[today]:ring-indigo-300"
    ),
    weekCell: "text-indigo-400 font-medium",
  }}
/>
```

### Compact Mobile Layout

```tsx
<Calendar
  type="single"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  size="s"
  classNames={{
    container: "w-full max-w-sm mx-auto rounded-lg border",
    dayGridContainer: "gap-0.5",
    dayCell: "text-xs p-1",
    weekCell: "text-xs p-1",
    actionableIcon: "w-6 h-6",
    headingButton: "text-sm",
  }}
/>
```

### Enterprise Dashboard Style

```tsx
<Calendar
  type="multiple"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  size="l"
  classNames={{
    container: "bg-gray-50 border-2 border-gray-200 rounded-lg",
    actionableIcon: "text-gray-600 hover:bg-gray-200",
    headingButton: "text-gray-800 font-bold",
    dayCell: cn(
      "border border-gray-100 hover:border-gray-300",
      "data-[selected]:bg-blue-600 data-[selected]:text-white",
      "data-[selected]:border-blue-600"
    ),
    weekCell: "bg-gray-100 text-gray-600 font-semibold",
    dayGridContainer: "border border-gray-200 rounded",
  }}
/>
```

## Integration Examples

### With Form Validation

```tsx
import { useForm, Controller } from "react-hook-form";

const BookingForm = () => {
  const {
    control,
    handleSubmit,
    formState: { errors },
  } = useForm();

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Controller
        name="checkInDate"
        control={control}
        rules={{ required: "Check-in date is required" }}
        render={({ field }) => (
          <div>
            <label className="block text-sm font-medium mb-2">Check-in Date</label>
            <Calendar
              type="single"
              selectedDates={field.value || []}
              handleDateChange={field.onChange}
              disableMinDate={new Date().toISOString().split("T")[0]}
              size="m"
            />
            {errors.checkInDate && (
              <p className="text-red-500 text-sm mt-1">{errors.checkInDate.message}</p>
            )}
          </div>
        )}
      />
    </form>
  );
};
```

### With External State Management

```tsx
import { useContext } from "react";
import { BookingContext } from "./BookingContext";

const BookingCalendar = () => {
  const { selectedDates, updateSelectedDates, unavailableDates } = useContext(BookingContext);

  return (
    <Calendar
      type="range"
      selectedDates={selectedDates}
      handleDateChange={updateSelectedDates}
      excludeConfig={{ excludeDates: unavailableDates }}
      size="l"
    />
  );
};
```

### With Custom Validation Logic

```tsx
const ValidatedCalendar = () => {
  const [selectedDates, setSelectedDates] = useState<Date[]>([]);
  const [error, setError] = useState<string>("");

  const handleDateChange = (dates: Date[]) => {
    setError("");

    // Custom validation: minimum 2 days notice
    if (dates.length > 0) {
      const selectedDate = dates[0];
      const twoDaysFromNow = new Date();
      twoDaysFromNow.setDate(twoDaysFromNow.getDate() + 2);

      if (selectedDate < twoDaysFromNow) {
        setError("Please select a date at least 2 days in advance");
        return;
      }
    }

    setSelectedDates(dates);
  };

  return (
    <div>
      <Calendar
        type="single"
        selectedDates={selectedDates}
        handleDateChange={handleDateChange}
        disableMinDate={new Date().toISOString().split("T")[0]}
        classNames={{
          container: error ? "border-red-500" : "border-gray-200",
        }}
      />
      {error && <p className="text-red-500 text-sm mt-2">{error}</p>}
    </div>
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Arrow Keys:** Navigate between dates in the calendar grid
- **Enter/Space:** Select the focused date
- **Tab:** Move between interactive elements (navigation buttons, month/year headers)
- **Escape:** Close any open view (month/year selection)

### Screen Reader Support

```tsx
<Calendar
  type="single"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  // Implicit ARIA attributes:
  // - role="application" on calendar container
  // - aria-selected on selected dates
  // - aria-disabled on disabled dates
  // - aria-current="date" on today
/>
```

### Focus Management

- Visual focus indicators on all interactive elements
- Logical tab order through calendar controls
- Focus restoration after view changes
- Clear focus boundaries for screen readers

## Technical Considerations

### Performance Optimization

```tsx
// Memoize expensive date calculations
const memoizedExcludeConfig = useMemo(
  () => ({
    excludeWeekdays: [0, 6],
    excludeDates: getHolidaysForYear(2024),
  }),
  []
);

<Calendar
  type="multiple"
  selectedDates={selectedDates}
  handleDateChange={setSelectedDates}
  excludeConfig={memoizedExcludeConfig}
/>;
```

### Date Formatting Considerations

```tsx
// Ensure consistent date handling
const formatDateForCalendar = (date: Date): string => {
  return date.toISOString().split("T")[0];
};

// Handle timezone considerations
const normalizeDate = (date: Date): Date => {
  return new Date(date.getFullYear(), date.getMonth(), date.getDate());
};
```

## Troubleshooting

### Common Issues

**Issue:** Selected dates not updating

```tsx
// ❌ Incorrect: Not handling state properly
<Calendar type="single" selectedDates={[]} />;

// ✅ Correct: Properly manage state
const [dates, setDates] = useState<Date[]>([]);
<Calendar type="single" selectedDates={dates} handleDateChange={setDates} />;
```

**Issue:** Date constraints not working

```tsx
// ❌ Incorrect: Wrong date format
<Calendar disableMinDate="01/01/2024" />

// ✅ Correct: ISO string format
<Calendar disableMinDate="2024-01-01" />
```

**Issue:** Custom styling not applied

```tsx
// ❌ Incorrect: Wrong class targeting
<Calendar classNames={{ day: "custom-style" }} />

// ✅ Correct: Use proper class names
<Calendar classNames={{ dayCell: "custom-style" }} />
```

## Best Practices

### Do's ✅

- Always provide `handleDateChange` callback for controlled components
- Use ISO date strings for `disableMinDate` and `disableMaxDate`
- Implement proper validation for date selection business rules
- Provide clear visual feedback for disabled and selected dates
- Test keyboard navigation and screen reader compatibility
- Consider mobile responsiveness when choosing size variants

### Don'ts ❌

- Don't mutate the `selectedDates` array directly
- Don't use local date formats for date constraints
- Don't rely solely on client-side validation for critical date logic
- Don't ignore timezone considerations in date handling
- Don't remove focus indicators without providing alternatives
- Don't implement date selection without proper error handling

## Component Relationships

Consider using Calendar with:

- **Button** — For triggering calendar popover or modal
- **Input** — For displaying selected dates in text form
- **Modal/Dialog** — For overlay calendar selection
- **Form** — For date input validation and submission
- **Popover** — For dropdown calendar interfaces
- **Badge** — For displaying selected date count or status

## Browser Support

- **Chrome/Edge:** Full support for all features
- **Firefox:** Full support for all features
- **Safari:** Full support for all features
- **Mobile Safari/Chrome:** Optimized touch interactions
- **Screen Readers:** NVDA, JAWS, VoiceOver compatible
