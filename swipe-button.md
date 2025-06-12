# Swipe Button Component

## Overview

The Swipe Button component is a highly interactive and secure action trigger that requires users to perform a sliding gesture for confirmation. Designed for critical actions requiring an extra layer of user intent verification, it provides smooth touch and mouse interactions with comprehensive visual feedback. Built with Genesis Design System tokens and accessible patterns, the component offers customizable appearance, state management, and confirmation handling for scenarios like payment processing, data deletion, or any high-stakes operations.

## Component API

### SwipeButton Props

| Prop             | Type                                                             | Default                    | Description                               |
| ---------------- | ---------------------------------------------------------------- | -------------------------- | ----------------------------------------- |
| `text`           | `string`                                                         | `"Swipe to confirm"`       | Primary text displayed on the button      |
| `onConfirm`      | `() => Promise<void> \| void`                                    | `() => alert("Confirmed")` | Function executed when swipe is completed |
| `disabled`       | `boolean`                                                        | `false`                    | Whether the button is disabled            |
| `id`             | `string`                                                         | `""`                       | HTML id attribute for the button          |
| `className`      | `string`                                                         | `undefined`                | Additional CSS classes                    |
| `style`          | `React.CSSProperties`                                            | `{}`                       | Inline styles for the button              |
| `color`          | `string`                                                         | `"#3535f3"`                | Background color of the button            |
| `textColor`      | `string`                                                         | `"#ffffff"`                | Text and icon color                       |
| `width`          | `string`                                                         | `"296px"`                  | Width of the button                       |
| `height`         | `string`                                                         | `"48px"`                   | Height of the button                      |
| `confirmingText` | `string`                                                         | `"Confirming"`             | Text shown during confirmation process    |
| `confirmedText`  | `string`                                                         | `"Confirmed"`              | Text shown after successful confirmation  |
| `loadingText`    | `string`                                                         | `"Processing..."`          | Text shown during async operation         |
| `icon`           | `React.ReactNode`                                                | `<IcChevronRight />`       | Icon displayed in idle state              |
| `confirmIcon`    | `React.ReactNode`                                                | `<IcConfirm />`            | Icon displayed in confirmed state         |
| `loadingIcon`    | `React.ReactNode`                                                | Spinner animation          | Icon displayed during loading state       |
| `stateText`      | `{ confirming?: string; loading?: string; confirmed?: string; }` | `undefined`                | Object to override state-specific text    |

### State Management

The component manages four distinct states internally:

```typescript
type SwipeButtonState =
  | "idle" // Default state, ready for interaction
  | "confirming" // Momentary state when swipe reaches threshold
  | "loading" // During async onConfirm execution
  | "confirmed"; // After successful completion
```

## Basic Usage

### Simple Confirmation

```typescript
import { SwipeButton } from "gends";

// Basic swipe button
<SwipeButton
  text="Swipe to confirm"
  onConfirm={() => console.log("Action confirmed!")}
/>

// Custom text and handler
<SwipeButton
  text="Swipe to delete account"
  onConfirm={handleAccountDeletion}
  color="#dc2626"
  confirmingText="Deleting..."
  confirmedText="Account deleted"
/>
```

### Async Operations

```typescript
// Promise-based confirmation
<SwipeButton
  text="Swipe to process payment"
  onConfirm={async () => {
    await processPayment();
    showSuccessNotification();
  }}
  loadingText="Processing payment..."
  confirmedText="Payment successful!"
/>

// Error handling with automatic reset
<SwipeButton
  text="Swipe to submit"
  onConfirm={async () => {
    try {
      await submitData();
    } catch (error) {
      // Button automatically resets to idle on error
      showErrorMessage(error.message);
      throw error; // Re-throw to ensure proper state handling
    }
  }}
/>
```

## Visual Customization

### Size Variants

