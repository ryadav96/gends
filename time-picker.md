# Time Picker Component

## Overview

The Time Picker component is a sophisticated time input control designed for forms requiring precise time selection. Built with Genesis Design System tokens, it supports both 12-hour and 24-hour formats, comprehensive validation states, and interactive dropdown interfaces. Perfect for scheduling applications, appointment systems, and any interface requiring structured time input with accessibility features and keyboard navigation support.

## Component API

### TimePicker Props

| Prop                | Type                                             | Default     | Description                                    |
| ------------------- | ------------------------------------------------ | ----------- | ---------------------------------------------- |
| `label`             | `string`                                         | -           | Input label text                               |
| `required`          | `boolean`                                        | `false`     | Shows required indicator (\*)                  |
| `value`             | `string`                                         | -           | Current time value (HH:MM or HH:MM AM/PM)      |
| `time24Format`      | `boolean`                                        | `false`     | Use 24-hour format instead of 12-hour          |
| `validationState`   | `'default' \| 'error' \| 'warning' \| 'success'` | `'default'` | Visual validation state                        |
| `placeholder`       | `string`                                         | `'HH:MM'`   | Placeholder text for input fields              |
| `helperText`        | `string`                                         | -           | Tooltip help text displayed with question mark |
| `size`              | `'s' \| 'm' \| 'l'`                              | `'m'`       | Component size affecting height and padding    |
| `disabled`          | `boolean`                                        | `false`     | Disables all interactions                      |
| `validationMessage` | `string`                                         | -           | Validation message text with appropriate icon  |
| `onChange`          | `(time: string) => void`                         | -           | Callback when time value changes               |
| `tooltipText`       | `string`                                         | -           | Additional tooltip text (legacy prop)          |
| `supportText`       | `string`                                         | -           | Supporting text displayed below component      |
| `autoCloseTimer`    | `number`                                         | `0`         | Auto-close timer for dropdowns (milliseconds)  |
| `dropdownProps`     | `DropdownProps`                                  | -           | Additional props passed to dropdown components |
| `classNames`        | `ClassNames`                                     | -           | Custom styling classes for different elements  |

### ClassNames Interface

```typescript
interface ClassNames {
  containerclass?: string; // Main container
  toolTipTriggerClass?: string; // Tooltip trigger icon
  toolTipContentClass?: string; // Tooltip content
  selectorContainerClass?: string; // AM/PM selector container
  selectorItemClass?: string; // AM/PM selector items
}
```

## Size Variants

The Time Picker offers three size variants optimized for different interface densities:

| Size | Height | Font Size | Padding   | Icon Size | Recommended Use Case    |
| ---- | ------ | --------- | --------- | --------- | ----------------------- |
| `s`  | 32px   | 14px      | 4px/12px  | 16×16     | Dense forms, compact UI |
| `m`  | 40px   | 14px      | 8px/12px  | 16×16     | Standard forms, default |
| `l`  | 48px   | 16px      | 12px/12px | 20×20     | Prominent inputs, touch |

```tsx
// Size comparison
<div className="space-y-4">
  <TimePicker label="Small Size" size="s" placeholder="HH:MM" />
  <TimePicker label="Medium Size" size="m" placeholder="HH:MM" />
  <TimePicker label="Large Size" size="l" placeholder="HH:MM" />
</div>
```

## Time Format Variants

### 12-Hour Format (Default)

Standard American time format with AM/PM selector.

- **Hour Range**: 1-12
- **Period Selector**: AM/PM toggle buttons
- **Output Format**: "HH:MM AM" or "HH:MM PM"
- **Use Cases**: Consumer applications, US-based systems

```tsx
<TimePicker
  label="Meeting Time"
  time24Format={false}
  value="02:30 PM"
  onChange={time => console.log(time)} // Output: "02:30 PM"
/>
```

### 24-Hour Format

International time format without AM/PM.

- **Hour Range**: 00-23
- **No Period Selector**: Direct hour entry
- **Output Format**: "HH:MM"
- **Use Cases**: International apps, military time, backend systems

