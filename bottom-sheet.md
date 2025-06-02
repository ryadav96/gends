# Bottom Sheet

A modal component that slides up from the bottom of the screen, commonly used in mobile interfaces for providing contextual details or controls. The component supports various configurations for header, body, and footer sections with customizable content and actions.

---

## 1. Quick start

```tsx
import { BottomSheet } from "gends";

function Example() {
  return (
    <BottomSheet
      title="Sheet Title"
      bodyText="This is a bottom sheet used commonly in mobile platforms."
      primaryButtonText="Confirm"
      secondaryButtonText="Cancel"
      onClose={() => {}}
    />
  );
}
```

---

## 2. Sizes

The BottomSheet component supports two size variants:

| Size | Height | Use case                     |
| ---- | ------ | ---------------------------- |
| `sm` | 32px   | Compact actions, simple UI   |
| `md` | 40px   | Standard usage, rich content |

```tsx
// Small size
<BottomSheet size="sm" title="Small Sheet">
  {/* Content */}
</BottomSheet>

// Medium size (default)
<BottomSheet size="md" title="Medium Sheet">
  {/* Content */}
</BottomSheet>
```

---

## 3. Header Configuration

Customize the header section with various options:

```tsx
// Basic header with back button
<BottomSheet
  title="With Back Button"
  backIcon={true}
  onBackClick={() => {}}
/>

// Custom header slot
<BottomSheet
  headerSlot={true}
  swapHeaderSlot={<CustomHeaderContent />}
/>

// Hide header title
<BottomSheet
  headerTitle={false}
  title="Hidden Title"
/>
```

---

## 4. Body Content

Control the body section's content and behavior:

```tsx
// Basic body with text
<BottomSheet
  bodyText="This is the main content"
  bodyTextVisible={true}
/>

// Custom body content
<BottomSheet
  showBodySlot={true}
  swapBodySlot={<CustomBodyContent />}
/>

// Scrollable content
<BottomSheet
  scroll={true}
  bodyText="Long content that needs scrolling"
/>
```

---

## 5. Footer Actions

Configure the footer section with primary and secondary actions:

```tsx
// Basic actions
<BottomSheet
  primaryButtonText="Save"
  secondaryButtonText="Cancel"
  onPrimaryClick={() => {}}
  onSecondaryClick={() => {}}
/>

// Custom action handlers
<BottomSheet
  primaryButtonText="Delete"
  secondaryButtonText="Keep"
  onPrimaryClick={handleDelete}
  onSecondaryClick={handleKeep}
/>
```

---

## 6. Custom Styling

Apply custom styles to different sections of the bottom sheet:

```tsx
<BottomSheet
  classNames={{
    container: "custom-container-class",
    header: "custom-header-class",
    body: "custom-body-class",
    footer: "custom-footer-class",
    backdrop: "custom-backdrop-class",
  }}
  style={{ maxWidth: "500px" }}
/>
```

---

## 7. Full Prop Reference

### Basic Props

| Prop       | Type                  | Default                       | Description                         |
| ---------- | --------------------- | ----------------------------- | ----------------------------------- |
| `title`    | `string`              | `"Sheet title"`               | The title displayed in the header   |
| `bodyText` | `string`              | `"This is a bottom sheet..."` | Default body text content           |
| `size`     | `'sm' \| 'md'`        | `'md'`                        | Size variant of the bottom sheet    |
| `id`       | `string`              | `""`                          | Unique identifier for the component |
| `style`    | `React.CSSProperties` | `{}`                          | Inline styles for the container     |

### Header Props

| Prop             | Type        | Default    | Description                |
| ---------------- | ----------- | ---------- | -------------------------- |
| `backIcon`       | `boolean`   | `true`     | Show back button in header |
| `headerSlot`     | `boolean`   | `true`     | Enable custom header slot  |
| `swapHeaderSlot` | `ReactNode` | `<Slot />` | Custom header content      |
| `headerTitle`    | `boolean`   | `true`     | Show the title in header   |

### Body Props