```typescript
// Compact size
<SwipeButton
  text="Swipe to confirm"
  width="240px"
  height="40px"
/>

// Large size
<SwipeButton
  text="Swipe to authorize payment"
  width="400px"
  height="60px"
/>

// Full width responsive
<SwipeButton
  text="Swipe to continue"
  className="w-full max-w-md"
  style={{ minWidth: "280px" }}
/>
```

### Color Customization

```typescript
// Primary action (default)
<SwipeButton
  text="Swipe to save"
  color="#3535f3"
  textColor="#ffffff"
/>

// Success action
<SwipeButton
  text="Swipe to approve"
  color="#22c55e"
  textColor="#ffffff"
/>

// Warning action
<SwipeButton
  text="Swipe to archive"
  color="#f59e0b"
  textColor="#ffffff"
/>

// Destructive action
<SwipeButton
  text="Swipe to delete"
  color="#ef4444"
  textColor="#ffffff"
/>

// Custom gradient styling
<SwipeButton
  text="Swipe to unlock"
  style={{
    background: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)",
    border: "2px solid #4f46e5",
    boxShadow: "0 4px 15px rgba(79, 70, 229, 0.3)",
  }}
/>
```

### Icon Customization

```typescript
import { IcConfirm, IcStatusLoading   } from "gends";

// Payment flow with card icon
<SwipeButton
  text="Swipe to pay $25.99"
  icon={<CreditCard className="h-5 w-5" />}
  confirmIcon={<IcConfirm className="w-6 h-6 text-current" />}
  loadingIcon={<IcStatusLoading className="w-6 h-6 text-current" />}
/>



// Custom animated loading icon
<SwipeButton
  text="Swipe to process"
  loadingIcon={
    <div className="relative">
      <div className="animate-pulse w-5 h-5 bg-current rounded-full opacity-75" />
      <div className="absolute inset-0 animate-ping w-5 h-5 bg-current rounded-full opacity-25" />
    </div>
  }
/>
```

## State Text Customization

### Individual State Text

```typescript
// Custom text for each state
<SwipeButton
  text="Swipe to send money"
  confirmingText="Authorizing..."
  loadingText="Transferring funds..."
  confirmedText="Transfer complete!"
/>

// Using stateText object for centralized control
<SwipeButton
  text="Swipe to backup data"
  stateText={{
    confirming: "Initiating backup...",
    loading: "Uploading to cloud...",
    confirmed: "Backup successful!"
  }}
/>
```

### Contextual Messaging

```typescript
// E-commerce checkout
<SwipeButton
  text="Swipe to place order"
  confirmingText="Confirming order..."
  loadingText="Processing payment..."
  confirmedText="Order placed successfully!"
/>

// Data management
<SwipeButton
  text="Swipe to sync changes"
  confirmingText="Preparing sync..."
  loadingText="Syncing with server..."
  confirmedText="All changes synced!"
/>

// User account actions
<SwipeButton
  text="Swipe to activate premium"
  confirmingText="Activating..."
  loadingText="Updating account..."
  confirmedText="Premium activated!"
/>
```

## Real-World Examples

### 1. Payment Processing

```typescript
const PaymentSwipeButton = ({ amount, currency, onPaymentSuccess }) => {
  const [isProcessing, setIsProcessing] = useState(false);

  const handlePayment = async () => {
    setIsProcessing(true);
    try {
      const paymentResult = await processPayment({
        amount,
        currency,
        method: 'card'
      });

      if (paymentResult.success) {
        onPaymentSuccess(paymentResult);
        showNotification('Payment successful!', 'success');
      } else {
        throw new Error(paymentResult.error);
      }
    } catch (error) {
      showNotification(`Payment failed: ${error.message}`, 'error');
      throw error; // Ensure button resets
    } finally {
      setIsProcessing(false);
    }
  };

  return (
    <div className="max-w-sm mx-auto p-6">
      <div className="mb-4 text-center">
        <h3 className="text-lg font-semibold">Complete Payment</h3>
        <p className="text-2xl font-bold text-primary">
          {currency}{amount.toFixed(2)}
        </p>
      </div>

      <SwipeButton
        text={`Swipe to pay ${currency}${amount.toFixed(2)}`}
        onConfirm={handlePayment}
        disabled={isProcessing}
        color="#22c55e"
        confirmingText="Authorizing payment..."
        loadingText="Processing payment..."
        confirmedText="Payment successful!"
        icon={<CreditCard className="h-5 w-5" />}
        confirmIcon={<IcConfirm className="w-6 h-6 text-current" />}
        width="100%"
        className="w-full"
      />

      <p className="text-xs text-gray-500 text-center mt-2">
        Slide to confirm your payment
      </p>
    </div>
  );
};
```

