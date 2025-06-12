# Feedback Message Component

## Overview

The Feedback Message component (MessageBox) is a versatile and accessible alert component built with Genesis Design System tokens. It provides consistent visual feedback for user actions, system states, and validation messages through three semantic message types, four size variants, and comprehensive customization options. The component follows accessibility best practices with proper ARIA attributes and supports flexible content and styling.

## Component API

### MessageBox Props

| Prop          | Type                                | Default | Description                                        |
| ------------- | ----------------------------------- | ------- | -------------------------------------------------- |
| type          | `"error" \| "warning" \| "success"` | -       | Semantic message type determining color and icon   |
| size          | `"xs" \| "s" \| "m" \| "l"`         | `"m"`   | Size variant controlling dimensions and typography |
| children      | `ReactNode`                         | -       | Message content (text, elements, or components)    |
| showIcon      | `boolean`                           | `true`  | Whether to display the semantic icon               |
| className     | `string`                            | -       | Additional CSS classes for the message container   |
| iconClassName | `string`                            | -       | Custom CSS classes for the icon element            |
| textClassName | `string`                            | -       | Custom CSS classes for the text content            |
| style         | `React.CSSProperties`               | -       | Inline styles for the message container            |

### Extended HTML Props

The component extends `React.HTMLAttributes<HTMLDivElement>`, supporting all standard div attributes including:

- Event handlers (`onClick`, `onMouseOver`, etc.)
- Data attributes (`data-*`)
- ARIA attributes (`aria-*`)
- Standard HTML attributes (`id`, `role`, etc.)

## Import

```tsx
import { MessageBox } from "gends";
```

## Message Types

### Error Messages

Error messages communicate critical issues, failures, or validation errors that require immediate attention.

```tsx
<MessageBox type="error">
  Unable to save changes. Please check your connection and try again.
</MessageBox>
```

**Visual Characteristics:**

- **Background**: `bg-color-bg-error-subdued` (light red)
- **Text Color**: `text-color-text-error-subdued` (dark red)
- **Icon**: `IcCloseRemove` with `#F50031` color
- **Use Cases**: Form validation errors, API failures, critical system alerts

### Warning Messages

Warning messages alert users to potential issues or important information that needs attention.

```tsx
<MessageBox type="warning">
  Your session will expire in 5 minutes. Save your work to avoid losing changes.
</MessageBox>
```

**Visual Characteristics:**

- **Background**: `bg-color-bg-warning-subdued` (light orange)
- **Text Color**: `text-color-text-warning-subdued` (dark orange)
- **Icon**: `IcWarning` with `#F06D0F` color
- **Use Cases**: Cautions, temporary states, non-critical issues, confirmations

### Success Messages

Success messages confirm successful operations and positive outcomes.

```tsx
<MessageBox type="success">Profile updated successfully! Your changes have been saved.</MessageBox>
```

**Visual Characteristics:**

- **Background**: `bg-color-bg-success-subdued` (light green)
- **Text Color**: `text-color-text-success-subdued` (dark green)
- **Icon**: `IcSuccess` with `#25AB21` color
- **Use Cases**: Successful submissions, completed actions, positive confirmations

## Size Variants

### Extra Small (xs)

```tsx
<MessageBox type="success" size="xs">
  Compact success message for tight spaces
</MessageBox>
```

- **Icon Size**: 12px
- **Typography**: `text-en-desktop-body-s` (12px)
- **Spacing**: `gap-gd-4`, `p-gd-4`
- **Use Cases**: Inline validation, compact UI elements, table feedback

### Small (s)

```tsx
<MessageBox type="warning" size="s">
  Small warning message for dense layouts
</MessageBox>
```

- **Icon Size**: 16px
- **Typography**: `text-en-desktop-body-s` (12px)
- **Spacing**: `gap-gd-4`, `p-gd-4`
- **Use Cases**: Form fields, sidebar notifications, list item feedback

### Medium (m) - Default

```tsx
<MessageBox type="error" size="m">
  Standard error message for most use cases
</MessageBox>
```

- **Icon Size**: 16px
- **Typography**: `text-en-desktop-body-m` (14px)
- **Spacing**: `gap-gd-4`, `p-gd-4`
- **Use Cases**: Form validation, modal dialogs, card components

### Large (l)

```tsx
<MessageBox type="success" size="l">
  Large success message for prominent notifications
</MessageBox>
```

