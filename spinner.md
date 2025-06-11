# Spinner Component

## Overview

The Spinner component is a versatile and accessible loading indicator that provides smooth circular animation to communicate ongoing processes to users. Built with Genesis Design System tokens and optimized SVG graphics, it offers five size variants, customizable colors, label positioning, and extensive styling options. The component ensures optimal user experience with proper accessibility features and seamless integration across different contexts.

## Component API

### Spinner Props

| Prop               | Type                                     | Default                       | Description                                     |
| ------------------ | ---------------------------------------- | ----------------------------- | ----------------------------------------------- |
| size               | `"xs" \| "s" \| "m" \| "l" \| "xl"`      | `"m"`                         | Size variant determining dimensions and spacing |
| customSize         | `string`                                 | `""`                          | Custom size override (e.g., "32px", "2rem")     |
| color              | `string`                                 | `"var(--gd-primary-50)"`      | Active spinner arc color                        |
| background         | `string`                                 | `"var(--gd-neutral-grey-40)"` | Background track color                          |
| label              | `string`                                 | `""`                          | Loading text label                              |
| position           | `"top" \| "bottom" \| "left" \| "right"` | `"bottom"`                    | Label position relative to spinner              |
| labelClassName     | `string`                                 | `undefined`                   | Additional CSS classes for label                |
| labelStyle         | `CSSProperties`                          | `{}`                          | Inline styles for label                         |
| containerClassName | `string`                                 | `undefined`                   | Additional CSS classes for container            |
| containerStyle     | `CSSProperties`                          | `{}`                          | Inline styles for container                     |
| ...props           | `React.HTMLAttributes<HTMLDivElement>`   | `{}`                          | All standard div HTML attributes                |

### TypeScript Interface

```typescript
export interface LoaderProps {
  size?: "xs" | "s" | "m" | "l" | "xl";
  customSize?: string;
  color?: string;
  background?: string;
  label?: string;
  position?: "top" | "bottom" | "left" | "right";
  labelClassName?: string;
  labelStyle?: CSSProperties;
  containerClassName?: string;
  containerStyle?: CSSProperties;
}
```

### Import Statement

```typescript
import { Spinner } from "gends";
```

## Basic Usage

### Default Spinner

```tsx
import { Spinner } from "gends";

function MyComponent() {
  return <Spinner />;
}
```

## Size Variants

### All Available Sizes

| Size | Dimensions | Font Size | Label Gap | Stroke Width | Use Case                          |
| ---- | ---------- | --------- | --------- | ------------ | --------------------------------- |
| xs   | 12×12px    | 12px/16px | 4px       | 2.25px       | Inline text, compact spaces       |
| s    | 16×16px    | 14px/20px | 8px       | 3px          | Small buttons, tight layouts      |
| m    | 24×24px    | 16px/24px | 12px      | 4px          | Default size, general use         |
| l    | 40×40px    | 18px/24px | 16px      | 5px          | Large buttons, prominent sections |
| xl   | 48×48px    | 18px/24px | 16px      | 6px          | Full-page loading, hero areas     |

```tsx
{
  /* Extra Small - Inline loading indicators */
}
<Spinner size="xs" />;

{
  /* Small - Button loading states */
}
<Spinner size="s" />;

{
  /* Medium - Default general use */
}
<Spinner size="m" />;

{
  /* Large - Card loading, sections */
}
<Spinner size="l" />;

{
  /* Extra Large - Page loading, overlays */
}
<Spinner size="xl" />;

{
  /* Custom Size - Override with specific dimensions */
}
<Spinner size="m" customSize="32px" />;
```

## Label Positioning

### Position Variants

```tsx
{
  /* Top - Label above spinner */
}
<Spinner size="m" label="Loading data..." position="top" />;

{
  /* Bottom - Label below spinner (default) */
}
<Spinner size="m" label="Please wait..." position="bottom" />;

{
  /* Left - Label before spinner */
}
<Spinner size="s" label="Processing" position="left" />;

{
  /* Right - Label after spinner */
}
<Spinner size="s" label="Saving..." position="right" />;
```

