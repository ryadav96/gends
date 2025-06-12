# Divider Component

## Overview

The Divider component is a versatile visual separator built on Radix UI's Separator primitive with Genesis Design System tokens. It provides flexible content separation with support for horizontal and vertical orientations, optional labels, interactive buttons, icon integration, and multiple styling variants. The component is perfect for structuring layouts, creating section breaks, and providing actionable separators with comprehensive accessibility features.

## Component API

### Divider Props

| Prop             | Type                                     | Default        | Description                                        |
| ---------------- | ---------------------------------------- | -------------- | -------------------------------------------------- |
| `orientation`    | `"horizontal" \| "vertical"`             | `"horizontal"` | Determines the direction of the divider line       |
| `withLabel`      | `boolean`                                | `false`        | Shows a text label in the center of the divider    |
| `label`          | `string`                                 | `"label"`      | Text content displayed in the center               |
| `button`         | `boolean`                                | `false`        | Converts the label into an interactive button      |
| `buttonType`     | `"primary" \| "secondary" \| "tertiary"` | `"tertiary"`   | Button variant when button mode is enabled         |
| `onButtonClick`  | `() => void`                             | `undefined`    | Click handler function for button interactions     |
| `prefixIcon`     | `React.ReactNode`                        | `<></>`        | Icon displayed before the label or button text     |
| `suffixIcon`     | `React.ReactNode`                        | `<></>`        | Icon displayed after the label or button text      |
| `bold`           | `boolean`                                | `false`        | Makes the label text bold (font-weight: 600)       |
| `dashed`         | `boolean`                                | `false`        | Uses dashed line style instead of solid            |
| `subtle`         | `boolean`                                | `true`         | Controls line color intensity (light vs dark)      |
| `className`      | `string`                                 | `undefined`    | Additional CSS classes for the container element   |
| `labelClassName` | `string`                                 | `undefined`    | Custom CSS classes for the label or button element |
| `lineClassName`  | `string`                                 | `undefined`    | Custom CSS classes for the separator line elements |
| `buttonProps`    | `ButtonProps`                            | `undefined`    | Additional props passed to the underlying Button   |

## Basic Usage

### Import

```tsx
import { Divider } from "gends";
```

### Simple Horizontal Divider

```tsx
const BasicDivider = () => {
  return (
    <div className="space-y-4">
      <p>First section content</p>
      <Divider />
      <p>Second section content</p>
    </div>
  );
};
```

### Simple Vertical Divider

```tsx
const VerticalDivider = () => {
  return (
    <div className="flex items-center gap-4">
      <span>Left content</span>
      <Divider orientation="vertical" className="h-8" />
      <span>Right content</span>
    </div>
  );
};
```

## Orientation Variants

### Horizontal Dividers

Horizontal dividers extend across the full width and are used for separating content vertically:

```tsx
// Basic horizontal divider
<Divider orientation="horizontal" />

// With spacing
<div className="my-8">
  <Divider orientation="horizontal" />
</div>

// Full-width section separator
<div className="w-full">
  <Divider orientation="horizontal" className="my-6" />
</div>
```

### Vertical Dividers

Vertical dividers extend vertically and are used for separating content horizontally:

```tsx
// Basic vertical divider
<div className="flex items-center">
  <div>Left content</div>
  <Divider orientation="vertical" className="h-16 mx-4" />
  <div>Right content</div>
</div>

// Sidebar separator
<div className="flex h-screen">
  <aside className="w-64 bg-gray-50 p-4">Sidebar content</aside>
  <Divider orientation="vertical" className="h-full" />
  <main className="flex-1 p-4">Main content</main>
</div>

// Inline content separator
<div className="flex items-center space-x-4">
  <span>Item 1</span>
  <Divider orientation="vertical" className="h-6" />
  <span>Item 2</span>
  <Divider orientation="vertical" className="h-6" />
  <span>Item 3</span>
</div>
```

## Label Variants

### Basic Text Labels

```tsx
// Simple label divider
<Divider withLabel label="OR" />

// Bold label
<Divider withLabel label="SECTION BREAK" bold />

// Custom styled label
<Divider
  withLabel
  label="Important Notice"
  bold
  labelClassName="text-blue-600 text-lg"
/>
```

### Label Examples