- **Icon Size**: 24px
- **Typography**: `text-en-desktop-body-l` (16px)
- **Spacing**: `gap-gd-8`, `p-gd-8`
- **Use Cases**: Page-level notifications, important announcements, hero sections

## Advanced Features

### Messages Without Icons

For text-only messages or when using custom icons:

```tsx
<MessageBox type="warning" showIcon={false}>
  Important: Please review the terms and conditions before proceeding.
</MessageBox>
```

### Custom Styled Messages

Apply custom styling to different parts of the component:

```tsx
<MessageBox
  type="success"
  size="m"
  className="border-2 border-dashed border-color-border-success shadow-lg"
  iconClassName="animate-pulse"
  textClassName="font-semibold underline"
>
  Custom styled success message with enhanced visual treatment
</MessageBox>
```

### Messages with Rich Content

Include complex content with multiple elements:

```tsx
<MessageBox type="error" size="l">
  <div className="space-y-2">
    <div className="font-semibold">Upload Failed</div>
    <div>The file exceeds the maximum size limit of 10MB.</div>
    <div className="text-sm">
      Try compressing your file or{" "}
      <a href="#" className="underline hover:no-underline">
        contact support
      </a>{" "}
      for assistance.
    </div>
  </div>
</MessageBox>
```

## Real-World Usage Examples

### Form Validation Feedback

```tsx
const FormValidation = () => {
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");
  const [success, setSuccess] = useState("");

  const validateEmail = value => {
    if (!value.includes("@")) {
      setError("Please enter a valid email address");
      setSuccess("");
    } else {
      setError("");
      setSuccess("Email format is valid");
    }
  };

  return (
    <div className="space-y-4">
      <div>
        <label htmlFor="email">Email Address</label>
        <input
          id="email"
          type="email"
          value={email}
          onChange={e => {
            setEmail(e.target.value);
            validateEmail(e.target.value);
          }}
          className="w-full p-2 border rounded"
        />
      </div>

      {error && (
        <MessageBox type="error" size="s">
          {error}
        </MessageBox>
      )}

      {success && (
        <MessageBox type="success" size="s">
          {success}
        </MessageBox>
      )}
    </div>
  );
};
```

### API Response Handling

```tsx
const ApiMessageHandler = () => {
  const [loading, setLoading] = useState(false);
  const [message, setMessage] = useState(null);

  const handleApiCall = async () => {
    setLoading(true);
    setMessage(null);

    try {
      const response = await fetch("/api/data");
      if (response.ok) {
        setMessage({
          type: "success",
          content: "Data updated successfully!",
        });
      } else {
        throw new Error("Update failed");
      }
    } catch (error) {
      setMessage({
        type: "error",
        content: "Failed to update data. Please try again.",
      });
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="space-y-4">
      <button
        onClick={handleApiCall}
        disabled={loading}
        className="px-4 py-2 bg-blue-500 text-white rounded disabled:opacity-50"
      >
        {loading ? "Updating..." : "Update Data"}
      </button>

      {message && (
        <MessageBox type={message.type} size="m">
          {message.content}
        </MessageBox>
      )}
    </div>
  );
};
```

### Dashboard Alerts

```tsx
const DashboardAlerts = () => {
  return (
    <div className="space-y-4">
      <MessageBox type="warning" size="l" className="mb-6">
        <div className="flex items-center justify-between w-full">
          <div>
            <div className="font-semibold">System Maintenance Scheduled</div>
            <div>Maintenance window: Tonight 11 PM - 1 AM PST</div>
          </div>
          <button className="ml-4 px-3 py-1 bg-orange-500 text-white rounded text-sm">
            Learn More
          </button>
        </div>
      </MessageBox>

      <MessageBox type="error" size="m">
        <div className="flex items-center justify-between w-full">
          <span>Connection to database lost. Retrying...</span>
          <div className="animate-spin w-4 h-4 border-2 border-red-500 border-t-transparent rounded-full"></div>
        </div>
      </MessageBox>

      <MessageBox type="success" size="s">
        All systems operational
      </MessageBox>
    </div>
  );
};
```

### Multi-Step Form Progress

