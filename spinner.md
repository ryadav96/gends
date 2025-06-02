# Spinner

A versatile loading indicator component that provides smooth circular animation with customizable sizes, colors, labels, and positions—perfect for indicating loading states across your application.

---

## 1. Quick start

```tsx
import Spinner from "gends";

function Example() {
  return (
    <div className="space-y-4">
      {/* Basic spinner */}
      <Spinner />

      {/* With label */}
      <Spinner label="Loading..." position="right" />
    </div>
  );
}
```

Wrap **nothing**—`Spinner` is self-contained and provides a loading indicator with built-in animation.

---

## 2. Sizes

| Size | Dimensions | Font Size | Label Gap | Use Case                         |
| ---- | ---------- | --------- | --------- | -------------------------------- |
| `xs` | 12×12px    | 12px      | 4px       | Inline text, compact UIs         |
| `s`  | 16×16px    | 14px      | 8px       | Small buttons, tight spaces      |
| `m`  | 24×24px    | 16px      | 12px      | Default size, general use        |
| `l`  | 40×40px    | 18px      | 16px      | Large buttons, prominent areas   |
| `xl` | 48×48px    | 18px      | 16px      | Full-page loading, hero sections |

```tsx
<Spinner size="xs" />
<Spinner size="s" />
<Spinner size="m" />
<Spinner size="l" />
<Spinner size="xl" />

// Custom size
<Spinner customSize="32px" />
```

---

## 3. Label positions

| Position | Description          | Use Case              |
| -------- | -------------------- | --------------------- |
| `top`    | Label above spinner  | Vertical layouts      |
| `bottom` | Label below spinner  | Default position      |
| `left`   | Label before spinner | Inline text           |
| `right`  | Label after spinner  | Button loading states |

```tsx
<Spinner label="Loading" position="top" />
<Spinner label="Loading" position="bottom" />
<Spinner label="Loading" position="left" />
<Spinner label="Loading" position="right" />
```

---

## 4. Colors

Customize the spinner's appearance with color props:

```tsx
<Spinner
  color="var(--gd-primary-50)"      // Active spinner color
  background="var(--gd-neutral-40)" // Track color
/>

// Custom colors
<Spinner
  color="#0066FF"
  background="#E5E5E5"
/>
```

---

## 5. Full prop reference

### Basic

| Prop         | Type                                     | Default    | Description          |
| ------------ | ---------------------------------------- | ---------- | -------------------- |
| `size`       | `"xs" \| "s" \| "m" \| "l" \| "xl"`      | `"m"`      | Spinner size variant |
| `customSize` | `string`                                 | `""`       | Custom size override |
| `label`      | `string`                                 | `""`       | Loading text label   |
| `position`   | `"top" \| "bottom" \| "left" \| "right"` | `"bottom"` | Label position       |

### Colors

| Prop         | Type     | Default                     | Description          |
| ------------ | -------- | --------------------------- | -------------------- |
| `color`      | `string` | `var(--gd-primary-50)`      | Spinner active color |
| `background` | `string` | `var(--gd-neutral-grey-40)` | Spinner track color  |

### Styling

| Prop                 | Type            | Default | Description              |
| -------------------- | --------------- | ------- | ------------------------ |
| `containerClassName` | `string`        | -       | Container wrapper styles |
| `containerStyle`     | `CSSProperties` | `{}`    | Container inline styles  |
| `labelClassName`     | `string`        | -       | Label text styles        |
| `labelStyle`         | `CSSProperties` | `{}`    | Label inline styles      |

---

## 6. Recipes

### Button loading state

```tsx
function LoadingButton({ loading, children }) {
  return (
    <button className="flex items-center gap-2 px-4 py-2 rounded bg-primary-500" disabled={loading}>
      {loading ? (
        <Spinner
          size="s"
          color="white"
          background="rgba(255,255,255,0.3)"
          label="Loading"
          position="right"
        />
      ) : (
        children
      )}
    </button>
  );
}
```

### Full-page loader

```tsx
function PageLoader() {
  return (
    <div className="fixed inset-0 flex items-center justify-center bg-white/80">
      <Spinner size="xl" label="Loading content" position="bottom" labelClassName="text-gray-600" />
    </div>
  );
}
```

### Inline text loader

```tsx
function InlineLoader({ text }) {
  return (
    <span className="inline-flex items-center gap-2">
      <Spinner
        size="xs"
        color="currentColor"
        background="currentColor"
        label={text}
        position="right"
      />
    </span>
  );
}
```

### Card loading state

```tsx
function LoadingCard() {
  return (
    <div className="p-4 border rounded-lg flex items-center justify-center min-h-[200px]">
      <Spinner size="l" label="Loading card content" labelClassName="text-gray-500" />
    </div>
  );
}
```

### Custom styled spinner

```tsx
function BrandedSpinner() {
  return (
    <Spinner
      size="m"
      color="var(--brand-primary)"
      background="var(--brand-light)"
      label="Please wait"
      position="right"
      containerClassName="bg-gray-50 px-4 py-2 rounded-full shadow-sm"
      labelClassName="font-medium text-brand-dark"
    />
  );
}
```

---

## 7. Accessibility considerations

- Uses semantic `role="status"` for screen readers
- Includes hidden "Loading" text for assistive technology
- Maintains proper contrast ratios
- Supports keyboard focus management
- Provides clear loading indication

```tsx
<div aria-live="polite">
  <Spinner aria-label="Loading content" />
</div>
```

---

## 8. Design patterns

### Layout patterns

- Consistent positioning
- Proper spacing with labels
- Clear visual hierarchy
- Responsive sizing

### Animation patterns

- Smooth circular animation
- Consistent rotation speed
- Clear loading indication
- Visual feedback

### Styling patterns

- Brand color integration
- Proper contrast ratios
- Size consistency
- Label alignment

---
