# NotificationNudge

A comprehensive notification system with toast messages, promise handling, and flexible customization options for user feedback and alerts.

---

## 1. Quick start

```tsx
import { notify, NotificationProvider } from "gends";

function App() {
  return (
    <NotificationProvider>
      <YourApp />
    </NotificationProvider>
  );
}

function Example() {
  const handleNotify = () => {
    notify({
      title: "Success!",
      description: "Your changes have been saved.",
      variant: "success",
      duration: 5000,
    });
  };

  return <Button onClick={handleNotify}>Show Notification</Button>;
}
```

---

## 2. Notification variants

| variant   | Icon         | Background color | Use case              |
| --------- | ------------ | ---------------- | --------------------- |
| `info`    | Info icon    | Dark gray        | General information   |
| `success` | Success icon | Green            | Successful operations |
| `error`   | Error icon   | Red              | Error messages        |
| `loading` | Spinner      | Dark gray        | Loading operations    |

```tsx
// Info notification (default)
notify({ title: "Information", variant: "info" });

// Success notification
notify({ title: "Success!", variant: "success" });

// Error notification
notify({ title: "Error occurred", variant: "error" });

// Loading notification
notify({ title: "Processing...", variant: "loading" });
```

---

## 3. Duration and positioning

```tsx
// Auto-dismiss after 3 seconds
notify({
  title: "Auto dismiss",
  duration: 3000,
  position: "top-right",
});

// Manual dismiss (stays until closed)
notify({
  title: "Manual dismiss",
  duration: null,
  position: "bottom-center",
});

// Available positions: "top-left", "top-center", "top-right",
// "bottom-left", "bottom-center", "bottom-right"
```

---

## 4. Actions and progress

```tsx
// With action buttons
notify({
  title: "Confirm action",
  description: "Are you sure you want to continue?",
  variant: "info",
  showActions: true,
  primaryAction: {
    label: "Confirm",
    onClick: () => console.log("Confirmed"),
  },
  secondaryAction: {
    label: "Cancel",
    onClick: () => console.log("Cancelled"),
  },
});

// With progress bar
notify({
  title: "Processing...",
  variant: "loading",
  showProgressBar: true,
  duration: 10000,
});
```

---

## 5. Promise notifications

```tsx
// Automatically handle promise states
const saveData = async () => {
  const promise = fetch("/api/save", { method: "POST" });

  notifyPromise(promise, {
    loading: "Saving your changes...",
    success: "Changes saved successfully!",
    error: "Failed to save changes",
    position: "top-right",
  });
};
```

---

## 6. Custom styling and icons

```tsx
// Custom icon and styling
notify({
  title: "Custom notification",
  customIcon: <CustomIcon />,
  className: "custom-notification",
  style: { backgroundColor: "purple" },
  iconStyle: { color: "white" },
});

// Stackable vs non-stackable
notify({
  title: "Single notification",
  stackable: false, // Only one notification at a time
});
```

---

## 7. Full prop reference

### Basic Notification Options

| Prop          | Type                                          | Default       | Description                       |
| ------------- | --------------------------------------------- | ------------- | --------------------------------- |
| `title`       | `string`                                      | -             | Notification title (required)     |
| `variant`     | `'info' \| 'success' \| 'error' \| 'loading'` | `'info'`      | Notification type                 |
| `description` | `string`                                      | -             | Optional description text         |
| `duration`    | `number \| null`                              | `5000`        | Auto-dismiss time (null = manual) |
| `position`    | `Position`                                    | `'top-right'` | Toast position on screen          |

### Display Options

| Prop              | Type        | Default | Description                    |
| ----------------- | ----------- | ------- | ------------------------------ |
| `showActions`     | `boolean`   | `false` | Show action buttons            |
| `showProgressBar` | `boolean`   | `false` | Show progress bar for duration |
| `stackable`       | `boolean`   | `true`  | Allow multiple notifications   |
| `customIcon`      | `ReactNode` | -       | Custom icon element            |

### Actions