### 2. Account Deletion

```typescript
const AccountDeletionButton = ({ userId, onAccountDeleted }) => {
  const [confirmationStep, setConfirmationStep] = useState(0);

  const handleAccountDeletion = async () => {
    if (confirmationStep < 1) {
      setConfirmationStep(1);
      return;
    }

    try {
      await deleteUserAccount(userId);
      await clearUserData(userId);
      onAccountDeleted();
      router.push('/goodbye');
    } catch (error) {
      showError('Failed to delete account. Please try again.');
      throw error;
    }
  };

  return (
    <div className="max-w-md mx-auto p-6 border border-red-200 rounded-lg bg-red-50">
      <div className="mb-6">
        <h3 className="text-lg font-semibold text-red-800">
          Delete Account
        </h3>
        <p className="text-sm text-red-600 mt-2">
          This action cannot be undone. All your data will be permanently deleted.
        </p>
      </div>

      {confirmationStep === 0 ? (
        <SwipeButton
          text="Swipe to confirm deletion"
          onConfirm={handleAccountDeletion}
          color="#dc2626"
          confirmingText="Are you sure?"
          icon={<AlertTriangle className="h-5 w-5" />}
          width="100%"
        />
      ) : (
        <SwipeButton
          text="Swipe again to delete permanently"
          onConfirm={handleAccountDeletion}
          color="#991b1b"
          confirmingText="Deleting account..."
          loadingText="Removing all data..."
          confirmedText="Account deleted"
          icon={<Trash2 className="h-5 w-5" />}
          confirmIcon={<IcConfirm className="w-6 h-6 text-current" />}
          width="100%"
        />
      )}

      <button
        onClick={() => setConfirmationStep(0)}
        className="w-full mt-3 text-sm text-gray-600 hover:text-gray-800"
      >
        Cancel
      </button>
    </div>
  );
};
```

### 3. File Upload Confirmation

```typescript
const FileUploadConfirmation = ({ files, onUploadComplete }) => {
  const [uploadProgress, setUploadProgress] = useState(0);

  const handleFileUpload = async () => {
    try {
      const uploadPromises = files.map(async (file, index) => {
        const formData = new FormData();
        formData.append('file', file);

        const response = await fetch('/api/upload', {
          method: 'POST',
          body: formData,
          onUploadProgress: (progressEvent) => {
            const progress = (progressEvent.loaded / progressEvent.total) * 100;
            setUploadProgress(Math.round(progress));
          }
        });

        if (!response.ok) {
          throw new Error(`Failed to upload ${file.name}`);
        }

        return await response.json();
      });

      const results = await Promise.all(uploadPromises);
      onUploadComplete(results);
    } catch (error) {
      showError(`Upload failed: ${error.message}`);
      throw error;
    }
  };

  const totalSize = files.reduce((sum, file) => sum + file.size, 0);
  const formattedSize = formatFileSize(totalSize);

  return (
    <div className="max-w-lg mx-auto p-6">
      <div className="mb-6">
        <h3 className="text-lg font-semibold">Upload Files</h3>
        <p className="text-sm text-gray-600">
          {files.length} file{files.length !== 1 ? 's' : ''} • {formattedSize}
        </p>

        <div className="mt-4 space-y-2">
          {files.map((file, index) => (
            <div key={index} className="flex items-center text-sm">
              <FileIcon className="h-4 w-4 mr-2 text-gray-400" />
              <span className="truncate">{file.name}</span>
              <span className="ml-auto text-gray-500">
                {formatFileSize(file.size)}
              </span>
            </div>
          ))}
        </div>
      </div>

      <SwipeButton
        text="Swipe to upload files"
        onConfirm={handleFileUpload}
        color="#3b82f6"
        confirmingText="Starting upload..."
        loadingText={`Uploading... ${uploadProgress}%`}
        confirmedText="Upload complete!"
        icon={<Upload className="h-5 w-5" />}
        confirmIcon={<IcConfirm className="w-6 h-6 text-current" />}
        loadingIcon={<Loader2 className="h-5 w-5 animate-spin" />}
        width="100%"
      />
    </div>
  );
};
```

