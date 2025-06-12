# Counter Badge Component

## Overview

The CounterBadge component is a specialized numeric display built on top of the Badge component, designed for displaying counts, notifications, and actionable numeric indicators. It provides consistent sizing patterns, multiple color variants, and optional interaction capabilities with comprehensive accessibility support. The component is perfect for notification counts, cart indicators, progress displays, and any numerical data that requires visual prominence.

## Component API

### CounterBadge Props

| Prop         | Type                                             | Default     | Description                                           |
| ------------ | ------------------------------------------------ | ----------- | ----------------------------------------------------- |
| `value`      | `string`                                         | `"99"`      | Numeric value or text to display in the badge         |
| `size`       | `'xxs' \| 'xs' \| 's' \| 'm' \| 'l'`             | `'m'`       | Size variant affecting dimensions and typography      |
| `color`      | `'default' \| 'success' \| 'error' \| 'warning'` | `'default'` | Color variant determining appearance theme            |
| `actionable` | `boolean`                                        | `false`     | Whether the badge is clickable and shows hover states |
| `subtle`     | `boolean`                                        | `false`     | Light background mode vs colored background mode      |
| `onClick`    | `(ev: MouseEvent<HTMLButtonElement>) => void`    | `() => {}`  | Click handler function when actionable is true        |
| `className`  | `string`                                         | `undefined` | Additional CSS classes for the container              |
| `classNames` | `classNames`                                     | `{}`        | Granular styling overrides object                     |

### ClassNames Interface

| Property     | Type         | Description                                    |
| ------------ | ------------ | ---------------------------------------------- |
| `className`  | `string`     | Custom CSS classes for container styling       |
| `badgeProps` | `BadgeProps` | Props passed to the underlying Badge component |

### Extended Props

The component also accepts all standard HTML div props and forwards them to the underlying Badge component.

## Basic Usage

### Import

```tsx
import { CounterBadge } from "gends";
```

### Simple Counter Badge

```tsx
const BasicCounterBadge = () => {
  return <CounterBadge value="5" />;
};
```

### With Click Handler

```tsx
const ClickableCounterBadge = () => {
  const [count, setCount] = useState(5);

  return (
    <CounterBadge value={count.toString()} actionable={true} onClick={() => setCount(count + 1)} />
  );
};
```

## Size Variants

The CounterBadge component supports five size variants with specific dimensions and typography:

### Size Specifications

| Size  | Height | Min Width | Font Size                | Padding    | Use Case                 |
| ----- | ------ | --------- | ------------------------ | ---------- | ------------------------ |
| `xxs` | 16px   | 22px      | desktop-body-xs          | 1px × 4px  | Ultra-compact indicators |
| `xs`  | 18px   | 24px      | desktop-body-s-prominent | 1px × 4px  | Small notification dots  |
| `s`   | 24px   | 34px      | desktop-body-m-prominent | 2px × 8px  | Standard notifications   |
| `m`   | 28px   | 38px      | desktop-body-m-prominent | 4px × 10px | Prominent counters       |
| `l`   | 32px   | 45px      | desktop-body-l-prominent | 4px × 12px | Large action indicators  |

### Size Examples

```tsx
// Extra Small - ultra-compact indicators
<CounterBadge size="xxs" value="1" />

// Small - notification dots
<CounterBadge size="xs" value="5" />

// Small - standard notifications
<CounterBadge size="s" value="12" />

// Medium - prominent counters (default)
<CounterBadge size="m" value="99" />

// Large - action indicators
<CounterBadge size="l" value="999+" />
```

### Size Comparison

```tsx
const SizeComparison = () => (
  <div className="flex gap-4 items-end flex-wrap">
    <CounterBadge value="5" size="xxs" />
    <CounterBadge value="12" size="xs" />
    <CounterBadge value="3" size="s" />
    <CounterBadge value="99" size="m" />
    <CounterBadge value="1000" size="l" />
  </div>
);
```

## Color Variants

The CounterBadge component supports four color variants with semantic meanings:

### Color Specifications

| Color     | Background (Subtle) | Background (Intense) | Text Color | Use Case               |
| --------- | ------------------- | -------------------- | ---------- | ---------------------- |
| `default` | Primary-20          | Primary-60           | Default    | Standard notifications |
| `success` | Success-20          | Success-50           | White      | Positive indicators    |
| `error`   | Error-20            | Error-50             | White      | Alert notifications    |
| `warning` | Warning-20          | Warning-50           | Default    | Warning indicators     |