```tsx
<TimePicker
  label="Departure Time"
  time24Format={true}
  value="14:30"
  onChange={time => console.log(time)} // Output: "14:30"
/>
```

## Validation States

### Default State

Standard appearance with no validation styling.

```tsx
<TimePicker label="Select Time" validationState="default" placeholder="HH:MM" />
```

### Success State

Green styling indicating successful validation.

```tsx
<TimePicker
  label="Valid Time"
  validationState="success"
  validationMessage="Time format is correct"
  value="09:30 AM"
/>
```

### Error State

Red styling indicating validation errors.

```tsx
<TimePicker
  label="Invalid Time"
  validationState="error"
  validationMessage="Please select a valid time"
  value=""
/>
```

### Warning State

Orange styling for warnings or cautions.

```tsx
<TimePicker
  label="Time Warning"
  validationState="warning"
  validationMessage="Selected time is outside business hours"
  value="11:45 PM"
/>
```

## Basic Usage

### Simple Time Picker

```tsx
import { TimePicker } from "gends";

const BasicExample = () => {
  const [selectedTime, setSelectedTime] = useState("");

  return (
    <TimePicker
      label="Appointment Time"
      value={selectedTime}
      onChange={setSelectedTime}
      placeholder="Select time"
      size="m"
    />
  );
};
```

### Required Field with Validation

```tsx
const RequiredExample = () => {
  const [time, setTime] = useState("");
  const [error, setError] = useState("");

  const handleTimeChange = (newTime: string) => {
    setTime(newTime);
    if (newTime) {
      setError("");
    } else {
      setError("Time is required");
    }
  };

  return (
    <TimePicker
      label="Meeting Time"
      required
      value={time}
      onChange={handleTimeChange}
      validationState={error ? "error" : "default"}
      validationMessage={error}
      helperText="Select your preferred meeting time"
    />
  );
};
```

## Advanced Features

### Time Format Switching

```tsx
const FormatSwitchExample = () => {
  const [time, setTime] = useState("14:30");
  const [is24Hour, setIs24Hour] = useState(true);

  const toggleFormat = () => {
    if (is24Hour) {
      // Convert 24h to 12h
      const [hour, minute] = time.split(":");
      const hourNum = parseInt(hour);
      const period = hourNum >= 12 ? "PM" : "AM";
      const displayHour = hourNum % 12 || 12;
      setTime(`${displayHour.toString().padStart(2, "0")}:${minute} ${period}`);
    } else {
      // Convert 12h to 24h
      const [timePart, period] = time.split(" ");
      const [hour, minute] = timePart.split(":");
      let hourNum = parseInt(hour);
      if (period === "PM" && hourNum !== 12) hourNum += 12;
      if (period === "AM" && hourNum === 12) hourNum = 0;
      setTime(`${hourNum.toString().padStart(2, "0")}:${minute}`);
    }
    setIs24Hour(!is24Hour);
  };

  return (
    <div className="space-y-4">
      <div className="flex items-center gap-2">
        <button onClick={toggleFormat} className="px-3 py-1 bg-blue-500 text-white rounded text-sm">
          Switch to {is24Hour ? "12-hour" : "24-hour"} format
        </button>
        <span className="text-sm text-gray-600">Current: {is24Hour ? "24-hour" : "12-hour"}</span>
      </div>

      <TimePicker
        label="Flexible Time Format"
        time24Format={is24Hour}
        value={time}
        onChange={setTime}
        placeholder={is24Hour ? "HH:MM" : "HH:MM AM/PM"}
      />
    </div>
  );
};
```

### Custom Styling and Classes

```tsx
const CustomStyledExample = () => {
  return (
    <TimePicker
      label="Custom Styled Time Picker"
      classNames={{
        containerclass: "bg-blue-50 p-4 rounded-lg",
        toolTipTriggerClass: "text-blue-600",
        toolTipContentClass: "bg-blue-900 text-white",
        selectorContainerClass: "bg-gradient-to-r from-blue-400 to-blue-600",
        selectorItemClass: "hover:bg-blue-200",
      }}
      supportText="Custom styling applied with Genesis tokens"
    />
  );
};
```

### Disabled State with Context