| Prop              | Type        | Default | Description                |
| ----------------- | ----------- | ------- | -------------------------- |
| `scroll`          | `boolean`   | `true`  | Enable scrolling in body   |
| `swapBodySlot`    | `ReactNode` | `null`  | Custom body content        |
| `showBodySlot`    | `boolean`   | `true`  | Show the body slot         |
| `bodyTextVisible` | `boolean`   | `true`  | Show the default body text |

### Footer Props

| Prop                  | Type         | Default    | Description                      |
| --------------------- | ------------ | ---------- | -------------------------------- |
| `primaryButtonText`   | `string`     | `"Button"` | Text for primary action button   |
| `secondaryButtonText` | `string`     | `"Cancel"` | Text for secondary action button |
| `onPrimaryClick`      | `() => void` | `() => {}` | Primary button click handler     |
| `onSecondaryClick`    | `() => void` | `() => {}` | Secondary button click handler   |

### Event Handlers

| Prop          | Type         | Default    | Description                          |
| ------------- | ------------ | ---------- | ------------------------------------ |
| `onClose`     | `() => void` | `() => {}` | Handler for closing the bottom sheet |
| `onBackClick` | `() => void` | `() => {}` | Handler for back button click        |

### Styling Props

| Prop         | Type         | Default | Description                               |
| ------------ | ------------ | ------- | ----------------------------------------- |
| `classNames` | `ClassNames` | `{}`    | Custom class names for different sections |

---

## 8. Recipes

### Basic Form Sheet

```tsx
<BottomSheet
  title="Add New Item"
  bodyText="Fill in the details below"
  primaryButtonText="Save"
  secondaryButtonText="Cancel"
  onPrimaryClick={handleSave}
  onSecondaryClick={handleCancel}
>
  <form>{/* Form fields */}</form>
</BottomSheet>
```

### Confirmation Dialog

```tsx
<BottomSheet
  title="Confirm Action"
  bodyText="Are you sure you want to proceed?"
  primaryButtonText="Confirm"
  secondaryButtonText="Cancel"
  onPrimaryClick={handleConfirm}
  onSecondaryClick={handleCancel}
  size="sm"
/>
```

### Custom Content Sheet

```tsx
<BottomSheet
  title="Custom Content"
  headerSlot={true}
  swapHeaderSlot={<CustomHeader />}
  showBodySlot={true}
  swapBodySlot={<CustomContent />}
  primaryButtonText="Done"
  secondaryButtonText="Close"
/>
```

### Navigation Sheet

```tsx
<BottomSheet
  title="Navigation"
  backIcon={true}
  onBackClick={handleBack}
  showBodySlot={true}
  swapBodySlot={<NavigationMenu />}
  primaryButtonText="Select"
  secondaryButtonText="Cancel"
/>
```

---

## 9. Accessibility

The BottomSheet component includes several accessibility features:

- Proper ARIA attributes for modal dialog
- Focus management
- Keyboard navigation support
- Screen reader announcements
- Backdrop click handling
- Proper heading hierarchy

```tsx
<BottomSheet
  title="Accessible Sheet"
  role="dialog"
  aria-modal="true"
  aria-labelledby="bottom-sheet-title"
>
  {/* Content */}
</BottomSheet>
```

---

## 10. Design Tokens

The BottomSheet component uses the following design system tokens:

**Spacing:**

- Header padding: `px-gd-12 py-gd-16`
- Body padding: `px-gd-24 py-gd-0`
- Footer padding: `px-gd-24 py-gd-16`
- Gap between elements: `gap-gd-8`, `gap-gd-12`

**Typography:**

- Title: `text-en-desktop-heading-xl`
- Body text: `text-color-neutral-grey-80`

**Colors:**

- Background: `bg-color-neutral-white`
- Backdrop: `bg-color-neutral-grey-100`
- Border: Default border color

**Layout:**

- Max height: `max-h-[60vh]` for scrollable content
- Border radius: `rounded-t-xl`
- Width: `max-w-md`

**Transitions:**

- Duration: `duration-300`
- Timing: `ease-in-out`

---

Consider using BottomSheet with:

- **Button** — For action buttons
- **IconButton** — For header actions
- **Typography** — For consistent text styling
- **Form** — For input fields
- **List** — For navigation items
- **Card** — For content sections