### Color Examples

```tsx
// Default color - standard notifications
<CounterBadge color="default" value="3" />

// Success color - positive indicators
<CounterBadge color="success" value="5" />

// Error color - alert notifications
<CounterBadge color="error" value="12" />

// Warning color - warning indicators
<CounterBadge color="warning" value="7" />
```

### Color Variants Display

```tsx
const ColorVariants = () => (
  <div className="flex gap-4 flex-wrap">
    <CounterBadge value="5" color="default" />
    <CounterBadge value="12" color="success" />
    <CounterBadge value="3" color="error" />
    <CounterBadge value="99" color="warning" />
  </div>
);
```

## Appearance Modes

### Subtle vs Intense Styling

```tsx
// Subtle appearance - light background
<CounterBadge value="5" color="error" subtle={true} />

// Intense appearance - colored background (default)
<CounterBadge value="5" color="error" subtle={false} />
```

### Subtle Mode Examples

```tsx
const SubtleVariants = () => (
  <div className="flex gap-4 flex-wrap">
    <CounterBadge value="5" subtle />
    <CounterBadge value="12" color="success" subtle />
    <CounterBadge value="3" color="error" subtle />
    <CounterBadge value="99" color="warning" subtle />
  </div>
);
```

### Mode Comparison

```tsx
const ModeComparison = () => (
  <div className="space-y-4">
    <div className="flex gap-4">
      <span className="text-sm font-medium w-20">Intense:</span>
      <CounterBadge value="5" color="error" subtle={false} />
      <CounterBadge value="12" color="success" subtle={false} />
      <CounterBadge value="3" color="warning" subtle={false} />
    </div>
    <div className="flex gap-4">
      <span className="text-sm font-medium w-20">Subtle:</span>
      <CounterBadge value="5" color="error" subtle={true} />
      <CounterBadge value="12" color="success" subtle={true} />
      <CounterBadge value="3" color="warning" subtle={true} />
    </div>
  </div>
);
```

## Interactive Counter Badges

### Actionable Counters

When `actionable` is true, the counter badge becomes clickable with hover and focus states:

```tsx
const ActionableCounter = () => {
  const [count, setCount] = useState(5);

  return (
    <CounterBadge
      value={count.toString()}
      color="default"
      actionable={true}
      onClick={() => setCount(count + 1)}
    />
  );
};
```

### All Sizes Actionable

```tsx
const ActionableSizes = () => (
  <div className="flex gap-4 flex-wrap">
    <CounterBadge value="5" size="xxs" actionable onClick={() => console.log("Badge clicked")} />
    <CounterBadge value="12" size="xs" actionable onClick={() => console.log("Badge clicked")} />
    <CounterBadge value="3" size="s" actionable onClick={() => console.log("Badge clicked")} />
    <CounterBadge value="99" size="m" actionable onClick={() => console.log("Badge clicked")} />
    <CounterBadge value="1000" size="l" actionable onClick={() => console.log("Badge clicked")} />
  </div>
);
```

### Interactive States

Actionable counter badges automatically handle:

- **Hover**: Background color transition
- **Focus**: Focus ring with primary-60 color
- **Active**: Pressed state styling
- **Disabled**: Reduced opacity and pointer events disabled

## Common Usage Patterns

### Notification Counts

```tsx
const NotificationCounter = ({ count }) => {
  // Handle overflow with "99+" pattern
  const displayValue = count > 99 ? "99+" : count.toString();

  return <CounterBadge value={displayValue} color="error" size="s" subtle={false} />;
};
```

### Shopping Cart Items

```tsx
const CartCounter = ({ itemCount, onCartClick }) => {
  return (
    <CounterBadge
      value={itemCount.toString()}
      color="success"
      size="m"
      actionable={true}
      onClick={onCartClick}
    />
  );
};
```

### Progress Indicators

```tsx
const ProgressCounter = ({ current, total }) => {
  const isComplete = current === total;

  return (
    <CounterBadge
      value={`${current}/${total}`}
      color={isComplete ? "success" : "warning"}
      size="l"
      subtle={true}
    />
  );
};
```