### 4. Authentication Action

```typescript
const BiometricAuthButton = ({ onAuthSuccess }) => {
  const [authMethod, setAuthMethod] = useState('fingerprint');

  const handleBiometricAuth = async () => {
    try {
      // Check if biometric authentication is available
      if (!('credentials' in navigator)) {
        throw new Error('Biometric authentication not supported');
      }

      const credential = await navigator.credentials.create({
        publicKey: {
          challenge: new Uint8Array(32),
          rp: { name: "Your App" },
          user: {
            id: new Uint8Array(16),
            name: "user@example.com",
            displayName: "User"
          },
          pubKeyCredParams: [{ alg: -7, type: "public-key" }],
          authenticatorSelection: {
            authenticatorAttachment: "platform"
          }
        }
      });

      if (credential) {
        onAuthSuccess(credential);
      } else {
        throw new Error('Authentication failed');
      }
    } catch (error) {
      showError(`Authentication failed: ${error.message}`);
      throw error;
    }
  };

  return (
    <div className="max-w-sm mx-auto p-6">
      <div className="text-center mb-6">
        <div className="w-16 h-16 mx-auto mb-4 bg-blue-100 rounded-full flex items-center justify-center">
          <Shield className="h-8 w-8 text-blue-600" />
        </div>
        <h3 className="text-lg font-semibold">Secure Authentication</h3>
        <p className="text-sm text-gray-600 mt-2">
          Use your biometric authentication to proceed
        </p>
      </div>

      <SwipeButton
        text="Swipe to authenticate"
        onConfirm={handleBiometricAuth}
        color="#1e40af"
        confirmingText="Authenticating..."
        loadingText="Verifying identity..."
        confirmedText="Authentication successful!"
        icon={<Fingerprint className="h-5 w-5" />}
        confirmIcon={<ShieldCheck className="h-5 w-5" />}
        width="100%"
      />

      <div className="mt-4 text-center">
        <button className="text-sm text-blue-600 hover:text-blue-800">
          Use password instead
        </button>
      </div>
    </div>
  );
};
```

### 5. Subscription Management