```tsx
const DisabledExample = () => {
  const [isBusinessHours, setIsBusinessHours] = useState(false);

  return (
    <div className="space-y-4">
      <div className="flex items-center gap-2">
        <input
          type="checkbox"
          id="businessHours"
          checked={isBusinessHours}
          onChange={e => setIsBusinessHours(e.target.checked)}
        />
        <label htmlFor="businessHours">Enable outside business hours</label>
      </div>

      <TimePicker
        label="Appointment Time"
        disabled={!isBusinessHours}
        value="18:30"
        time24Format={true}
        validationState={!isBusinessHours ? "warning" : "default"}
        validationMessage={!isBusinessHours ? "Only business hours appointments available" : ""}
        supportText="Business hours: 9:00 AM - 6:00 PM"
      />
    </div>
  );
};
```

### 3. Timer and Countdown Setup

```tsx
const TimerSetup = () => {
  const [timerSettings, setTimerSettings] = useState({
    workDuration: "25:00",
    shortBreak: "05:00",
    longBreak: "15:00",
    sessions: 4,
  });

  const [currentTimer, setCurrentTimer] = useState(null);
  const [timeLeft, setTimeLeft] = useState(0);
  const [isRunning, setIsRunning] = useState(false);

  const startTimer = (type, duration) => {
    const [minutes, seconds] = duration.split(":").map(Number);
    const totalSeconds = minutes * 60 + seconds;

    setCurrentTimer(type);
    setTimeLeft(totalSeconds);
    setIsRunning(true);
  };

  const formatTime = seconds => {
    const mins = Math.floor(seconds / 60);
    const secs = seconds % 60;
    return `${mins.toString().padStart(2, "0")}:${secs.toString().padStart(2, "0")}`;
  };

  const validateDuration = duration => {
    if (!duration) return false;
    const [minutes, seconds] = duration.split(":").map(Number);
    return minutes >= 1 && minutes <= 60 && seconds >= 0 && seconds < 60;
  };

  return (
    <div className="max-w-lg space-y-6">
      <h3 className="text-xl font-semibold">Pomodoro Timer Setup</h3>

      {currentTimer && (
        <div className="text-center p-6 bg-gradient-to-r from-blue-500 to-purple-600 text-white rounded-lg">
          <div className="text-sm opacity-90 mb-1">{currentTimer}</div>
          <div className="text-4xl font-mono font-bold">{formatTime(timeLeft)}</div>
          <button
            onClick={() => setIsRunning(!isRunning)}
            className="mt-3 px-4 py-2 bg-white text-blue-600 rounded-md font-medium"
          >
            {isRunning ? "Pause" : "Resume"}
          </button>
        </div>
      )}

      <div className="space-y-4">
        <TimePicker
          label="Work Duration"
          value={timerSettings.workDuration}
          onChange={value => setTimerSettings(prev => ({ ...prev, workDuration: value }))}
          time24Format={true}
          placeholder="MM:SS"
          size="m"
          validationState={validateDuration(timerSettings.workDuration) ? "success" : "error"}
          validationMessage={
            !validateDuration(timerSettings.workDuration) ? "Enter 1-60 minutes" : ""
          }
          helperText="Focus work session duration"
        />

        <TimePicker
          label="Short Break"
          value={timerSettings.shortBreak}
          onChange={value => setTimerSettings(prev => ({ ...prev, shortBreak: value }))}
          time24Format={true}
          placeholder="MM:SS"
          size="m"
          validationState={validateDuration(timerSettings.shortBreak) ? "success" : "error"}
          helperText="Break between work sessions"
        />

        <TimePicker
          label="Long Break"
          value={timerSettings.longBreak}
          onChange={value => setTimerSettings(prev => ({ ...prev, longBreak: value }))}
          time24Format={true}
          placeholder="MM:SS"
          size="m"
          validationState={validateDuration(timerSettings.longBreak) ? "success" : "error"}
          helperText="Extended break after session cycle"
        />

        <div className="flex gap-3 pt-4">
          <button
            onClick={() => startTimer("Work Session", timerSettings.workDuration)}
            className="flex-1 px-4 py-2 bg-green-600 text-white rounded-md font-medium"
          >
            Start Work
          </button>
          <button
            onClick={() => startTimer("Short Break", timerSettings.shortBreak)}
            className="flex-1 px-4 py-2 bg-blue-600 text-white rounded-md font-medium"
          >
            Short Break
          </button>
          <button
            onClick={() => startTimer("Long Break", timerSettings.longBreak)}
            className="flex-1 px-4 py-2 bg-purple-600 text-white rounded-md font-medium"
          >
            Long Break
          </button>
        </div>
      </div>
    </div>
  );
};
```