### Conditional Display

```tsx
const ConditionalCounter = ({ count, showZero = false }) => {
  if (count === 0 && !showZero) {
    return null;
  }

  return (
    <CounterBadge value={count.toString()} color={count > 10 ? "error" : "default"} size="s" />
  );
};
```

## Advanced Usage

### Notification Bell with Counter

```tsx
const NotificationBell = ({ unreadCount }) => {
  return (
    <div className="relative">
      <button className="p-2 hover:bg-gray-100 rounded-full">
        <BellIcon className="h-6 w-6" />
      </button>
      {unreadCount > 0 && (
        <CounterBadge
          value={unreadCount > 99 ? "99+" : unreadCount.toString()}
          color="error"
          size="xs"
          subtle={false}
          className="absolute -top-1 -right-1"
        />
      )}
    </div>
  );
};
```

### Message Thread Counter

```tsx
const MessageThread = ({ messageCount, isUnread, onThreadClick }) => {
  return (
    <div
      className="flex items-center justify-between p-3 hover:bg-gray-50 cursor-pointer"
      onClick={onThreadClick}
    >
      <div className="flex-1">
        <h4 className="font-medium">Thread Title</h4>
        <p className="text-sm text-gray-600">Last message preview...</p>
      </div>
      <CounterBadge
        value={messageCount.toString()}
        color={isUnread ? "error" : "default"}
        size="s"
        subtle={!isUnread}
      />
    </div>
  );
};
```

### Status Dashboard Counters

```tsx
const StatusDashboard = ({ stats }) => {
  return (
    <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
      <div className="p-4 bg-white rounded-lg shadow">
        <div className="flex items-center justify-between">
          <span className="text-sm font-medium text-gray-600">Active</span>
          <CounterBadge value={stats.active.toString()} color="success" size="m" />
        </div>
      </div>

      <div className="p-4 bg-white rounded-lg shadow">
        <div className="flex items-center justify-between">
          <span className="text-sm font-medium text-gray-600">Pending</span>
          <CounterBadge value={stats.pending.toString()} color="warning" size="m" />
        </div>
      </div>

      <div className="p-4 bg-white rounded-lg shadow">
        <div className="flex items-center justify-between">
          <span className="text-sm font-medium text-gray-600">Errors</span>
          <CounterBadge value={stats.errors.toString()} color="error" size="m" />
        </div>
      </div>

      <div className="p-4 bg-white rounded-lg shadow">
        <div className="flex items-center justify-between">
          <span className="text-sm font-medium text-gray-600">Total</span>
          <CounterBadge value={stats.total.toString()} color="default" size="m" subtle={true} />
        </div>
      </div>
    </div>
  );
};
```

### Interactive Counter with Actions

```tsx
const InteractiveCounter = () => {
  const [count, setCount] = useState(0);
  const [history, setHistory] = useState([]);

  const handleIncrement = () => {
    const newCount = count + 1;
    setCount(newCount);
    setHistory(prev => [...prev, { action: "increment", value: newCount, timestamp: new Date() }]);
  };

  const handleDecrement = () => {
    const newCount = Math.max(0, count - 1);
    setCount(newCount);
    setHistory(prev => [...prev, { action: "decrement", value: newCount, timestamp: new Date() }]);
  };

  const handleReset = () => {
    setCount(0);
    setHistory([]);
  };

  return (
    <div className="space-y-4">
      <div className="flex items-center gap-4">
        <button
          onClick={handleDecrement}
          className="px-3 py-1 bg-red-100 text-red-700 rounded hover:bg-red-200"
          disabled={count === 0}
        >
          -
        </button>

        <CounterBadge
          value={count.toString()}
          color={count > 10 ? "error" : count > 5 ? "warning" : "default"}
          size="l"
          actionable={true}
          onClick={handleIncrement}
        />

        <button
          onClick={handleIncrement}
          className="px-3 py-1 bg-green-100 text-green-700 rounded hover:bg-green-200"
        >
          +
        </button>

        <button
          onClick={handleReset}
          className="px-3 py-1 bg-gray-100 text-gray-700 rounded hover:bg-gray-200"
        >
          Reset
        </button>
      </div>

      <div className="text-xs text-gray-500">
        Click the counter to increment, or use the buttons
      </div>

      {history.length > 0 && (
        <div className="text-xs text-gray-400">
          Last action: {history[history.length - 1].action} at{" "}
          {history[history.length - 1].timestamp.toLocaleTimeString()}
        </div>
      )}
    </div>
  );
};
```