```typescript
const SubscriptionCancelButton = ({ subscription, onCancellationComplete }) => {
  const [retentionOffer, setRetentionOffer] = useState(null);
  const [showConfirmation, setShowConfirmation] = useState(false);

  const handleCancellation = async () => {
    if (!showConfirmation) {
      // First swipe - show retention offer
      setRetentionOffer({
        discount: 50,
        duration: 3,
        originalPrice: subscription.price
      });
      setShowConfirmation(true);
      return;
    }

    try {
      // Actually cancel the subscription
      await cancelSubscription(subscription.id);
      await sendCancellationEmail(subscription.userEmail);
      onCancellationComplete();
    } catch (error) {
      showError('Failed to cancel subscription. Please contact support.');
      throw error;
    }
  };

  const acceptRetentionOffer = async () => {
    try {
      await applyRetentionOffer(subscription.id, retentionOffer);
      showSuccess('Discount applied! Your subscription continues.');
    } catch (error) {
      showError('Failed to apply discount. Please try again.');
    }
  };

  return (
    <div className="max-w-md mx-auto p-6">
      <div className="mb-6">
        <h3 className="text-lg font-semibold">Cancel Subscription</h3>
        <p className="text-sm text-gray-600">
          Current plan: {subscription.planName} - ${subscription.price}/month
        </p>
      </div>

      {retentionOffer && !showConfirmation && (
        <div className="mb-6 p-4 bg-green-50 border border-green-200 rounded-lg">
          <h4 className="font-medium text-green-800">Special Offer!</h4>
          <p className="text-sm text-green-700 mt-1">
            Stay subscribed and get {retentionOffer.discount}% off for {retentionOffer.duration} months
          </p>
          <button
            onClick={acceptRetentionOffer}
            className="mt-3 bg-green-600 text-white px-4 py-2 rounded text-sm hover:bg-green-700"
          >
            Accept Offer
          </button>
        </div>
      )}

      <SwipeButton
        text={!showConfirmation
          ? "Swipe to cancel subscription"
          : "Swipe again to confirm cancellation"
        }
        onConfirm={handleCancellation}
        color={!showConfirmation ? "#f59e0b" : "#dc2626"}
        confirmingText={!showConfirmation
          ? "Processing..."
          : "Cancelling subscription..."
        }
        loadingText="Finalizing cancellation..."
        confirmedText="Subscription cancelled"
        icon={<XCircle className="h-5 w-5" />}
        confirmIcon={<IcConfirm className="w-6 h-6 text-current" />}
        width="100%"
      />

      <div className="mt-4 text-center">
        <button
          onClick={() => {
            setShowConfirmation(false);
            setRetentionOffer(null);
          }}
          className="text-sm text-gray-600 hover:text-gray-800"
        >
          Keep my subscription
        </button>
      </div>
    </div>
  );
};
```

## Accessibility Features

### Keyboard Navigation

The component supports full keyboard accessibility:

```typescript
// Keyboard activation
<SwipeButton
  text="Swipe or press Enter to confirm"
  onConfirm={handleConfirmation}
  aria-label="Confirm action by swiping or pressing Enter"
/>

// Focus management
<SwipeButton
  text="Swipe to submit"
  onConfirm={handleSubmit}
  onKeyDown={(e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      handleSubmit();
    }
  }}
/>
```

### Screen Reader Support

```typescript
// Enhanced ARIA attributes
<SwipeButton
  text="Swipe to delete"
  onConfirm={handleDeletion}
  aria-label="Delete item by swiping or pressing Enter"
  aria-describedby="deletion-warning"
  role="button"
  tabIndex={0}
/>

<p id="deletion-warning" className="sr-only">
  This action cannot be undone. The item will be permanently deleted.
</p>
```

### Visual Accessibility

```typescript
// High contrast support
<SwipeButton
  text="Swipe to confirm"
  className="high-contrast:border-2 high-contrast:border-white"
  style={{
    '--high-contrast-bg': '#000000',
    '--high-contrast-text': '#ffffff'
  }}
/>

// Focus indicators
<SwipeButton
  text="Swipe to proceed"
  className="focus:ring-4 focus:ring-blue-300 focus:ring-opacity-50"
/>
```

## States and Behavior

### Disabled State

```typescript
// Static disabled state
<SwipeButton
  text="Action not available"
  disabled={true}
  className="opacity-50 cursor-not-allowed"
/>

// Conditional disabled state
const [isFormValid, setIsFormValid] = useState(false);

<SwipeButton
  text={isFormValid ? "Swipe to submit" : "Complete form to continue"}
  disabled={!isFormValid}
  onConfirm={handleSubmit}
/>
```

### Loading State Management

