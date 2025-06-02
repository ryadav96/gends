# MessageBox

A flexible and accessible message component that displays feedback, alerts, and notifications with different types, sizes, and styling options.

---

## 1. Quick start

```tsx
import { MessageBox } from "gends";

function Example() {
  return (
    <MessageBox type="success" size="m">
      Your changes have been saved successfully!
    </MessageBox>
  );
}
```

---

## 2. Message Types

The MessageBox component supports three types of messages:

| Type      | Description                         | Use case                 |
| --------- | ----------------------------------- | ------------------------ |
| `error`   | Red background with error icon      | Error messages, warnings |
| `warning` | Orange background with warning icon | Cautionary messages      |
| `success` | Green background with success icon  | Success notifications    |

```tsx
<MessageBox type="error">An error occurred</MessageBox>
<MessageBox type="warning">Please review your changes</MessageBox>
<MessageBox type="success">Operation completed successfully</MessageBox>
```

---

## 3. Sizes

The MessageBox component supports four size variants:

| Size | Description             | Use case                    |
| ---- | ----------------------- | --------------------------- |
| `xs` | Extra small (12px icon) | Compact UI, inline messages |
| `s`  | Small (16px icon)       | Dense layouts               |
| `m`  | Medium (16px icon)      | Standard usage              |
| `l`  | Large (24px icon)       | Prominent notifications     |

```tsx
<MessageBox type="success" size="xs">Small message</MessageBox>
<MessageBox type="success" size="s">Small message</MessageBox>
<MessageBox type="success" size="m">Medium message</MessageBox>
<MessageBox type="success" size="l">Large message</MessageBox>
```

---

## 4. Custom Styling

Apply custom styles to different parts of the message:

```tsx
<MessageBox
  type="success"
  size="m"
  className="custom-message"
  iconClassName="custom-icon"
  textClassName="custom-text"
  style={{ margin: "16px" }}
>
  Custom styled message
</MessageBox>
```

---

## 5. Icon Options

Control the visibility of the message icon:

```tsx
// With icon (default)
<MessageBox type="success" showIcon={true}>
  Message with icon
</MessageBox>

// Without icon
<MessageBox type="success" showIcon={false}>
  Message without icon
</MessageBox>
```

---

## 6. Full Prop Reference

### Basic Props

| Prop       | Type                                | Default | Description                 |
| ---------- | ----------------------------------- | ------- | --------------------------- |
| `type`     | `'error' \| 'warning' \| 'success'` | -       | Message type                |
| `size`     | `'xs' \| 's' \| 'm' \| 'l'`         | `'m'`   | Size variant of the message |
| `children` | `ReactNode`                         | -       | Message content             |
| `showIcon` | `boolean`                           | `true`  | Show/hide the message icon  |

### Styling Props

| Prop            | Type     | Default | Description                            |
| --------------- | -------- | ------- | -------------------------------------- |
| `className`     | `string` | -       | Additional CSS classes for the message |
| `iconClassName` | `string` | -       | Custom class names for the icon        |
| `textClassName` | `string` | -       | Custom class names for the text        |
| `style`         | `object` | -       | Inline styles for the message          |

---

## 7. Recipes

### Error Message with Custom Styling

```tsx
<MessageBox
  type="error"
  size="l"
  className="border border-red-200"
  iconClassName="text-red-600"
  textClassName="font-medium"
>
  Failed to save changes. Please try again.
</MessageBox>
```

### Warning Message without Icon

```tsx
<MessageBox type="warning" size="m" showIcon={false} className="bg-orange-50">
  Your session will expire in 5 minutes
</MessageBox>
```

### Success Message with Custom Icon

```tsx
<MessageBox type="success" size="s" iconClassName="text-green-600" className="bg-green-50">
  Profile updated successfully
</MessageBox>
```

---

## 8. Accessibility

The MessageBox component includes several accessibility features:

- Proper ARIA attributes:
  - `role="alert"` for important messages
  - `aria-live="polite"` for dynamic updates
- Icon marked as decorative with `aria-hidden="true"`
- Color contrast compliance
- Clear visual hierarchy

```tsx
<MessageBox type="error" size="m" role="alert" aria-live="polite">
  Critical error message
</MessageBox>
```

---

## 9. Design Tokens

The MessageBox component uses the following design system tokens:

**Colors:**

- Error: `text-color-text-error-subdued bg-color-bg-error-subdued`
- Warning: `text-color-text-warning-subdued bg-color-bg-warning-subdued`
- Success: `text-color-text-success-subdued bg-color-bg-success-subdued`

**Typography:**

- XS: `text-en-desktop-body-s`
- S: `text-en-desktop-body-s`
- M: `text-en-desktop-body-m`
- L: `text-en-desktop-body-l`

**Spacing:**

- XS/S/M: `gap-gd-4`
- L: `gap-gd-8`

**Icon Sizes:**

- XS: `12px`
- S/M: `16px`
- L: `24px`

**Layout:**

- Border radius: `rounded-lg`
- Flex layout: `flex items-center`

---

Consider using MessageBox with:

- **Button** — For action buttons in messages
- **Icon** — For custom icons
- **Typography** — For message text
- **Form** — For form feedback
- **Modal** — For modal messages
- **Toast** — For temporary notifications