## Accessibility Features

The Time Picker component is built with comprehensive accessibility support:

### Keyboard Navigation

- **Tab**: Move focus between hour, minute, and AM/PM controls
- **Arrow Keys**: Navigate through dropdown options
- **Enter/Space**: Select dropdown option or toggle AM/PM
- **Escape**: Close open dropdowns

### Screen Reader Support

- Proper ARIA labels for all interactive elements
- Live region updates when time values change
- Descriptive text for validation states
- Helper text association with form controls

### Visual Accessibility

- High contrast color ratios for all text and borders
- Clear focus indicators with Genesis design tokens
- Consistent sizing for touch targets (minimum 44px)
- Color-blind friendly validation states

```tsx
// Accessibility-focused implementation
<TimePicker
  label="Appointment Time"
  helperText="Use arrow keys to navigate time options"
  validationMessage="Please select a time between 9 AM and 5 PM"
  supportText="Business hours only"
  aria-describedby="time-help time-validation"
/>
```

## Genesis Design System Integration

### Design Tokens

The Time Picker leverages Genesis design tokens for consistent theming:

```tsx
// Color tokens used internally
const timePickerTokens = {
  // Background colors
  background: "var(--gd-background-surface-0)",
  backgroundHover: "var(--gd-background-surface-10)",

  // Border colors
  border: "var(--gd-neutral-grey-40)",
  borderFocus: "var(--gd-primary-50)",
  borderError: "var(--gd-feedback-error-50)",

  // Text colors
  text: "var(--gd-text-default)",
  textSubdued: "var(--gd-text-subdued-1)",
  textError: "var(--gd-feedback-error-80)",

  // Spacing
  paddingHorizontal: "var(--gd-spacing-12)",
  paddingVertical: "var(--gd-spacing-8)",
  borderRadius: "var(--gd-border-radius-8)",
};
```

### Typography Scale

```tsx
// Typography tokens used
const typographyTokens = {
  label: "text-en-desktop-body-m-prominent", // 14px, weight 500
  input: "text-en-desktop-body-m", // 14px, weight 400
  helperText: "text-en-desktop-body-s", // 12px, weight 400
  validationText: "text-en-desktop-body-s", // 12px, weight 400
};
```

### Theme Support

```tsx
// Multi-theme support example
const ThemedTimePicker = ({ theme = "falcon" }) => (
  <div className={`theme-${theme}`}>
    <TimePicker
      label="Time with Theme"
      value="10:30 AM"
      classNames={{
        containerclass: `bg-[var(--gd-background-surface-0)] border-[var(--gd-border)]`,
        toolTipContentClass: `bg-[var(--gd-background-surface-20)] text-[var(--gd-text-default)]`,
      }}
    />
  </div>
);
```

## Best Practices

### Performance Optimization

```tsx
// Memoize expensive time calculations
const OptimizedTimePickerContainer = () => {
  const memoizedTimeOptions = useMemo(() => generateTimeOptions(), []);

  const debouncedOnChange = useMemo(() => debounce(time => console.log(time), 300), []);

  return (
    <TimePicker
      onChange={debouncedOnChange}
      // Pre-calculated options for better performance
    />
  );
};
```

### Form Integration Patterns

```tsx
// React Hook Form integration
const FormIntegratedTimePicker = () => {
  const {
    control,
    formState: { errors },
  } = useForm();

  return (
    <Controller
      name="appointmentTime"
      control={control}
      rules={{ required: "Time is required" }}
      render={({ field }) => (
        <TimePicker
          {...field}
          label="Appointment Time"
          validationState={errors.appointmentTime ? "error" : "default"}
          validationMessage={errors.appointmentTime?.message}
        />
      )}
    />
  );
};
```

