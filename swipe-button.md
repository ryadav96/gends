# Swipe Button

A highly interactive button component that requires a sliding gesture for confirmation—perfect for critical actions, payment confirmations, and other operations that need an extra layer of user intent verification.

---

## 1. Quick start

```tsx
import SwipeButton from "gends";

function Example() {
  return <SwipeButton text="Swipe to confirm" onConfirm={() => console.log("Action confirmed!")} />;
}
```

Wrap **nothing else**—`SwipeButton` is self-contained and handles all gesture interactions internally.

---

## 2. Dimensions

| Property | Default | Description              |
| -------- | ------- | ------------------------ |
| Width    | 296px   | Total button width       |
| Height   | 48px    | Button height            |
| Thumb    | 40x40px | Sliding thumb dimensions |
| Padding  | 16px    | Internal spacing (gd-4)  |

```tsx
<SwipeButton width="400px" height="56px" />
```

All dimensions can be customized via props or className.

---

## 3. States

| State      | Description           | Visual feedback                                |
| ---------- | --------------------- | ---------------------------------------------- |
| Idle       | Initial state         | Default appearance with chevron icon           |
| Dragging   | User is sliding       | Thumb follows touch/mouse with grabbing cursor |
| Confirming | Threshold reached     | Shows confirming text and icon                 |
| Loading    | Processing action     | Displays spinner and loading text              |
| Confirmed  | Action complete       | Shows success icon and confirmed text          |
| Disabled   | Interaction prevented | Reduced opacity and not-allowed cursor         |

```tsx
// Default state
<SwipeButton text="Swipe to pay" />

// Disabled state
<SwipeButton text="Swipe to pay" disabled />

// Custom state text
<SwipeButton
  text="Swipe to send"
  confirmingText="Sending..."
  confirmedText="Sent!"
  loadingText="Processing..."
/>
```

---

## 4. Color customization

The component supports full color customization:

```tsx
<SwipeButton
  color="#0066FF" // Background color
  textColor="#FFFFFF" // Text and icon color
  style={{
    // Additional custom styles
    borderRadius: "8px",
    boxShadow: "0 2px 4px rgba(0,0,0,0.1)",
  }}
/>
```

---

## 5. Icons

Each state can have its own icon:

| State     | Default icon  | Prop          |
| --------- | ------------- | ------------- |
| Idle      | Chevron right | `icon`        |
| Loading   | Spinner       | `loadingIcon` |
| Confirmed | Checkmark     | `confirmIcon` |

```tsx
<SwipeButton
  icon={<CustomIcon className="h-5 w-5" />}
  loadingIcon={<Spinner className="h-5 w-5" />}
  confirmIcon={<CheckIcon className="h-5 w-5" />}
/>
```

---

## 6. Confirmation handling

The `onConfirm` handler supports both synchronous and asynchronous operations:

```tsx
// Synchronous confirmation
<SwipeButton
  onConfirm={() => {
    console.log("Confirmed!");
  }}
/>

// Async with Promise
<SwipeButton
  onConfirm={async () => {
    await submitPayment();
    showSuccessMessage();
  }}
/>

// Error handling
<SwipeButton
  onConfirm={async () => {
    try {
      await riskyOperation();
    } catch (error) {
      // Button automatically resets on error
      showErrorMessage(error);
    }
  }}
/>
```

---

## 7. Full prop reference

### Basic

| Prop        | Type                          | Default              | Description               |
| ----------- | ----------------------------- | -------------------- | ------------------------- |
| `text`      | `string`                      | `"Swipe to confirm"` | Primary button text       |
| `onConfirm` | `() => Promise<void> \| void` | `alert("Confirmed")` | Confirmation handler      |
| `disabled`  | `boolean`                     | `false`              | Disables all interactions |
| `id`        | `string`                      | `""`                 | HTML id attribute         |

### Styling

| Prop        | Type            | Default    | Description             |
| ----------- | --------------- | ---------- | ----------------------- |
| `color`     | `string`        | Primary-50 | Button background color |
| `textColor` | `string`        | White      | Text and icon color     |
| `width`     | `string`        | `"296px"`  | Button width            |
| `height`    | `string`        | `"48px"`   | Button height           |
| `className` | `string`        | –          | Additional CSS classes  |
| `style`     | `CSSProperties` | `{}`       | Inline styles           |

### State text

