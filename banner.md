# Banner

A versatile banner component for displaying important messages, announcements, and alerts with customizable actions and styling options.

---

## 1. Quick start

```tsx
import { Banner } from "gends";

function Example() {
  return (
    <Banner
      title="Welcome!"
      description="Thank you for joining our platform."
      variant="primary"
      primaryBtnText="Get Started"
      primaryBtnAction={() => console.log("Getting started")}
    />
  );
}
```

---

## 2. Banner variants

| variant   | Background   | Border color | Use case              |
| --------- | ------------ | ------------ | --------------------- |
| `primary` | Light blue   | Blue         | General announcements |
| `success` | Light green  | Green        | Success messages      |
| `error`   | Light red    | Red          | Error notifications   |
| `warning` | Light orange | Orange       | Warning alerts        |
| `neutral` | Light gray   | Gray         | Neutral information   |

```tsx
<Banner variant="primary" title="Primary Banner" description="General announcement" />
<Banner variant="success" title="Success!" description="Operation completed" />
<Banner variant="error" title="Error" description="Something went wrong" />
<Banner variant="warning" title="Warning" description="Please review" />
<Banner variant="neutral" title="Info" description="Neutral information" />
```

---

## 3. Layout options

The banner supports two main layout modes:

| layout       | Description                        | Use case            |
| ------------ | ---------------------------------- | ------------------- |
| `multiLine`  | Full height with title and actions | Detailed messages   |
| `singleLine` | Compact height, inline content     | Brief notifications |

```tsx
// Multi-line banner (default)
<Banner
  title="Multi-line Banner"
  description="This banner shows both title and description with action buttons."
  isSingleLine={false}
/>

// Single-line banner
<Banner
  description="Brief notification message"
  isSingleLine={true}
  hideTitle={true}
/>

// Full-width banner
<Banner
  description="This banner spans the full screen width"
  isFullWidth={true}
  isSingleLine={true}
/>
```

---

## 4. Actions and buttons

```tsx
// With both action buttons
<Banner
  title="Confirm Action"
  description="Are you sure you want to proceed?"
  variant="warning"
  primaryBtnText="Confirm"
  secondaryBtnText="Cancel"
  primaryBtnAction={() => handleConfirm()}
  secondaryBtnAction={() => handleCancel()}
/>

// Primary button only
<Banner
  title="Single Action"
  description="Click to continue"
  hideSecondaryBtn={true}
  primaryBtnText="Continue"
  primaryBtnAction={() => handleContinue()}
/>

// No buttons
<Banner
  title="Information Only"
  description="This is just an informational message"
  hideButtons={true}
/>
```

---

## 5. Icons and content

```tsx
// Custom icon
<Banner
  title="Custom Icon"
  description="Banner with a custom icon"
  icon={<CustomIcon />}
/>

// Hide icon
<Banner
  title="No Icon"
  description="Banner without an icon"
  hideIcon={true}
/>

// Loading state
<Banner
  title="Processing..."
  description="Please wait while we process your request"
  loading={true}
/>
```

---

## 6. Visibility and closing

```tsx
// Closeable banner
<Banner
  title="Closeable Banner"
  description="Click the X to close this banner"
  onClose={() => setBannerVisible(false)}
/>

// Hide close button
<Banner
  title="Persistent Banner"
  description="This banner cannot be closed"
  hideClose={true}
/>

// Controlled visibility
<Banner
  title="Controlled Banner"
  description="Banner visibility is controlled externally"
  showBanner={isVisible}
  onClose={() => setIsVisible(false)}
/>
```

---

## 7. Full prop reference

### Content Props

| Prop          | Type                                                          | Default         | Description                     |
| ------------- | ------------------------------------------------------------- | --------------- | ------------------------------- |
| `title`       | `string`                                                      | `"Title"`       | Banner title text               |
| `description` | `string`                                                      | `"Description"` | Banner description text         |
| `variant`     | `'neutral' \| 'primary' \| 'error' \| 'success' \| 'warning'` | `'primary'`     | Visual variant affecting colors |
| `icon`        | `React.ReactNode`                                             | -               | Custom icon element             |

### Layout Props

| Prop           | Type      | Default | Description                        |
| -------------- | --------- | ------- | ---------------------------------- |
| `isFullWidth`  | `boolean` | `false` | Make banner span full screen width |
| `isSingleLine` | `boolean` | `false` | Use compact single-line layout     |
| `hideTitle`    | `boolean` | `false` | Hide the title text                |
| `hideIcon`     | `boolean` | `false` | Hide the icon                      |