## Custom Styling

### Basic Custom Styling

```tsx
const CustomStyledCounter = () => (
  <CounterBadge
    value="42"
    color="default"
    size="m"
    className="shadow-lg border-2 border-blue-200"
  />
);
```

### Advanced Custom Styling

```tsx
const AdvancedCustomCounter = () => (
  <CounterBadge
    value="99+"
    color="error"
    size="l"
    actionable={true}
    onClick={() => console.log("Custom styled counter clicked")}
    classNames={{
      className: "shadow-xl border-2 border-red-300 hover:shadow-2xl transition-all duration-200",
      badgeProps: {
        classNames: {
          textClasses: "font-bold tracking-wide",
        },
      },
    }}
  />
);
```

### Animated Counter

```tsx
const AnimatedCounter = ({ value }) => {
  const [displayValue, setDisplayValue] = useState(value);
  const [isAnimating, setIsAnimating] = useState(false);

  useEffect(() => {
    if (value !== displayValue) {
      setIsAnimating(true);
      const timer = setTimeout(() => {
        setDisplayValue(value);
        setIsAnimating(false);
      }, 150);
      return () => clearTimeout(timer);
    }
  }, [value, displayValue]);

  return (
    <CounterBadge
      value={displayValue.toString()}
      color="success"
      size="m"
      className={`transition-transform duration-150 ${isAnimating ? "scale-110" : "scale-100"}`}
    />
  );
};
```

## Design Tokens & Styling

### Color Specifications

| Color Variant | Subtle Background | Intense Background | Text Color | Border |
| ------------- | ----------------- | ------------------ | ---------- | ------ |
| Default       | `primary-20`      | `primary-60`       | Auto       | None   |
| Success       | `success-20`      | `success-50`       | White      | None   |
| Error         | `error-20`        | `error-50`         | White      | None   |
| Warning       | `warning-20`      | `warning-50`       | Auto       | None   |

### Interactive States

| State               | Background          | Text             | Border           |
| ------------------- | ------------------- | ---------------- | ---------------- |
| Default             | Based on color/mode | Based on color   | None             |
| Hover (actionable)  | `surface-30`        | `text-subdued-1` | None             |
| Focus (actionable)  | Based on color/mode | Based on color   | 4px `primary-60` |
| Active (actionable) | Darker variant      | Based on color   | None             |
| Disabled            | `surface-30`        | `text-subdued-2` | None             |

### Typography & Spacing

| Size  | Font Class                 | Line Height | Letter Spacing | Border Radius |
| ----- | -------------------------- | ----------- | -------------- | ------------- |
| `xxs` | `desktop-body-xs`          | Auto        | Normal         | `9999px`      |
| `xs`  | `desktop-body-s-prominent` | Auto        | Normal         | `9999px`      |
| `s`   | `desktop-body-m-prominent` | Auto        | Normal         | `9999px`      |
| `m`   | `desktop-body-m-prominent` | Auto        | Normal         | `9999px`      |
| `l`   | `desktop-body-l-prominent` | Auto        | Normal         | `9999px`      |

### Dimensions

All counter badges use a circular border radius (`border-radius: 9999px`) and have minimum widths to ensure proper circular appearance even with single digits.

## Accessibility Features

The CounterBadge component provides comprehensive accessibility support:

### ARIA Attributes

- `role="button"` when actionable is true
- `aria-label` for screen reader context
- `tabindex="0"` for keyboard navigation when actionable
- `aria-disabled` when disabled

### Keyboard Navigation

- **Tab**: Focus the counter badge (when actionable)
- **Enter**: Activate the click handler (when actionable)
- **Space**: Activate the click handler (when actionable)

### Screen Reader Support

```tsx
// Proper labeling for screen readers
<CounterBadge
  value="5"
  color="error"
  actionable={true}
  onClick={handleNotificationClick}
  aria-label="5 unread notifications, click to view"
/>

// Descriptive labeling for complex counters
<CounterBadge
  value="3/10"
  color="warning"
  aria-label="3 out of 10 tasks completed"
/>
```