```tsx
// Authentication separator
<div className="space-y-4">
  <button className="w-full">Sign in with Google</button>
  <Divider withLabel label="OR" />
  <button className="w-full">Sign in with Email</button>
</div>

// Section separator
<div>
  <h2>Account Settings</h2>
  <Divider withLabel label="PERSONAL INFORMATION" bold className="my-6" />
  <form>...</form>
</div>

// Content grouping
<div className="space-y-6">
  <div>Recent items...</div>
  <Divider withLabel label="EARLIER" />
  <div>Older items...</div>
</div>
```

## Interactive Button Variants

### Button Types

The Divider component supports three button types when `button={true}`:

#### Tertiary Button (Default)

```tsx
<Divider
  button
  label="Show more"
  buttonType="tertiary"
  onButtonClick={() => console.log("Tertiary clicked")}
/>
```

#### Secondary Button

```tsx
<Divider
  button
  label="Load more items"
  buttonType="secondary"
  onButtonClick={() => console.log("Secondary clicked")}
/>
```

#### Primary Button

```tsx
<Divider
  button
  label="Add new item"
  buttonType="primary"
  onButtonClick={() => console.log("Primary clicked")}
/>
```

### Button Examples

```tsx
// Load more pattern
const LoadMoreDivider = () => {
  const [loading, setLoading] = useState(false);

  const handleLoadMore = async () => {
    setLoading(true);
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    setLoading(false);
  };

  return (
    <Divider
      button
      buttonType="secondary"
      label={loading ? "Loading..." : "Load more items"}
      onButtonClick={handleLoadMore}
      buttonProps={{ disabled: loading }}
    />
  );
};

// Add item pattern
const AddItemDivider = () => {
  const handleAddItem = () => {
    // Add item logic
    console.log("Adding new item");
  };

  return (
    <Divider
      button
      buttonType="primary"
      label="Add new task"
      onButtonClick={handleAddItem}
      className="my-4"
    />
  );
};
```

## Icon Integration

### Prefix Icons

```tsx
import { IcAdd, IcHeartRate } from "gends";

// Button with prefix icon
<Divider
  button
  label="Add item"
  buttonType="primary"
  prefixIcon={<IcAdd className="w-6 h-6 text-current" />}
  onButtonClick={() => console.log("Add clicked")}
/>

// Label with prefix icon
<Divider
  withLabel
  label="Favorites"
  prefixIcon={<IcHeartRate className="w-6 h-6 text-current" />}
  bold
/>
```

### Suffix Icons

```tsx
import { IcChevronDown , IcDownload  } from "gends";

// Button with suffix icon
<Divider
  button
  label="Download"
  buttonType="secondary"
  suffixIcon={<IcDownload className="w-6 h-6 text-current" />}
  onButtonClick={() => console.log("Download clicked")}
/>

// Expandable section indicator
<Divider
  button
  label="Advanced options"
  buttonType="tertiary"
  suffixIcon={<IcChevronDown className="w-6 h-6 text-current" />}
  onButtonClick={() => console.log("Expand clicked")}
/>
```

### Both Prefix and Suffix Icons

```tsx
import { IcStar, IcChevronRight } from "gends";

<Divider
  button
  label="Featured items"
  buttonType="secondary"
  prefixIcon={<IcStar className="w-6 h-6 text-current" />}
  suffixIcon={<IcChevronRight className="w-6 h-6 text-current" />}
  onButtonClick={() => console.log("Featured clicked")}
/>;
```

## Line Style Variants

### Solid Lines (Default)

```tsx
// Default solid line
<Divider />

// Solid line with label
<Divider withLabel label="Section" />

// Solid vertical line
<Divider orientation="vertical" className="h-8" />
```

### Dashed Lines

```tsx
// Dashed horizontal line
<Divider dashed />

// Dashed line with label
<Divider withLabel label="Optional Section" dashed />

// Dashed vertical line
<Divider orientation="vertical" dashed className="h-8" />
```

## Color Intensity Variants

### Subtle (Default)

Uses lighter border color (`border-color-neutral-grey-40`):

```tsx
// Subtle horizontal divider
<Divider subtle />

// Subtle with label
<Divider withLabel label="Subtle Section" subtle />
```

### Intense

Uses darker border color (`border-color-neutral-grey-60`):

```tsx
// Intense horizontal divider
<Divider subtle={false} />

// Intense with label
<Divider withLabel label="Important Section" subtle={false} bold />

// Intense dashed line
<Divider dashed subtle={false} />
```

## Advanced Usage Examples

### Authentication Flow