## Color Customization

### Genesis Design System Colors

```tsx
{
  /* Primary colors */
}
<Spinner color="var(--gd-primary-50)" background="var(--gd-primary-20)" />;

{
  /* Success state */
}
<Spinner
  color="var(--gd-feedback-success-50)"
  background="var(--gd-feedback-success-20)"
  label="Upload complete"
  position="right"
/>;

{
  /* Error state */
}
<Spinner
  color="var(--gd-feedback-error-50)"
  background="var(--gd-feedback-error-20)"
  label="Error occurred"
  position="right"
/>;

{
  /* Warning state */
}
<Spinner
  color="var(--gd-feedback-warning-50)"
  background="var(--gd-feedback-warning-20)"
  label="Processing with caution"
  position="right"
/>;
```

### Custom Colors

```tsx
{
  /* Custom hex colors */
}
<Spinner color="#00C853" background="#E8F5E8" label="Custom green theme" position="right" />;

{
  /* CSS variables */
}
<Spinner
  color="rgb(59, 130, 246)"
  background="rgb(219, 234, 254)"
  label="Blue theme"
  position="right"
/>;

{
  /* Current color inheritance */
}
<div className="text-purple-600">
  <Spinner
    color="currentColor"
    background="rgba(147, 51, 234, 0.2)"
    label="Inherits text color"
    position="right"
  />
</div>;
```

## Real-World Usage Examples

### Button Loading States

```tsx
function LoadingButton({ isLoading, onClick, children }) {
  return (
    <button
      onClick={onClick}
      disabled={isLoading}
      className="flex items-center gap-3 px-4 py-2 bg-primary-50 text-white rounded-lg disabled:opacity-50"
    >
      {isLoading ? (
        <Spinner
          size="s"
          color="white"
          background="rgba(255, 255, 255, 0.3)"
          label="Saving..."
          position="right"
        />
      ) : (
        children
      )}
    </button>
  );
}

// Usage variants
<LoadingButton isLoading={isSaving}>Save Changes</LoadingButton>
<LoadingButton isLoading={isSubmitting}>Submit Form</LoadingButton>
<LoadingButton isLoading={isUploading}>Upload File</LoadingButton>
```

### Full-Page Loading Overlay

```tsx
function PageLoader({ isVisible, message = "Loading content..." }) {
  if (!isVisible) return null;

  return (
    <div className="fixed inset-0 bg-white/80 backdrop-blur-sm flex items-center justify-center z-50">
      <div className="text-center">
        <Spinner
          size="xl"
          label={message}
          position="bottom"
          labelClassName="text-neutral-grey-80 font-medium"
          containerClassName="bg-white rounded-lg shadow-lg p-8"
        />
      </div>
    </div>
  );
}

// Usage examples
<PageLoader isVisible={isInitialLoading} />
<PageLoader isVisible={isPageTransition} message="Navigating..." />
<PageLoader isVisible={isDataRefresh} message="Refreshing data..." />
```

### Inline Text Loading

```tsx
function InlineLoadingText({ isLoading, text, loadingText = "Loading..." }) {
  return (
    <span className="inline-flex items-center">
      {isLoading ? (
        <Spinner
          size="xs"
          color="currentColor"
          background="rgba(0, 0, 0, 0.2)"
          label={loadingText}
          position="right"
          labelClassName="text-inherit"
        />
      ) : (
        text
      )}
    </span>
  );
}

// Usage in different contexts
<p>Status: <InlineLoadingText isLoading={isChecking} text="Connected" loadingText="Checking..." /></p>
<h3>Data count: <InlineLoadingText isLoading={isCounting} text="42 items" loadingText="Counting..." /></h3>
```

### Card Loading States