| Prop             | Type     | Default           | Description              |
| ---------------- | -------- | ----------------- | ------------------------ |
| `confirmingText` | `string` | `"Confirming"`    | Text during confirmation |
| `loadingText`    | `string` | `"Processing..."` | Text while processing    |
| `confirmedText`  | `string` | `"Confirmed"`     | Text after success       |
| `stateText`      | `object` | –                 | Override all state texts |

### Icons

| Prop          | Type        | Default              | Description           |
| ------------- | ----------- | -------------------- | --------------------- |
| `icon`        | `ReactNode` | `<IcChevronRight />` | Default state icon    |
| `loadingIcon` | `ReactNode` | `<Spinner />`        | Processing state icon |
| `confirmIcon` | `ReactNode` | `<IcConfirm />`      | Success state icon    |

---

## 8. Recipes

### Payment confirmation

```tsx
function PaymentButton({ amount, onPaymentComplete }) {
  return (
    <SwipeButton
      text={`Swipe to pay ${amount}`}
      confirmingText="Authorizing..."
      loadingText="Processing payment..."
      confirmedText="Payment successful!"
      onConfirm={async () => {
        await processPayment(amount);
        onPaymentComplete();
      }}
      color="#00875A" // Success green
      className="w-full max-w-md"
    />
  );
}
```

### Delete confirmation

```tsx
function DeleteButton({ itemId, onDeleted }) {
  return (
    <SwipeButton
      text="Swipe to delete"
      confirmingText="Release to confirm"
      loadingText="Deleting..."
      confirmedText="Deleted"
      onConfirm={async () => {
        await deleteItem(itemId);
        onDeleted();
      }}
      color="#DC2626" // Danger red
      icon={<TrashIcon className="h-5 w-5" />}
      confirmIcon={<CheckIcon className="h-5 w-5" />}
    />
  );
}
```

### Form submission

```tsx
function SubmitFormButton({ form, onSuccess }) {
  const [isValid, setIsValid] = useState(false);

  useEffect(() => {
    setIsValid(form.checkValidity());
  }, [form]);

  return (
    <SwipeButton
      text="Swipe to submit"
      disabled={!isValid}
      onConfirm={async () => {
        const data = new FormData(form);
        await submitForm(data);
        onSuccess();
      }}
      stateText={{
        confirming: "Validating...",
        loading: "Submitting...",
        confirmed: "Submitted successfully!",
      }}
    />
  );
}
```

### Multi-step confirmation

```tsx
function DeployButton({ service, environment }) {
  const [step, setStep] = useState(1);

  return (
    <SwipeButton
      text={`Swipe to deploy to ${environment}`}
      confirmingText={`Step ${step}/3`}
      loadingText="Deploying..."
      confirmedText="Deployed!"
      onConfirm={async () => {
        // Step 1: Build
        setStep(1);
        await buildService(service);

        // Step 2: Test
        setStep(2);
        await runTests(service);

        // Step 3: Deploy
        setStep(3);
        await deploy(service, environment);
      }}
      icon={<RocketIcon className="h-5 w-5" />}
      className="w-full"
    />
  );
}
```

### Custom feedback states

```tsx
function ActionButton({ onAction }) {
  const [status, setStatus] = useState("idle");

  return (
    <SwipeButton
      text="Swipe to proceed"
      onConfirm={async () => {
        try {
          setStatus("processing");
          await onAction();
          setStatus("success");
        } catch (error) {
          setStatus("error");
          throw error; // Allows button to reset
        }
      }}
      stateText={{
        confirming: "Release to continue",
        loading: status === "processing" ? "Processing..." : "Verifying...",
        confirmed: status === "success" ? "Complete!" : "Error occurred",
      }}
      confirmIcon={status === "success" ? <CheckIcon /> : <AlertIcon />}
      color={status === "error" ? "#DC2626" : "#0066FF"}
    />
  );
}
```

---

## 9. Accessibility considerations

- Supports keyboard interaction for accessibility
- Uses ARIA attributes to communicate state changes
- Provides visual feedback through colors and icons
- Maintains sufficient color contrast ratios
- Includes loading states for async operations

```tsx
<SwipeButton aria-label="Confirm payment of $50" aria-disabled={disabled} role="button" />
```

---

## 10. Design patterns

### Progress indication

- Clear visual feedback during sliding
- Distinct states for confirming/loading/confirmed
- Animated transitions between states
- Loading spinner for async operations

### Error handling

- Automatic reset on error
- Visual feedback for invalid states
- Clear error messaging
- Graceful degradation

### Interaction design

- Smooth sliding animation
- Haptic feedback on confirmation
- Clear success/error states
- Responsive to both touch and mouse events

---