```tsx
const AuthenticationDivider = () => {
  return (
    <div className="max-w-md mx-auto space-y-4">
      <button className="w-full bg-blue-600 text-white py-2 rounded">Continue with Google</button>

      <Divider withLabel label="OR" className="my-6" />

      <form className="space-y-4">
        <input type="email" placeholder="Email" className="w-full p-2 border rounded" />
        <input type="password" placeholder="Password" className="w-full p-2 border rounded" />
        <button type="submit" className="w-full bg-gray-900 text-white py-2 rounded">
          Sign In
        </button>
      </form>
    </div>
  );
};
```

### Dashboard Section Separator

```tsx
const DashboardSections = () => {
  return (
    <div className="space-y-8">
      <section>
        <h2 className="text-xl font-semibold mb-4">Recent Activity</h2>
        <div>Recent activity content...</div>
      </section>

      <Divider withLabel label="ANALYTICS" bold subtle={false} className="my-8" />

      <section>
        <h2 className="text-xl font-semibold mb-4">Performance Metrics</h2>
        <div>Analytics content...</div>
      </section>

      <Divider
        button
        label="View detailed analytics"
        buttonType="secondary"
        onButtonClick={() => console.log("Navigate to analytics")}
        className="my-8"
      />
    </div>
  );
};
```

### List with Load More

```tsx
const ItemList = () => {
  const [items, setItems] = useState(Array.from({ length: 5 }, (_, i) => `Item ${i + 1}`));
  const [loading, setLoading] = useState(false);

  const handleLoadMore = async () => {
    setLoading(true);
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    const newItems = Array.from({ length: 3 }, (_, i) => `Item ${items.length + i + 1}`);
    setItems(prev => [...prev, ...newItems]);
    setLoading(false);
  };

  return (
    <div className="space-y-2">
      {items.map((item, index) => (
        <div key={index} className="p-3 bg-gray-50 rounded">
          {item}
        </div>
      ))}

      <Divider
        button
        buttonType="tertiary"
        label={loading ? "Loading..." : "Load more items"}
        onButtonClick={handleLoadMore}
        buttonProps={{ disabled: loading }}
        className="my-4"
      />
    </div>
  );
};
```

### Sidebar Layout

```tsx
const SidebarLayout = () => {
  return (
    <div className="flex h-screen">
      {/* Main sidebar */}
      <aside className="w-64 bg-gray-50 p-4">
        <nav className="space-y-2">
          <a href="#" className="block p-2 rounded hover:bg-gray-200">
            Dashboard
          </a>
          <a href="#" className="block p-2 rounded hover:bg-gray-200">
            Projects
          </a>
          <a href="#" className="block p-2 rounded hover:bg-gray-200">
            Tasks
          </a>
        </nav>

        <Divider withLabel label="ADMIN" className="my-6" />

        <nav className="space-y-2">
          <a href="#" className="block p-2 rounded hover:bg-gray-200">
            Users
          </a>
          <a href="#" className="block p-2 rounded hover:bg-gray-200">
            Settings
          </a>
        </nav>
      </aside>

      {/* Vertical divider */}
      <Divider orientation="vertical" className="h-full" />

      {/* Main content */}
      <main className="flex-1 p-6">
        <h1>Main Content Area</h1>
      </main>
    </div>
  );
};
```

## Custom Styling

### Basic Custom Styling

```tsx
<Divider
  withLabel
  label="Custom Styled"
  className="my-8"
  lineClassName="border-blue-500"
  labelClassName="text-blue-600 bg-white px-4"
/>
```

### Advanced Custom Styling

```tsx
<Divider
  button
  buttonType="primary"
  label="Custom Button"
  onButtonClick={() => console.log("Custom clicked")}
  className="my-6"
  lineClassName="border-gradient border-2"
  labelClassName="shadow-lg rounded-full"
  buttonProps={{
    className:
      "bg-gradient-to-r from-purple-500 to-pink-500 hover:from-purple-600 hover:to-pink-600",
  }}
/>
```

### Themed Dividers

```tsx
// Success theme
<Divider
  withLabel
  label="Success"
  bold
  lineClassName="border-green-500"
  labelClassName="text-green-700 bg-green-50 px-3 py-1 rounded"
/>

// Warning theme
<Divider
  withLabel
  label="Warning"
  bold
  lineClassName="border-yellow-500"
  labelClassName="text-yellow-700 bg-yellow-50 px-3 py-1 rounded"
/>

// Error theme
<Divider
  withLabel
  label="Error"
  bold
  lineClassName="border-red-500"
  labelClassName="text-red-700 bg-red-50 px-3 py-1 rounded"
/>
```

## Responsive Design

### Mobile-First Approach