```tsx
function LoadingCard({ isLoading, children, title }) {
  return (
    <div className="border border-neutral-grey-40 rounded-lg p-6 min-h-[200px]">
      <h3 className="text-lg font-semibold mb-4">{title}</h3>
      {isLoading ? (
        <div className="flex items-center justify-center h-32">
          <Spinner
            size="l"
            label="Loading content..."
            position="bottom"
            labelClassName="text-neutral-grey-80"
          />
        </div>
      ) : (
        children
      )}
    </div>
  );
}

// Skeleton loading variant
function SkeletonCard({ isLoading, children }) {
  return (
    <div className="border border-neutral-grey-40 rounded-lg p-6">
      {isLoading ? (
        <div className="space-y-4">
          <div className="flex items-center gap-3">
            <Spinner size="s" />
            <div className="h-4 bg-neutral-grey-30 rounded w-1/3"></div>
          </div>
          <div className="space-y-2">
            <div className="h-3 bg-neutral-grey-30 rounded w-full"></div>
            <div className="h-3 bg-neutral-grey-30 rounded w-2/3"></div>
          </div>
        </div>
      ) : (
        children
      )}
    </div>
  );
}
```

### Data Table Loading

```tsx
function DataTableWithLoading({ data, isLoading, columns }) {
  return (
    <div className="bg-white rounded-lg border">
      <table className="w-full">
        <thead>
          <tr>
            {columns.map(col => (
              <th key={col.key} className="text-left p-4 border-b">
                {col.label}
              </th>
            ))}
          </tr>
        </thead>
        <tbody>
          {isLoading ? (
            <tr>
              <td colSpan={columns.length} className="p-8 text-center">
                <Spinner
                  size="l"
                  label="Loading table data..."
                  position="bottom"
                  labelClassName="text-neutral-grey-80"
                />
              </td>
            </tr>
          ) : (
            data.map(row => (
              <tr key={row.id}>
                {columns.map(col => (
                  <td key={col.key} className="p-4 border-b">
                    {row[col.key]}
                  </td>
                ))}
              </tr>
            ))
          )}
        </tbody>
      </table>
    </div>
  );
}
```

### Form Field Loading

```tsx
function FormFieldWithLoading({ label, isValidating, error, children }) {
  return (
    <div className="space-y-2">
      <label className="flex items-center gap-2 text-sm font-medium">
        {label}
        {isValidating && (
          <Spinner
            size="xs"
            color="var(--gd-primary-50)"
            label="Validating..."
            position="right"
            labelClassName="text-xs text-neutral-grey-80"
          />
        )}
      </label>
      {children}
      {error && <p className="text-xs text-feedback-error-50">{error}</p>}
    </div>
  );
}

// Usage in forms
<FormFieldWithLoading label="Username" isValidating={isCheckingUsername} error={usernameError}>
  <input
    type="text"
    value={username}
    onChange={handleUsernameChange}
    className="w-full px-3 py-2 border rounded"
  />
</FormFieldWithLoading>;
```

### Search Results Loading

```tsx
function SearchResultsLoader({ isSearching, query, results }) {
  return (
    <div className="space-y-4">
      <div className="flex items-center justify-between">
        <h3 className="text-lg font-semibold">Search Results {query && `for "${query}"`}</h3>
        {isSearching && (
          <Spinner
            size="s"
            label="Searching..."
            position="right"
            labelClassName="text-sm text-neutral-grey-80"
          />
        )}
      </div>

      {isSearching ? (
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          {Array.from({ length: 6 }).map((_, i) => (
            <div key={i} className="border rounded-lg p-4 space-y-3">
              <div className="flex items-center gap-2">
                <Spinner size="xs" />
                <div className="h-4 bg-neutral-grey-30 rounded w-2/3"></div>
              </div>
              <div className="space-y-2">
                <div className="h-3 bg-neutral-grey-30 rounded w-full"></div>
                <div className="h-3 bg-neutral-grey-30 rounded w-1/2"></div>
              </div>
            </div>
          ))}
        </div>
      ) : (
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          {results.map(result => (
            <ResultCard key={result.id} data={result} />
          ))}
        </div>
      )}
    </div>
  );
}
```