```typescript
const [isExternalLoading, setIsExternalLoading] = useState(false);

<SwipeButton
  text="Swipe to sync"
  disabled={isExternalLoading}
  onConfirm={async () => {
    setIsExternalLoading(true);
    try {
      await performSyncOperation();
    } finally {
      setIsExternalLoading(false);
    }
  }}
  loadingText={isExternalLoading ? "Syncing data..." : "Processing..."}
/>
```

### Error Handling

```typescript
const SwipeButtonWithRetry = ({ onConfirm, maxRetries = 3 }) => {
  const [retryCount, setRetryCount] = useState(0);
  const [lastError, setLastError] = useState(null);

  const handleConfirmWithRetry = async () => {
    try {
      setLastError(null);
      await onConfirm();
      setRetryCount(0); // Reset on success
    } catch (error) {
      setLastError(error);
      setRetryCount(prev => prev + 1);

      if (retryCount < maxRetries - 1) {
        showError(`Attempt failed. ${maxRetries - retryCount - 1} retries remaining.`);
      } else {
        showError('All attempts failed. Please try again later.');
      }

      throw error; // Ensure button resets
    }
  };

  return (
    <div>
      <SwipeButton
        text={retryCount > 0 ? `Swipe to retry (${retryCount}/${maxRetries})` : "Swipe to confirm"}
        onConfirm={handleConfirmWithRetry}
        disabled={retryCount >= maxRetries}
        color={retryCount > 0 ? "#f59e0b" : "#3535f3"}
      />

      {lastError && (
        <p className="text-sm text-red-600 mt-2">
          Error: {lastError.message}
        </p>
      )}
    </div>
  );
};
```

## Design System Integration

### Genesis Design Tokens

The component integrates with Genesis Design System tokens:

```css
/* Button dimensions */
--swipe-button-width: 296px;
--swipe-button-height: 48px;
--swipe-thumb-size: 40px;

/* Spacing */
--swipe-padding: var(--gd-spacing-4);
--swipe-thumb-margin: var(--gd-spacing-4);

/* Colors */
--swipe-bg-primary: var(--gd-color-primary-50);
--swipe-text-inverse: var(--gd-color-text-default-inverse);
--swipe-thumb-bg: var(--gd-color-neutral-white);

/* Typography */
--swipe-text-style: var(--gd-typography-en-desktop-body-xl-prominent);

/* Animation */
--swipe-transition-duration: var(--gd-motion-duration-fast);
--swipe-easing: var(--gd-motion-easing-standard);
```

### Theme Support

```typescript
// Light/Dark mode compatibility
<SwipeButton
  text="Swipe to confirm"
  className="
    bg-primary-500 dark:bg-primary-400
    text-white dark:text-gray-900
  "
  style={{
    backgroundColor: 'var(--color-primary)',
    color: 'var(--color-on-primary)'
  }}
/>

// Custom theme integration
<SwipeButton
  text="Swipe to proceed"
  className="theme-ocean"
  color="var(--ocean-primary)"
  textColor="var(--ocean-on-primary)"
/>
```

## Best Practices

### UX Guidelines

- **Clear Intent**: Use descriptive text that clearly indicates the action
- **Appropriate Context**: Reserve for high-stakes or irreversible actions
- **Visual Feedback**: Provide clear state transitions and confirmations
- **Error Recovery**: Always handle errors gracefully with user feedback

```typescript
// Good: Clear, descriptive text
<SwipeButton text="Swipe to delete 5 selected items" />

// Avoid: Vague text
<SwipeButton text="Swipe to continue" />

// Good: Context-appropriate usage
<SwipeButton text="Swipe to cancel subscription" />

// Avoid: Overuse for simple actions
<SwipeButton text="Swipe to close modal" />
```

### Performance Optimization

```typescript
// Memoize expensive operations
const ExpensiveSwipeButton = memo(({ data, onConfirm }) => {
  const processedData = useMemo(() =>
    expensiveDataProcessing(data),
    [data]
  );

  const handleConfirm = useCallback(async () => {
    await onConfirm(processedData);
  }, [onConfirm, processedData]);

  return (
    <SwipeButton
      text="Swipe to process data"
      onConfirm={handleConfirm}
    />
  );
});
```

