# Notification Nudge

A lightweight, non-blocking “toast” system that floats above your UI.

---

## 1. Overview

* **Purpose:** Display short-lived messages without interrupting the current workflow.
* **API surface:**
  * `notify(options)` – programmatically push a notification.
  * `<NotificationProvider>` – context + toaster; wrap your application (or a subtree) once.

```tsx
import {
  NotificationProvider,
  notify,
} from '@/components/…/notification-nudge';

function App() {
  return (
    <NotificationProvider>
      <button
        onClick={() =>
          notify({ title: 'Saved!', variant: 'success' })
        }
      >
        Save
      </button>
    </NotificationProvider>
  );
}
```

---

## 2. Variants

| Variant   | Background                | Default icon     | Typical use-case                   |
|-----------|---------------------------|------------------|------------------------------------|
| `info`    | `#141414` (neutral)       | `IcInfo`         | Neutral / contextual information   |
| `success` | `#135610` (green)         | `IcSuccessColored` | Operation completed successfully   |
| `error`   | `#660014` (dark-red)      | `IcErrorColored` | Failure, destructive alert         |
| `loading` | `#141414` (neutral)       | `Spinner`        | Ongoing async operation            |

> Need a different icon? Supply a `customIcon` React node.

---

## 3. Position presets


```
'top-left'     'top-center'     'top-right'
'bottom-left'  'bottom-center'  'bottom-right'   // default
```

---

## 4. NotificationOptions

### Content

| Prop          | Type      | Default | Description                                  |
|---------------|-----------|---------|----------------------------------------------|
| `title`       | string    | –       | Main heading (required).                     |
| `description` | string    | `''`    | Secondary text                               |

### Appearance

| Prop             | Type                                          | Default       | Description                                                   |
|------------------|-----------------------------------------------|---------------|---------------------------------------------------------------|
| `variant`        | `'info' \| 'success' \| 'error' \| 'loading'` | `'info'`      | Visual style                                                  |
| `position`       | See positions above                           | `'top-right'` | Where the toast appears                                       |
| `showProgressBar`| boolean                                       | `false`       | Visual countdown                                              |
| `customIcon`     | `React.ReactNode`                             | `undefined`   | Override default icon                                         |
| `className`      | string                                        | –             | Extra classes for container                                   |
| `style`          | `CSSProperties`                               | –             | Inline container styles                                       |
| `iconStyle`      | `CSSProperties`                               | –             | Inline styles for the icon wrapper                            |

### Behaviour

| Prop        | Type                        | Default | Description                                                                |
|-------------|-----------------------------|---------|----------------------------------------------------------------------------|
| `duration`  | number (ms) \| `null`       | `5000`  | Auto-dismiss after *n* ms. `null`/`Infinity` → manual dismissal            |
| `stackable` | boolean                     | `true`  | `false` → new toast replaces previous one                                  |
| `onClose`   | `() => void`                | –       | Callback executed when toast disappears                                    |

### Actions

| Prop             | Type        | Default | Description                                                        |
|------------------|-------------|---------|--------------------------------------------------------------------|
| `showActions`    | boolean     | `false` | Render footer action buttons                                       |
| `primaryAction`  | object      | –       | `{ label, onClick, className?, style? }`                           |
| `secondaryAction`| object      | –       | Same shape as `primaryAction`                                      |

> The action buttons automatically adopt a high-contrast style for each variant. Closing the toast is handled for you after the callback runs.

---

## 5. Usage recipes

Below are **copy-paste-ready** snippets that cover every variant and the most common feature combinations. Mix & match the options as you need.

### 5.1 Basic variant examples

```ts
// Info (default)
notify({ title: 'Profile updated', variant: 'info' });

// Success
notify({ title: 'Payment complete', variant: 'success' });

// Error
notify({ title: 'Something went wrong', variant: 'error' });

// Loading (auto-dismiss after 4 s)
notify({ title: 'Syncing data…', variant: 'loading', duration: 4000 });
```

### 5.2 Success with description & progress bar

```ts
notify({
  title: 'Uploading file…',
  description: 'Your video will be available shortly.',
  variant: 'success',
  showProgressBar: true,
});
```

### 5.3 Error with actions (manual dismissal)

```ts
notify({
  title: 'Upload failed',
  description: 'Network error. Retry?',
  variant: 'error',
  duration: null,            // stay until user decides
  showActions: true,
  primaryAction: {
    label: 'Retry',
    onClick: retryUpload,
  },
  secondaryAction: {
    label: 'Cancel',
    onClick: () => {},
  },
});
```

### 5.4 Loading with cancel action (indefinite)

```ts
notify({
  title: 'Preparing export…',
  variant: 'loading',
  duration: null,            // manual mode
  showActions: true,
  secondaryAction: {
    label: 'Abort',
    onClick: cancelExport,
  },
});
```

### 5.5 Non-stackable banner

```ts
notify({
  title: 'Maintenance mode enabled',
  variant: 'info',
  stackable: false,          // replaces existing banner
  position: 'bottom-center',
});
```

### 5.6 Custom icon & styling

```ts
notify({
  title: 'Starred!',
  variant: 'info',
  customIcon: <span role="img" aria-label="star">⭐</span>,
  className: 'border border-blue-500',
  style: { backgroundColor: 'rgba(0,0,255,.1)' },
  iconStyle: { color: '#00f' },
});
```

### 5.7 Success with actions

```ts
notify({
  title: 'Profile saved',
  description: 'Changes will take effect next time you sign-in.',
  variant: 'success',
  showActions: true,
  primaryAction: {
    label: 'Undo',
    onClick: revertChanges,
  },
});
```


---

## 6. UX details

* **Hover-pause:** Auto-dismiss timers pause while the pointer is over the toast.
* **Accessibility:** Toasts live in a polite `aria-live` region (courtesy of Sonner).
* **Reduced motion:** Respects the user’s `prefers-reduced-motion` setting.
* **Keyboard:** `Esc` closes the most recent toast; focus is never trapped.

---

## 7. Component anatomy

```
NotificationProvider (context + Toaster)
└── NotificationToast
    ├── Icon (default or custom)
    ├── Content (title + optional description)
    ├── Actions (optional buttons)
    └── ProgressBar (optional)
```

---

## 8. Storybook playground

The file

```
src/components/genesis/molecules/notification-nudge/notification-nudge.stories.tsx
```

demonstrates every combination listed here:

* Info / Success / Error / Loading
* Description
* One / two actions
* Progress bar & hover-pause
* Custom icons + custom styling
* All six positions
* Stackable vs non-stackable

Launch Storybook and explore **Feedback / NotificationNudge** to tweak knobs and copy code.