### Media Upload with Progress

```tsx
function MediaUploadSpinner({ isUploading, progress, fileName }) {
  return (
    <div className="border-2 border-dashed border-primary-50 rounded-lg p-6 text-center">
      {isUploading ? (
        <div className="space-y-3">
          <Spinner
            size="l"
            color="var(--gd-primary-50)"
            background="var(--gd-primary-20)"
            label={`Uploading ${fileName}...`}
            position="bottom"
            labelClassName="text-sm font-medium"
          />
          {progress && (
            <div className="w-full bg-neutral-grey-30 rounded-full h-2">
              <div
                className="bg-primary-50 h-2 rounded-full transition-all duration-300"
                style={{ width: `${progress}%` }}
              />
            </div>
          )}
          <p className="text-xs text-neutral-grey-80">
            {progress ? `${progress}% complete` : "Preparing upload..."}
          </p>
        </div>
      ) : (
        <div className="space-y-2">
          <div className="text-4xl">📁</div>
          <p className="text-sm font-medium">Drop files here or click to browse</p>
        </div>
      )}
    </div>
  );
}
```

## Accessibility Features

### Screen Reader Support

```tsx
{/* Basic accessibility */}
<Spinner
  role="status"
  aria-label="Loading content"
  label="Please wait while we load your data"
/>

{/* Live region for dynamic updates */}
<div aria-live="polite" aria-atomic="true">
  <Spinner
    label={loadingMessage}
    position="bottom"
  />
</div>

{/* Descriptive loading states */}
<Spinner
  aria-describedby="loading-description"
  label="Uploading file"
  position="right"
/>
<div id="loading-description" className="sr-only">
  File upload is in progress. Please do not close this window.
</div>
```

### Keyboard Navigation Support

```tsx
function AccessibleLoadingContainer({ isLoading, children }) {
  return (
    <div>
      {isLoading && (
        <div
          role="status"
          aria-live="polite"
          aria-label="Content is loading"
          tabIndex={-1}
          className="focus:outline-none"
        >
          <Spinner size="l" label="Loading content..." position="bottom" />
        </div>
      )}
      <div aria-hidden={isLoading ? "true" : "false"}>{children}</div>
    </div>
  );
}
```

### Visual Accessibility

```tsx
{
  /* High contrast mode support */
}
<Spinner
  color="var(--gd-primary-50)"
  background="var(--gd-neutral-grey-40)"
  className="forced-colors:text-ButtonText forced-colors:bg-ButtonFace"
/>;

{
  /* Reduced motion support */
}
<Spinner
  className="motion-reduce:animate-none motion-reduce:opacity-75"
  label="Loading (animation paused for accessibility)"
/>;
```

## Advanced Customization

### Custom Styling

```tsx
{
  /* Brand-specific spinner */
}
<Spinner
  size="m"
  color="var(--brand-primary)"
  background="var(--brand-light)"
  label="Brand loading experience"
  position="right"
  containerClassName="bg-brand-surface rounded-full px-4 py-2 shadow-lg"
  labelClassName="font-brand text-brand-dark"
  containerStyle={{
    background: "linear-gradient(135deg, var(--brand-primary), var(--brand-secondary))",
  }}
/>;

{
  /* Theme-adaptive spinner */
}
<Spinner
  size="l"
  color="hsl(var(--primary))"
  background="hsl(var(--muted))"
  label="Theme-aware loading"
  labelClassName="text-foreground"
  containerClassName="bg-background border border-border rounded-lg p-4"
/>;
```

### Conditional Rendering Patterns