```tsx
const MultiStepFormMessages = ({ step, errors, warnings }) => {
  return (
    <div className="space-y-3">
      {errors.length > 0 && (
        <MessageBox type="error" size="m">
          <div>
            <div className="font-semibold mb-2">Please fix the following errors:</div>
            <ul className="list-disc list-inside space-y-1">
              {errors.map((error, index) => (
                <li key={index} className="text-sm">
                  {error}
                </li>
              ))}
            </ul>
          </div>
        </MessageBox>
      )}

      {warnings.length > 0 && (
        <MessageBox type="warning" size="s">
          <div>
            <div className="font-medium mb-1">Optional improvements:</div>
            <ul className="list-disc list-inside text-sm">
              {warnings.map((warning, index) => (
                <li key={index}>{warning}</li>
              ))}
            </ul>
          </div>
        </MessageBox>
      )}

      {step === 3 && errors.length === 0 && (
        <MessageBox type="success" size="l">
          <div className="text-center">
            <div className="font-semibold mb-1">Form Complete!</div>
            <div>Your application has been submitted successfully.</div>
          </div>
        </MessageBox>
      )}
    </div>
  );
};
```

## Accessibility Features

### ARIA Attributes

The MessageBox component includes comprehensive accessibility features:

```tsx
// Automatic ARIA attributes
<MessageBox type="error" size="m">
  Critical system error
</MessageBox>
// Renders with: role="alert" aria-live="polite"

// Custom ARIA attributes
<MessageBox
  type="warning"
  size="m"
  aria-labelledby="warning-title"
  aria-describedby="warning-description"
>
  <div id="warning-title">Session Timeout Warning</div>
  <div id="warning-description">Your session will expire in 5 minutes</div>
</MessageBox>
```

### Screen Reader Support

- **Role**: `alert` for important messages requiring immediate attention
- **Live Region**: `aria-live="polite"` for dynamic message updates
- **Icon Handling**: Icons marked with `aria-hidden="true"` as decorative
- **Semantic Structure**: Proper heading hierarchy within message content

### Keyboard Navigation

```tsx
// Focusable message for interactive content
<MessageBox
  type="warning"
  size="m"
  tabIndex={0}
  onKeyDown={e => {
    if (e.key === "Enter" || e.key === " ") {
      handleDismiss();
    }
  }}
>
  <div className="flex items-center justify-between w-full">
    <span>Session will expire soon</span>
    <button
      onClick={handleExtendSession}
      className="ml-4 px-2 py-1 bg-white rounded text-sm focus:outline-none focus:ring-2"
    >
      Extend Session
    </button>
  </div>
</MessageBox>
```

## Design Tokens

### Color System

#### Error Messages

- **Background**: `bg-color-bg-error-subdued` (light red background)
- **Text**: `text-color-text-error-subdued` (dark red text)
- **Icon**: `#F50031` (bright red icon)

#### Warning Messages

- **Background**: `bg-color-bg-warning-subdued` (light orange background)
- **Text**: `text-color-text-warning-subdued` (dark orange text)
- **Icon**: `#F06D0F` (orange icon)

#### Success Messages

- **Background**: `bg-color-bg-success-subdued` (light green background)
- **Text**: `text-color-text-success-subdued` (dark green text)
- **Icon**: `#25AB21` (green icon)

### Typography Scale

- **Extra Small**: `text-en-desktop-body-s` (12px/16px)
- **Small**: `text-en-desktop-body-s` (12px/16px)
- **Medium**: `text-en-desktop-body-m` (14px/20px)
- **Large**: `text-en-desktop-body-l` (16px/24px)

### Spacing System

- **Gap (XS/S/M)**: `gap-gd-4` (4px between icon and text)
- **Gap (L)**: `gap-gd-8` (8px between icon and text)
- **Padding**: Controlled via external container or custom className

### Icon Specifications

- **Extra Small**: 12×12px
- **Small/Medium**: 16×16px
- **Large**: 24×24px
- **Positioning**: Vertically centered, shrink-resistant

### Layout Properties

- **Container**: `flex items-center rounded-lg`
- **Border Radius**: `rounded-lg` (Genesis standard)
- **Flex Behavior**: Icon doesn't shrink, text content grows

## Best Practices

### Message Content

- **Be Specific**: Provide clear, actionable information
- **Use Plain Language**: Avoid technical jargon
- **Include Next Steps**: Tell users what to do next
- **Keep it Concise**: Respect user attention and screen real estate

### Visual Hierarchy