| Prop              | Type         | Description                           |
| ----------------- | ------------ | ------------------------------------- |
| `primaryAction`   | `ActionObj`  | Primary action button configuration   |
| `secondaryAction` | `ActionObj`  | Secondary action button configuration |
| `onClose`         | `() => void` | Callback when notification closes     |

### Action Object Type

| Prop        | Type                  | Description        |
| ----------- | --------------------- | ------------------ |
| `label`     | `string`              | Button text        |
| `onClick`   | `() => void`          | Click handler      |
| `className` | `string`              | Custom CSS classes |
| `style`     | `React.CSSProperties` | Inline styles      |

### Styling

| Prop        | Type                  | Description          |
| ----------- | --------------------- | -------------------- |
| `className` | `string`              | Custom CSS classes   |
| `style`     | `React.CSSProperties` | Inline styles        |
| `iconStyle` | `React.CSSProperties` | Icon-specific styles |

---

## 8. Promise notification options

### Promise-specific Props

| Prop      | Type                                 | Description                 |
| --------- | ------------------------------------ | --------------------------- |
| `loading` | `string`                             | Loading state message       |
| `success` | `string \| (data: T) => string`      | Success message or function |
| `error`   | `string \| (err: unknown) => string` | Error message or function   |

---

## 9. Recipes

### Basic success notification

```tsx
notify({
  title: "Profile updated",
  description: "Your profile changes have been saved.",
  variant: "success",
});
```

### Error with action

```tsx
notify({
  title: "Connection failed",
  description: "Unable to connect to server.",
  variant: "error",
  showActions: true,
  primaryAction: {
    label: "Retry",
    onClick: () => retryConnection(),
  },
});
```

### Loading with progress

```tsx
notify({
  title: "Uploading file...",
  variant: "loading",
  showProgressBar: true,
  duration: 10000,
});
```

### Promise-based operation

```tsx
const handleSubmit = async () => {
  const submitPromise = submitForm(formData);

  notifyPromise(submitPromise, {
    loading: "Submitting form...",
    success: data => `Form submitted! ID: ${data.id}`,
    error: err => `Submit failed: ${err.message}`,
    position: "top-center",
  });
};
```

### Non-stackable notification

```tsx
notify({
  title: "System status",
  description: "All systems operational",
  variant: "info",
  stackable: false,
  duration: null,
});
```

### Custom styled notification

```tsx
notify({
  title: "Custom design",
  customIcon: <StarIcon />,
  className: "bg-gradient-to-r from-purple-500 to-pink-500",
  style: { borderRadius: "16px" },
  iconStyle: { color: "gold" },
});
```

---

## 10. Accessibility

The NotificationNudge component includes comprehensive accessibility features:

- `role="alert"` for screen reader announcements
- Keyboard navigation support (Escape to close)
- Focus management and trapping
- Proper ARIA attributes
- High contrast color support

```tsx
notify({
  title: "Accessible notification",
  description: "This notification is screen reader friendly",
  variant: "info",
  // Automatic accessibility attributes are applied
});
```

---

## 11. Design Tokens

The NotificationNudge component uses the following design system tokens:

**Layout:**

- Min width: `328px`
- Max width: `380px`
- Border radius: `12px`
- Padding: `12px`
- Gap: `8px` between elements

**Typography:**

- Title: `text-en-desktop-body-m-prominent`
- Description: `text-en-desktop-body-s`

**Colors:**

- Info: `bg-[#141414]`
- Success: `bg-[#135610]`
- Error: `bg-[#660014]`
- Loading: `bg-[#141414]`
- Text: `text-white`

**Shadows:**

- Box shadow: `shadow-[0_0_8px_0_var(--gd-neutral-shadow-opacity)]`

**Animations:**

- Progress bar: `transition-all duration-100 ease-linear`
- Hover states: Pause/resume timers

---

Consider using NotificationNudge with:

- **Button** — For action triggers
- **Form** — For validation feedback
- **Modal** — For operation results
- **API calls** — For loading states
- **File uploads** — For progress tracking