## Best Practices

### Value Formatting

```tsx
// Good: Handle overflow gracefully
const formatCount = (count) => {
  if (count > 999) return "999+";
  if (count > 99) return "99+";
  return count.toString();
};

// Good: Use semantic colors
<CounterBadge
  value={formatCount(unreadCount)}
  color={unreadCount > 10 ? "error" : "default"}
/>

// Avoid: Raw large numbers
<CounterBadge value="1234567" /> // Hard to read
```

### Semantic Usage

```tsx
// Good: Use appropriate colors for context
<CounterBadge color="error" value="3" />    // Errors/alerts
<CounterBadge color="success" value="5" />  // Completions/success
<CounterBadge color="warning" value="2" />  // Warnings/pending
<CounterBadge color="default" value="8" />  // Neutral counts

// Good: Size appropriate to context
<CounterBadge size="xs" value="1" />  // Subtle indicators
<CounterBadge size="l" value="99+" /> // Important counters
```

### Performance Considerations

```tsx
// Good: Memoize expensive formatting
const FormattedCounter = memo(({ count, onClick }) => {
  const formattedValue = useMemo(() => (count > 99 ? "99+" : count.toString()), [count]);

  return <CounterBadge value={formattedValue} actionable={!!onClick} onClick={onClick} />;
});

// Good: Avoid unnecessary re-renders
const NotificationBadge = ({ notifications }) => {
  const count = useMemo(() => notifications.filter(n => !n.read).length, [notifications]);

  if (count === 0) return null;

  return <CounterBadge value={count.toString()} color="error" />;
};
```

## Troubleshooting

### Common Issues

**Counter badge not showing:**

- Verify `value` prop is provided and not empty
- Check if parent container has proper positioning
- Ensure no CSS is hiding the component

**Click handler not working:**

- Confirm `actionable={true}` is set
- Verify `onClick` function is properly defined
- Check for event propagation issues

**Styling not applying:**

- Ensure custom classes don't conflict with component styles
- Use `classNames` prop for granular control
- Check CSS specificity if overrides aren't working

**Text overflow in small sizes:**

- Use appropriate size for content length
- Format long numbers with "+" notation
- Consider abbreviating text content

### Performance Issues

```tsx
// Good: Optimize frequent updates
const OptimizedCounter = ({ count }) => {
  const debouncedCount = useDebounce(count, 100);

  return <CounterBadge value={debouncedCount.toString()} color="default" />;
};

// Good: Lazy load heavy components
const LazyCounterDashboard = lazy(() => import("./CounterDashboard"));
```

## Integration Examples

### With Navigation

```tsx
const NavigationWithCounters = () => {
  const { unreadMessages, pendingTasks, alerts } = useNotifications();

  return (
    <nav className="flex space-x-6">
      <NavItem href="/messages" label="Messages">
        {unreadMessages > 0 && (
          <CounterBadge
            value={unreadMessages.toString()}
            color="error"
            size="xs"
            className="ml-2"
          />
        )}
      </NavItem>

      <NavItem href="/tasks" label="Tasks">
        {pendingTasks > 0 && (
          <CounterBadge
            value={pendingTasks.toString()}
            color="warning"
            size="xs"
            className="ml-2"
          />
        )}
      </NavItem>

      <NavItem href="/alerts" label="Alerts">
        {alerts > 0 && (
          <CounterBadge value={alerts.toString()} color="success" size="xs" className="ml-2" />
        )}
      </NavItem>
    </nav>
  );
};
```

### With Data Tables

```tsx
const DataTableWithCounters = ({ rows }) => {
  return (
    <table className="w-full">
      <thead>
        <tr>
          <th>Category</th>
          <th>Count</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        {rows.map(row => (
          <tr key={row.id}>
            <td>{row.category}</td>
            <td>
              <CounterBadge
                value={row.count.toString()}
                color={row.status === "error" ? "error" : "default"}
                size="s"
              />
            </td>
            <td>{row.status}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
};
```

---

Consider using CounterBadge with:

- **Badge** — For extended badge variants and text content
- **Button** — For actionable counter integrations
- **IconButton** — For icon-based counter displays
- **Notification** — For alert and notification systems
- **Navigation** — For menu item counters and indicators
- **Card** — For metric displays and status indicators