```tsx
// Good: Clear hierarchy with title and description
<MessageBox type="error" size="m">
  <div>
    <div className="font-semibold">Upload Failed</div>
    <div className="text-sm mt-1">File size exceeds 10MB limit</div>
  </div>
</MessageBox>

// Good: Action-oriented with button
<MessageBox type="warning" size="l">
  <div className="flex items-center justify-between w-full">
    <div>
      <div className="font-semibold">Unsaved Changes</div>
      <div>You have unsaved changes that will be lost</div>
    </div>
    <div className="flex gap-2 ml-4">
      <button className="px-3 py-1 bg-orange-500 text-white rounded text-sm">
        Save
      </button>
      <button className="px-3 py-1 border border-orange-500 text-orange-500 rounded text-sm">
        Discard
      </button>
    </div>
  </div>
</MessageBox>
```

### Responsive Design

```tsx
// Responsive message sizing
<MessageBox type="error" size="s" className="text-sm md:text-base">
  <div className="md:flex md:items-center md:justify-between">
    <span>Error message content</span>
    <button className="mt-2 md:mt-0 md:ml-4 px-3 py-1 bg-red-500 text-white rounded text-sm">
      Retry
    </button>
  </div>
</MessageBox>
```

### Performance Considerations

```tsx
// Memoize messages with complex content
const ComplexMessage = memo(({ data, onAction }) => (
  <MessageBox type="warning" size="m">
    <div className="space-y-2">
      <div>Complex calculation result: {data.result}</div>
      <button onClick={onAction}>Take Action</button>
    </div>
  </MessageBox>
));

// Conditional rendering for better performance
const ConditionalMessage = ({ showMessage, type, content }) => {
  if (!showMessage) return null;

  return (
    <MessageBox type={type} size="m">
      {content}
    </MessageBox>
  );
};
```

## Integration Examples

### With Form Libraries

```tsx
// React Hook Form integration
const FormWithValidation = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <div>
        <input {...register("email", { required: "Email is required" })} />
        {errors.email && (
          <MessageBox type="error" size="s" className="mt-1">
            {errors.email.message}
          </MessageBox>
        )}
      </div>
    </form>
  );
};
```

### With State Management

```tsx
// Redux/Zustand integration
const MessageDisplay = () => {
  const messages = useSelector(state => state.messages);

  return (
    <div className="space-y-2">
      {messages.map(message => (
        <MessageBox
          key={message.id}
          type={message.type}
          size="m"
          className="transition-all duration-300"
        >
          {message.content}
        </MessageBox>
      ))}
    </div>
  );
};
```

## Troubleshooting

### Common Issues

**Icon not displaying**: Ensure the icon components are properly imported and the `showIcon` prop is not set to `false`.

**Colors not applying**: Verify that Genesis Design System tokens are available in your CSS and properly configured.

**Layout issues**: Check for conflicting CSS that might override the flex layout or spacing tokens.

**Accessibility warnings**: Ensure proper ARIA attributes are set when using interactive content within messages.

**Performance issues**: Use memoization for messages with complex content and conditional rendering for dynamic message lists.

### Migration Notes

When upgrading from previous versions:

- The component name is `MessageBox` (not `FeedbackMessage`)
- Size variant `xs` has been added for extra compact layouts
- Icon colors are now fixed per message type
- ARIA attributes are automatically applied

## Advanced Customization

### Custom Icon Implementation

```tsx
// Using custom icons (though not recommended due to semantic consistency)
const CustomIconMessage = ({ customIcon, ...props }) => (
  <MessageBox {...props} showIcon={false}>
    <div className="flex items-center gap-2">
      {customIcon}
      <span>{props.children}</span>
    </div>
  </MessageBox>
);
```

### Theme Customization

```tsx
// Custom theme implementation
const ThemedMessage = ({ theme = "default", ...props }) => {
  const themeClasses = {
    default: "",
    dark: "bg-gray-800 text-white",
    minimal: "bg-transparent border border-current",
  };

  return <MessageBox {...props} className={cn(themeClasses[theme], props.className)} />;
};
```

Remember: The MessageBox component is designed for consistent user feedback across your application. Always consider the user's context and the urgency of the message when choosing types and sizes.

---

Consider using MessageBox with:

- **Button** — For action buttons within messages
- **Form** — For validation feedback and status updates
- **Modal** — For dialog-specific messaging
- **Input** — For field-level validation
- **Card** — For section-specific alerts
- **Layout** — For page-level notifications