### Button Props

| Prop                 | Type         | Default    | Description                    |
| -------------------- | ------------ | ---------- | ------------------------------ |
| `hideButtons`        | `boolean`    | `false`    | Hide all action buttons        |
| `hidePrimaryBtn`     | `boolean`    | `false`    | Hide primary action button     |
| `hideSecondaryBtn`   | `boolean`    | `false`    | Hide secondary action button   |
| `primaryBtnText`     | `string`     | `"Submit"` | Primary button text            |
| `secondaryBtnText`   | `string`     | `"Cancel"` | Secondary button text          |
| `primaryBtnAction`   | `() => void` | `() => {}` | Primary button click handler   |
| `secondaryBtnAction` | `() => void` | `() => {}` | Secondary button click handler |

### State Props

| Prop         | Type         | Default | Description                |
| ------------ | ------------ | ------- | -------------------------- |
| `loading`    | `boolean`    | `false` | Show loading spinner       |
| `showBanner` | `boolean`    | `true`  | Control banner visibility  |
| `hideClose`  | `boolean`    | `false` | Hide close button          |
| `onClose`    | `() => void` | -       | Close button click handler |

---

## 8. Recipes

### Success notification banner

```tsx
<Banner
  title="Success!"
  description="Your account has been created successfully."
  variant="success"
  primaryBtnText="Continue"
  hideSecondaryBtn={true}
  primaryBtnAction={() => router.push("/dashboard")}
/>
```

### Error banner with retry action

```tsx
<Banner
  title="Connection Error"
  description="Unable to connect to the server. Please try again."
  variant="error"
  primaryBtnText="Retry"
  secondaryBtnText="Cancel"
  primaryBtnAction={() => retryConnection()}
  secondaryBtnAction={() => hideBanner()}
/>
```

### Full-width promotional banner

```tsx
<Banner
  description="🎉 Special offer: Get 20% off your first purchase!"
  variant="primary"
  isFullWidth={true}
  isSingleLine={true}
  hideTitle={true}
  primaryBtnText="Shop Now"
  primaryBtnAction={() => window.open("/shop")}
/>
```

### Warning banner with custom icon

```tsx
<Banner
  title="Maintenance Notice"
  description="System maintenance scheduled for tonight at 12 AM."
  variant="warning"
  icon={<MaintenanceIcon />}
  hideButtons={true}
/>
```

### Loading banner

```tsx
<Banner
  title="Processing Payment"
  description="Please wait while we process your payment..."
  variant="primary"
  loading={true}
  hideButtons={true}
  hideClose={true}
/>
```

### Dismissible info banner

```tsx
<Banner
  title="New Features Available"
  description="Check out our latest updates and improvements."
  variant="neutral"
  primaryBtnText="Learn More"
  primaryBtnAction={() => openFeatureGuide()}
  onClose={() => setShowBanner(false)}
/>
```

---

## 9. Accessibility

The Banner component includes several accessibility features:

- Proper ARIA roles and attributes
- Keyboard navigation support for interactive elements
- Focus management for action buttons
- Screen reader friendly content structure

```tsx
<Banner
  title="Accessible Banner"
  description="This banner follows accessibility best practices"
  variant="info"
  role="alert" // Automatically applied for error/warning variants
  aria-live="polite" // For non-urgent updates
/>
```

---

## 10. Design Tokens

The Banner component uses the following design system tokens:

**Layout:**

- Border radius: `12px`
- Border width: `1px`
- Padding: `12px`
- Gap between elements: `8px`, `12px`

**Typography:**

- Title: `text-en-desktop-body-l-prominent`
- Description: `text-en-desktop-body-m`
- Button text: Based on button component

**Colors:**

- Primary: `border-color-primary-30 bg-color-primary-10`
- Success: `border-color-text-success-default bg-color-feedback-success-20`
- Error: `border-color-feedback-error-50 bg-color-feedback-error-20`
- Warning: `border-color-feedback-warning-50 bg-color-feedback-warning-20`
- Neutral: `border-color-neutral-grey-40 bg-color-neutral-grey-10`

**Icons:**

- Size: `24px × 24px`
- Color: Matches variant theme

---

Consider using Banner with:

- **Button** — For action buttons
- **IconButton** — For close button
- **Spinner** — For loading states
- **Icon** — For custom icons
- **Modal** — For overlay messages