```tsx
function ConditionalSpinner({
  condition,
  size = "m",
  message = "Loading...",
  fallback = null
}) {
  if (!condition) return fallback;

  return (
    <Spinner
      size={size}
      label={message}
      position="bottom"
      containerClassName="flex items-center justify-center min-h-24"
    />
  );
}

// Usage with different conditions
<ConditionalSpinner condition={isInitialLoad} message="Initializing app..." />
<ConditionalSpinner condition={isSaving} size="s" message="Saving..." />
<ConditionalSpinner condition={isError} fallback={<ErrorMessage />} />
```

## Design System Integration

### Genesis Design Tokens

**Colors:**

- Default Active: `var(--gd-primary-50)`
- Default Background: `var(--gd-neutral-grey-40)`
- Success: `var(--gd-feedback-success-50)`
- Error: `var(--gd-feedback-error-50)`
- Warning: `var(--gd-feedback-warning-50)`

**Typography:**

- Font sizes: 12px, 14px, 16px, 18px
- Line heights: 16px, 20px, 24px
- Font weight: Normal (400)

**Spacing:**

- Label gaps: 4px, 8px, 12px, 16px
- Based on Genesis spacing tokens

**Animation:**

- CSS class: `animate-spin`
- Duration: Consistent with system animations
- Easing: Linear rotation

## Performance Considerations

### Optimized Rendering

```tsx
// Memoize spinner to prevent unnecessary re-renders
const MemoizedSpinner = memo(Spinner);

// Use conditional rendering to avoid DOM updates
{
  isLoading && <Spinner size="m" label="Loading..." />;
}

// Avoid inline styles when possible
const spinnerStyles = useMemo(
  () => ({
    color: primaryColor,
    background: trackColor,
  }),
  [primaryColor, trackColor]
);
```

### Animation Performance

- Uses CSS `animate-spin` for GPU acceleration
- SVG-based graphics for crisp rendering at all sizes
- Minimal DOM updates during animation
- Optimized stroke-width for each size variant

## Testing Support

### Test Data Attributes

```tsx
<Spinner data-testid="loading-spinner" label="Loading data" position="right" />

// Test elements available:
// - [data-testid="spinner-container"] - Main container
// - [data-testid="spinner-svg"] - SVG element
// - [data-testid="spinner-label"] - Label text
// - [data-testid="spinner-sr-text"] - Screen reader text
```

### Testing Examples

```tsx
// Jest/React Testing Library
import { render, screen } from "@testing-library/react";

test("renders spinner with label", () => {
  render(<Spinner label="Loading data" />);

  expect(screen.getByRole("status")).toBeInTheDocument();
  expect(screen.getByText("Loading data")).toBeInTheDocument();
  expect(screen.getByText("Loading...")).toHaveClass("sr-only");
});

test("applies custom size", () => {
  render(<Spinner size="xl" customSize="64px" />);

  const svg = screen.getByTestId("spinner-svg");
  expect(svg).toHaveStyle({ width: "64px", height: "64px" });
});
```

## Best Practices

### UX Guidelines

- Use appropriate sizes for context
- Provide meaningful loading messages
- Consider placement and visual hierarchy
- Handle long-running operations gracefully
- Provide escape mechanisms when possible

### Performance

- Minimize re-renders with proper memoization
- Use conditional rendering for visibility
- Avoid inline styles for static properties
- Consider animation performance on low-end devices

### Accessibility

- Always include descriptive labels
- Use proper ARIA attributes
- Support reduced motion preferences
- Maintain adequate color contrast
- Provide alternative communication methods

## Migration Notes

### From Previous Versions

- Update import paths to new component location
- Review prop name changes (`LoaderProps` interface)
- Test custom styling with new class structure
- Verify accessibility improvements work correctly

### Breaking Changes

- Renamed interface from generic to `LoaderProps`
- Added new test data attributes
- Enhanced accessibility markup
- Refined spacing and sizing calculations

Remember: The Spinner component should enhance user experience by providing clear feedback about loading states. Use appropriate sizing, meaningful labels, and ensure accessibility compliance for the best results across all user scenarios.