```tsx
const ResponsiveDivider = () => {
  return (
    <div className="space-y-4">
      {/* Hide vertical divider on mobile, show horizontal */}
      <div className="flex flex-col md:flex-row md:items-center">
        <div className="flex-1">Left content</div>
        <Divider orientation="horizontal" className="md:hidden my-4" />
        <Divider orientation="vertical" className="hidden md:block h-8 mx-4" />
        <div className="flex-1">Right content</div>
      </div>

      {/* Responsive button labels */}
      <Divider
        button
        label="Show more"
        buttonType="secondary"
        onButtonClick={() => console.log("Clicked")}
        buttonProps={{
          className: "text-sm md:text-base px-3 md:px-4",
        }}
      />
    </div>
  );
};
```

## Accessibility Features

The Divider component provides comprehensive accessibility support:

### Semantic HTML

- Uses `<hr>` element semantically when appropriate
- Maintains proper document structure
- Provides meaningful content separation

### ARIA Support

```tsx
// Button with proper ARIA attributes
<Divider
  button
  label="Expand section"
  onButtonClick={() => console.log("Expanded")}
  buttonProps={{
    "aria-label": "Expand to show more items",
    "aria-expanded": "false"
  }}
/>

// Descriptive divider
<Divider
  withLabel
  label="End of search results"
  role="separator"
  aria-label="End of search results section"
/>
```

### Keyboard Navigation

- All interactive buttons are keyboard accessible
- Proper focus management and indicators
- Standard keyboard interaction patterns

### Screen Reader Support

- Clear content structure communication
- Proper labeling of interactive elements
- Semantic separation indication

## Design Tokens

The Divider component uses Genesis Design System tokens:

### Colors

- **Subtle Border**: `border-color-neutral-grey-40` (light gray)
- **Intense Border**: `border-color-neutral-grey-60` (darker gray)
- **Text Color**: `text-color-neutral-grey-80` for labels
- **Button Colors**: Inherited from Button component variants

### Typography

- **Font Size**: `text-m` (14px) for labels and buttons
- **Font Weight**: `font-600` when `bold` is true
- **Line Height**: Auto, maintaining Genesis Design System ratios

### Spacing

- **Padding**: `px-gd-8` (horizontal padding for labels)
- **Gap**: `gap-gd-8` for button spacing
- **Margins**: Flexible through className prop

### Button Integration

- **Size**: Always uses `size="s"` for consistency
- **Styling**: Inherits from Genesis Button component
- **Icons**: Proper spacing and alignment

## Best Practices

### Do's ✅

- Use horizontal dividers for content sections
- Use vertical dividers for inline content separation
- Provide clear, concise labels for context
- Use appropriate button types for actions
- Test with keyboard navigation and screen readers
- Consider responsive behavior across devices
- Use semantic HTML structure

### Don'ts ❌

- Don't overuse dividers in dense layouts
- Don't use dividers where spacing alone would suffice
- Don't make divider buttons primary actions in complex interfaces
- Don't ignore color contrast requirements
- Don't nest dividers unnecessarily
- Don't use decorative dividers for critical functionality

## Performance Considerations

### Optimization Tips

```tsx
// Good: Memoize expensive click handlers
const MemoizedDivider = memo(({ onAction, label }) => {
  const handleClick = useCallback(() => {
    onAction();
  }, [onAction]);

  return <Divider button label={label} onButtonClick={handleClick} />;
});

// Good: Conditional rendering for dynamic content
const ConditionalDivider = ({ showDivider, items }) => {
  if (!showDivider || items.length === 0) return null;

  return <Divider withLabel label={`${items.length} items`} />;
};
```

## Troubleshooting

### Common Issues

**Divider not visible**: Check that parent container has proper dimensions and the divider isn't hidden by overflow settings.

**Vertical divider not showing**: Ensure the parent container has a defined height and proper display properties (flex/grid).

**Button not clickable**: Verify `onButtonClick` is provided and `button={true}` is set.

**Styling not applying**: Check CSS specificity and ensure custom classes don't conflict with component styles.

**Icons not displaying**: Confirm icon components are properly imported and have appropriate sizing classes.

Remember: The Divider component is designed for flexible content separation with optional interactive features. Always consider the visual hierarchy and user experience when implementing dividers in your interfaces.

---

Consider using Divider with:

- **Button** — For consistent button styling in interactive dividers
- **Layout** — For structured content organization
- **Navigation** — For menu section separation
- **Forms** — For logical field grouping
- **Lists** — For content pagination and loading patterns
- **Cards** — For internal content separation
