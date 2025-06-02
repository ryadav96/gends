# Calendar

A flexible and accessible calendar component built on top of react-day-picker. It provides a clean interface for date selection with support for single dates, date ranges, and custom styling.

---

## 1. Quick start

```tsx
import { Calendar } from "gends";

function Example() {
  return (
    <Calendar mode="single" selected={date} onSelect={setDate} className="rounded-md border" />
  );
}
```

---

## 2. Selection Modes

The Calendar component supports different selection modes:

| Mode       | Description                      | Use case                   |
| ---------- | -------------------------------- | -------------------------- |
| `single`   | Select a single date             | Date picker, appointments  |
| `range`    | Select a range of dates          | Booking periods, vacations |
| `multiple` | Select multiple individual dates | Event scheduling           |

```tsx
// Single date selection
<Calendar
  mode="single"
  selected={date}
  onSelect={setDate}
/>

// Date range selection
<Calendar
  mode="range"
  selected={dateRange}
  onSelect={setDateRange}
/>

// Multiple dates selection
<Calendar
  mode="multiple"
  selected={dates}
  onSelect={setDates}
/>
```

---

## 3. Navigation

Customize the calendar navigation:

```tsx
// Basic navigation
<Calendar
  showOutsideDays={true}
  fixedWeeks={true}
/>

// Custom navigation buttons
<Calendar
  components={{
    IconLeft: ({ ...props }) => <CustomLeftIcon {...props} />,
    IconRight: ({ ...props }) => <CustomRightIcon {...props} />
  }}
/>
```

---

## 4. Date Constraints

Set constraints on date selection:

```tsx
// Disable past dates
<Calendar
  disabled={{ before: new Date() }}
/>

// Disable specific dates
<Calendar
  disabled={[
    new Date(2024, 0, 1),
    new Date(2024, 0, 2)
  ]}
/>

// Disable date ranges
<Calendar
  disabled={{
    from: new Date(2024, 0, 1),
    to: new Date(2024, 0, 7)
  }}
/>
```

---

## 5. Custom Styling

Apply custom styles to different parts of the calendar:

```tsx
<Calendar
  className="custom-calendar"
  classNames={{
    months: "flex flex-col sm:flex-row space-y-4",
    month: "space-y-4",
    caption: "flex justify-center pt-1 relative items-center",
    caption_label: "text-sm font-medium",
    nav: "space-x-1 flex items-center",
    table: "w-full border-collapse space-y-1",
    head_row: "flex",
    head_cell: "text-muted-foreground rounded-md w-9 font-normal text-[0.8rem]",
    row: "flex w-full mt-2",
    cell: "text-center text-sm p-0 relative",
    day: "h-9 w-9 p-0 font-normal aria-selected:opacity-100",
  }}
/>
```

---

## 6. Full Prop Reference

### Basic Props

| Prop              | Type                                                                                     | Default    | Description                        |
| ----------------- | ---------------------------------------------------------------------------------------- | ---------- | ---------------------------------- |
| `mode`            | `'single' \| 'range' \| 'multiple'`                                                      | `'single'` | Selection mode                     |
| `selected`        | `Date \| Date[] \| DateRange`                                                            | -          | Selected date(s)                   |
| `onSelect`        | `(date: Date \| Date[] \| DateRange) => void`                                            | -          | Selection handler                  |
| `disabled`        | `Date \| Date[] \| DateRange \| { before?: Date; after?: Date; from?: Date; to?: Date }` | -          | Disabled dates                     |
| `showOutsideDays` | `boolean`                                                                                | `true`     | Show days from previous/next month |
| `fixedWeeks`      | `boolean`                                                                                | `false`    | Always show 6 weeks                |

### Navigation Props

| Prop        | Type     | Default | Description               |
| ----------- | -------- | ------- | ------------------------- |
| `fromDate`  | `Date`   | -       | Start date for navigation |
| `toDate`    | `Date`   | -       | End date for navigation   |
| `fromMonth` | `Date`   | -       | First month to display    |
| `toMonth`   | `Date`   | -       | Last month to display     |
| `fromYear`  | `number` | -       | First year to display     |
| `toYear`    | `number` | -       | Last year to display      |

### Styling Props

| Prop         | Type     | Default | Description                             |
| ------------ | -------- | ------- | --------------------------------------- |
| `className`  | `string` | -       | Additional CSS classes for the calendar |
| `classNames` | `object` | -       | Custom class names for different parts  |

### Component Props

| Prop         | Type     | Default | Description                          |
| ------------ | -------- | ------- | ------------------------------------ |
| `components` | `object` | -       | Custom components for calendar parts |

---

## 7. Recipes

### Date Picker with Range

```tsx
const [range, setRange] = useState<DateRange | undefined>();

<Calendar
  mode="range"
  selected={range}
  onSelect={setRange}
  numberOfMonths={2}
  showOutsideDays={true}
/>;
```

### Multiple Month View

```tsx
<Calendar mode="single" selected={date} onSelect={setDate} numberOfMonths={3} pagedNavigation />
```

### Disabled Weekends

```tsx
<Calendar
  mode="single"
  selected={date}
  onSelect={setDate}
  disabled={date => {
    const day = date.getDay();
    return day === 0 || day === 6;
  }}
/>
```

### Custom Styled Calendar

```tsx
<Calendar
  mode="single"
  selected={date}
  onSelect={setDate}
  className="rounded-lg border shadow-lg"
  classNames={{
    day_selected:
      "bg-primary text-primary-foreground hover:bg-primary hover:text-primary-foreground",
    day_today: "bg-accent text-accent-foreground",
    day_outside: "text-muted-foreground opacity-50",
  }}
/>
```

---

## 8. Accessibility

The Calendar component includes several accessibility features:

- Proper ARIA attributes for date selection
- Keyboard navigation support:
  - Arrow keys: Navigate between dates
  - Enter/Space: Select date
  - Tab: Move between interactive elements
- Screen reader announcements for selected dates
- Focus management
- Proper heading hierarchy

```tsx
<Calendar
  mode="single"
  selected={date}
  onSelect={setDate}
  aria-label="Select date"
  role="application"
/>
```

---

## 9. Design Tokens

The Calendar component uses the following design system tokens:

**Spacing:**

- Container padding: `p-3`
- Month spacing: `space-y-4`
- Cell dimensions: `h-9 w-9`
- Navigation button size: `h-7 w-7`

**Typography:**

- Caption: `text-sm font-medium`
- Day numbers: `text-sm`
- Weekday headers: `text-[0.8rem]`

**Colors:**

- Selected day: `bg-primary text-primary-foreground`
- Today: `bg-accent text-accent-foreground`
- Outside days: `text-muted-foreground`
- Disabled days: `opacity-50`

**Layout:**

- Border radius: `rounded-md`
- Table layout: `border-collapse`
- Flex layout: `flex flex-col sm:flex-row`

**Transitions:**

- Hover opacity: `opacity-50 hover:opacity-100`

---

Consider using Calendar with:

- **Button** — For navigation controls
- **Input** — For date input fields
- **Popover** — For dropdown calendar
- **Form** — For date selection in forms
- **DatePicker** — For combined input and calendar
- **DateRangePicker** — For range selection