### State Management

```typescript
// Custom hook for swipe button state
const useSwipeButtonState = initialText => {
  const [state, setState] = useState("idle");
  const [text, setText] = useState(initialText);

  const updateState = useCallback((newState, newText) => {
    setState(newState);
    if (newText) setText(newText);
  }, []);

  const resetState = useCallback(() => {
    setState("idle");
    setText(initialText);
  }, [initialText]);

  return { state, text, updateState, resetState };
};
```

## Troubleshooting

### Common Issues

**Swipe not triggering confirmation**

```typescript
// Ensure proper touch event handling
<SwipeButton
  text="Swipe to confirm"
  onConfirm={handleConfirm}
  style={{ touchAction: 'pan-x' }} // Allow horizontal panning
/>

// Check for container interference
<div style={{ overflow: 'visible' }}> {/* Avoid overflow: hidden */}
  <SwipeButton />
</div>
```

**Button not resetting after error**

```typescript
// Ensure errors are properly thrown
<SwipeButton
  onConfirm={async () => {
    try {
      await riskyOperation();
    } catch (error) {
      showError(error.message);
      throw error; // Required for proper reset
    }
  }}
/>
```

**Performance issues with frequent re-renders**

```typescript
// Stable onConfirm reference
const handleConfirm = useCallback(async () => {
  await performAction();
}, [/* dependencies */]);

<SwipeButton
  text="Swipe to confirm"
  onConfirm={handleConfirm} // Stable reference prevents re-renders
/>
```

### Browser Compatibility

```typescript
// Touch event fallbacks
<SwipeButton
  text="Swipe to confirm"
  onConfirm={handleConfirm}
  // Component automatically handles both touch and mouse events
  className="
    supports-touch:cursor-default
    supports-no-touch:cursor-pointer
  "
/>
```

## Migration Guide

### From Standard Button

```typescript
// Before: Standard button with confirmation
const [showConfirm, setShowConfirm] = useState(false);

{!showConfirm ? (
  <button onClick={() => setShowConfirm(true)}>
    Delete Item
  </button>
) : (
  <div>
    <button onClick={handleDelete}>Confirm Delete</button>
    <button onClick={() => setShowConfirm(false)}>Cancel</button>
  </div>
)}

// After: Swipe button
<SwipeButton
  text="Swipe to delete item"
  onConfirm={handleDelete}
  color="#dc2626"
/>
```

### From Modal Confirmation

```typescript
// Before: Modal-based confirmation
const [showModal, setShowModal] = useState(false);

<button onClick={() => setShowModal(true)}>Delete</button>
<Modal isOpen={showModal}>
  <p>Are you sure?</p>
  <button onClick={handleDelete}>Confirm</button>
  <button onClick={() => setShowModal(false)}>Cancel</button>
</Modal>

// After: Inline swipe confirmation
<SwipeButton
  text="Swipe to delete"
  onConfirm={handleDelete}
  confirmingText="Deleting..."
  confirmedText="Deleted successfully!"
/>
```

## Summary

The Swipe Button component provides a secure and intuitive way to handle critical user actions requiring intentional confirmation. Key features include:

- **Gesture-based Interaction**: Touch and mouse swipe gestures for confirmation
- **State Management**: Automatic handling of idle, confirming, loading, and confirmed states
- **Customizable Appearance**: Full control over colors, sizes, icons, and text
- **Async Operation Support**: Built-in handling of Promise-based operations
- **Accessibility**: Keyboard navigation and screen reader support
- **Error Handling**: Automatic reset on failed operations
- **Genesis Integration**: Design system tokens and theming support

Use the Swipe Button for payment confirmations, account deletions, data submissions, and any action where accidental activation could have significant consequences. The component ensures user intent while providing smooth, accessible interactions across all devices.