### State Management

```tsx
// Efficient state management for multiple time pickers
const useTimePickerGroup = (initialTimes = {}) => {
  const [times, setTimes] = useReducer((state, action) => {
    switch (action.type) {
      case "SET_TIME":
        return { ...state, [action.field]: action.value };
      case "RESET_ALL":
        return initialTimes;
      case "VALIDATE_ALL":
        return { ...state, ...action.validatedTimes };
      default:
        return state;
    }
  }, initialTimes);

  const updateTime = useCallback((field, value) => {
    setTimes({ type: "SET_TIME", field, value });
  }, []);

  return { times, updateTime, setTimes };
};
```

## Common Pitfalls & Troubleshooting

### Time Format Validation

```tsx
// ❌ Incorrect: Not validating time format
const handleTimeChange = time => {
  setValue(time); // May contain invalid time
};

// ✅ Correct: Validate time format
const handleTimeChange = time => {
  if (isValidTimeFormat(time)) {
    setValue(time);
    setError("");
  } else {
    setError("Invalid time format");
  }
};

const isValidTimeFormat = time => {
  const timeRegex12 = /^(0?[1-9]|1[0-2]):[0-5][0-9]\s?(AM|PM)$/i;
  const timeRegex24 = /^([01]?[0-9]|2[0-3]):[0-5][0-9]$/;
  return timeRegex12.test(time) || timeRegex24.test(time);
};
```

### Performance Issues

```tsx
// ❌ Incorrect: Re-creating handlers on every render
const BadExample = () => {
  return (
    <TimePicker
      onChange={time => console.log(time)} // New function every render
    />
  );
};

// ✅ Correct: Memoized handlers
const GoodExample = () => {
  const handleTimeChange = useCallback(time => {
    console.log(time);
  }, []);

  return <TimePicker onChange={handleTimeChange} />;
};
```

### Accessibility Issues

```tsx
// ❌ Incorrect: Missing accessibility attributes
<TimePicker label="Time" />

// ✅ Correct: Comprehensive accessibility
<TimePicker
  label="Appointment Time"
  required
  helperText="Select your preferred appointment time"
  validationMessage="Please select a valid time"
  aria-describedby="time-help"
  id="appointment-time"
/>
```

## Migration Guide

### From Legacy Time Inputs

```tsx
// Legacy HTML time input
<input type="time" name="time" />

// Migrate to Genesis Time Picker
<TimePicker
  label="Select Time"
  name="time"
  time24Format={true}
  onChange={(value) => setValue(value)}
/>
```

### From Other Time Picker Libraries

```tsx
// React-datetime example
<DateTime
  timeFormat="HH:mm"
  dateFormat={false}
  onChange={handleChange}
/>

// Genesis Time Picker equivalent
<TimePicker
  time24Format={true}
  value={time}
  onChange={handleChange}
  placeholder="HH:MM"
/>
```

### TypeScript Integration

```tsx
interface AppointmentFormData {
  startTime: string;
  endTime: string;
  duration: number;
}

const TypedTimePickerExample: React.FC = () => {
  const [formData, setFormData] = useState<AppointmentFormData>({
    startTime: "",
    endTime: "",
    duration: 30,
  });

  const handleTimeChange = (field: keyof AppointmentFormData) => (value: string) => {
    setFormData(prev => ({ ...prev, [field]: value }));
  };

  return (
    <div>
      <TimePicker
        label="Start Time"
        value={formData.startTime}
        onChange={handleTimeChange("startTime")}
        required
      />
      <TimePicker
        label="End Time"
        value={formData.endTime}
        onChange={handleTimeChange("endTime")}
        required
      />
    </div>
  );
};
```

## Conclusion

The Genesis Time Picker component provides a robust, accessible, and flexible solution for time input across various applications. Its comprehensive API, validation states, and design system integration make it suitable for everything from simple appointment forms to complex scheduling systems. The component's keyboard navigation, screen reader support, and theme compatibility ensure a consistent user experience across all platforms and user needs.
