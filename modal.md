# Modal

A versatile modal dialog component that supports multiple sizes, customizable headers and footers, button configurations, overflow detection, and comprehensive content management.

---

## 1. Quick start

```tsx
import { Modal } from "gends";

function Example() {
  const [open, setOpen] = useState(false);

  return (
    <Modal
      open={open}
      setOpen={setOpen}
      headerTitle="Confirm Action"
      description="Are you sure you want to continue?"
      primaryButtonProps={{
        title: "Confirm",
        onClick: () => handleConfirm(),
      }}
    />
  );
}
```

---

## 2. Sizes

| size     | Max width | Use case                |
| -------- | --------- | ----------------------- |
| `xSmall` | 560px     | Simple confirmations    |
| `small`  | 754px     | Basic forms and dialogs |
| `medium` | 950px     | Standard content modals |
| `large`  | 1392px    | Complex forms and data  |
| `full`   | Full      | Full-screen experiences |

```tsx
<Modal size="xSmall" headerTitle="Quick Confirmation" />
<Modal size="small" headerTitle="Simple Form" />
<Modal size="medium" headerTitle="Standard Dialog" />
<Modal size="large" headerTitle="Complex Interface" />
<Modal size="full" headerTitle="Full Experience" />
```

---

## 3. Header configurations

| header type | Description                | Use case                   |
| ----------- | -------------------------- | -------------------------- |
| Default     | Title with close button    | Standard modals            |
| Custom      | Custom header content      | Branded or complex headers |
| With back   | Title with back and close  | Multi-step workflows       |
| With slot   | Additional header elements | Extra actions or info      |

```tsx
// Default header
<Modal headerTitle="Standard Header" description="Modal description" />

// Custom header
<Modal
  header={
    <div className="flex justify-between items-center p-4">
      <h2>Custom Header</h2>
      <Badge>New</Badge>
    </div>
  }
/>

// Header with back button
<Modal
  headerTitle="Step 2"
  showBackButton={true}
  onBack={() => goToPreviousStep()}
/>

// Header with additional content
<Modal
  headerTitle="Settings"
  headerSlot={<Button size="s">Reset</Button>}
/>
```

---

## 4. Footer configurations

| footer type | Description                   | Use case                 |
| ----------- | ----------------------------- | ------------------------ |
| Default     | Primary and secondary buttons | Standard actions         |
| Custom      | Custom footer content         | Complex action layouts   |
| Hidden      | No footer                     | Content-only modals      |
| With slot   | Additional footer elements    | Extra context or actions |

```tsx
// Default footer with buttons
<Modal
  showPrimaryBtn={true}
  showSecondaryBtn={true}
  primaryButtonProps={{ title: "Save", onClick: handleSave }}
  secondaryButtonProps={{ title: "Cancel", onClick: handleCancel }}
/>

// Custom footer
<Modal
  footer={
    <div className="flex justify-between p-4">
      <Button kind="tertiary">More Options</Button>
      <div className="flex gap-2">
        <Button kind="secondary">Cancel</Button>
        <Button kind="primary">Confirm</Button>
      </div>
    </div>
  }
/>

// No footer
<Modal showFooter={false} />

// Footer with additional content
<Modal
  footerSlot={<p className="text-sm text-gray-500">Last saved 5 minutes ago</p>}
/>
```

---

## 5. Button configurations

```tsx
// Primary button only
<Modal
  showPrimaryBtn={true}
  showSecondaryBtn={false}
  primaryButtonProps={{
    title: "Continue",
    kind: "primary",
    appearance: "positive",
    onClick: handleContinue
  }}
/>

// Custom button behavior
<Modal
  primaryButtonProps={{
    title: "Delete",
    kind: "primary",
    appearance: "negative",
    onClick: handleDelete,
    disabled: !canDelete
  }}
  secondaryButtonProps={{
    title: "Keep",
    kind: "secondary",
    onClick: handleKeep
  }}
  primaryClose={true}  // Close modal after primary action
  secondaryClose={false} // Keep modal open after secondary action
/>
```

---

## 6. Content and states

```tsx
// With children content
<Modal headerTitle="Custom Content">
  <div className="space-y-4">
    <FormField label="Name" />
    <FormField label="Email" />
    <FormField label="Message" />
  </div>
</Modal>

// Acknowledgment style (centered)
<Modal
  acknowledgement={true}
  headerTitle="Success!"
  description="Your changes have been saved successfully."
/>

// No padding for custom layouts
<Modal noPadding={true} headerTitle="Custom Layout">
  <div className="p-8 bg-gradient-to-r from-blue-500 to-purple-600">
    Custom styled content
  </div>
</Modal>

// Without description
<Modal showDesc={false} headerTitle="No Description">
  <CustomContent />
</Modal>
```

---

## 7. Advanced features

```tsx
// Overflow detection with shadow
<Modal
  headerTitle="Long Content"
  hideFooterShadow={false} // Show shadow when content overflows
>
  <div className="h-[600px]">Very long content that scrolls...</div>
</Modal>

// No trigger button (controlled externally)
<Modal
  noTriggerBtn={true}
  open={isOpen}
  setOpen={setIsOpen}
  headerTitle="Externally Controlled"
/>

// Custom modal button
<Modal
  modalButton={<Button kind="secondary">Custom Trigger</Button>}
  headerTitle="Custom Trigger Modal"
/>

// Custom width
<Modal
  customWidth="600px"
  headerTitle="Custom Width Modal"
/>
```

---

## 8. Full prop reference

### Basic Props

| Prop          | Type       | Default                              | Description            |
| ------------- | ---------- | ------------------------------------ | ---------------------- |
| `size`        | `SizeKeys` | `'medium'`                           | Modal size variant     |
| `customWidth` | `string`   | -                                    | Custom width override  |
| `headerTitle` | `string`   | `"Leave page with unsaved changes?"` | Modal header title     |
| `description` | `string`   | `""`                                 | Modal description text |
| `btnTitle`    | `string`   | `"Open"`                             | Trigger button text    |

### Content Props

| Prop          | Type        | Default | Description                    |
| ------------- | ----------- | ------- | ------------------------------ |
| `children`    | `ReactNode` | `<></>` | Modal body content             |
| `supportText` | `string`    | -       | Additional header support text |
| `showDesc`    | `boolean`   | `true`  | Show description text          |
| `noPadding`   | `boolean`   | `false` | Remove default content padding |

### Display Props

| Prop              | Type       | Default | Description                         |
| ----------------- | ---------- | ------- | ----------------------------------- |
| `open`            | `boolean`  | -       | Controlled open state               |
| `setOpen`         | `function` | -       | Open state setter                   |
| `acknowledgement` | `boolean`  | `false` | Center-aligned acknowledgment style |
| `noTriggerBtn`    | `boolean`  | `false` | Hide default trigger button         |

### Header Props

| Prop             | Type        | Default         | Description                |
| ---------------- | ----------- | --------------- | -------------------------- |
| `header`         | `ReactNode` | -               | Custom header content      |
| `headerSlot`     | `ReactNode` | -               | Additional header elements |
| `headerClasses`  | `string`    | Default classes | Custom header CSS classes  |
| `showBackButton` | `boolean`   | `false`         | Show back button in header |
| `onBack`         | `function`  | -               | Back button click handler  |

### Footer Props

| Prop               | Type        | Default         | Description                |
| ------------------ | ----------- | --------------- | -------------------------- |
| `footer`           | `ReactNode` | -               | Custom footer content      |
| `footerSlot`       | `ReactNode` | -               | Additional footer elements |
| `footerClasses`    | `string`    | Default classes | Custom footer CSS classes  |
| `showFooter`       | `boolean`   | `true`          | Show footer section        |
| `hideFooterShadow` | `boolean`   | `false`         | Hide overflow shadow       |

### Button Props

| Prop                   | Type          | Default | Description                        |
| ---------------------- | ------------- | ------- | ---------------------------------- |
| `showPrimaryBtn`       | `boolean`     | `true`  | Show primary action button         |
| `showSecondaryBtn`     | `boolean`     | `true`  | Show secondary action button       |
| `primaryButtonProps`   | `ButtonProps` | Default | Primary button configuration       |
| `secondaryButtonProps` | `ButtonProps` | Default | Secondary button configuration     |
| `primaryClose`         | `boolean`     | `false` | Close modal after primary action   |
| `secondaryClose`       | `boolean`     | `true`  | Close modal after secondary action |

### ButtonProps Object

| Property   | Type         | Description          |
| ---------- | ------------ | -------------------- |
| `title`    | `string`     | Button text          |
| `onClick`  | `function`   | Click handler        |
| `kind`     | `ButtonKind` | Button style variant |
| `disabled` | `boolean`    | Disable button       |

### Trigger Props

| Prop          | Type        | Description                     |
| ------------- | ----------- | ------------------------------- |
| `modalButton` | `ReactNode` | Custom trigger button component |

---

## 9. Recipes

### Simple confirmation modal

```tsx
<Modal
  size="xSmall"
  headerTitle="Delete Item"
  description="This action cannot be undone."
  primaryButtonProps={{
    title: "Delete",
    kind: "primary",
    appearance: "negative",
    onClick: handleDelete,
  }}
  secondaryButtonProps={{
    title: "Cancel",
    kind: "secondary",
    onClick: handleCancel,
  }}
  primaryClose={true}
/>
```

### Multi-step form modal

```tsx
<Modal
  size="medium"
  headerTitle={`Step ${currentStep} of 3`}
  showBackButton={currentStep > 1}
  onBack={goToPreviousStep}
  primaryButtonProps={{
    title: currentStep === 3 ? "Finish" : "Next",
    onClick: currentStep === 3 ? handleFinish : goToNextStep,
  }}
  secondaryButtonProps={{
    title: "Cancel",
    onClick: handleCancel,
  }}
>
  <StepContent step={currentStep} />
</Modal>
```

### Success acknowledgment modal

```tsx
<Modal
  size="small"
  acknowledgement={true}
  headerTitle="Success!"
  description="Your account has been created successfully."
  showSecondaryBtn={false}
  primaryButtonProps={{
    title: "Continue",
    kind: "primary",
    appearance: "positive",
    onClick: handleContinue,
  }}
  primaryClose={true}
/>
```

### Custom content modal

```tsx
<Modal
  size="large"
  noPadding={true}
  headerTitle="Data Visualization"
  header={
    <div className="flex justify-between items-center p-6 border-b">
      <h2 className="text-xl font-semibold">Advanced Analytics</h2>
      <Badge variant="success">Live Data</Badge>
    </div>
  }
  footer={
    <div className="flex justify-between items-center p-6 border-t">
      <p className="text-sm text-gray-500">Last updated: {lastUpdate}</p>
      <div className="flex gap-2">
        <Button kind="secondary">Export</Button>
        <Button kind="primary">Refresh</Button>
      </div>
    </div>
  }
>
  <DataVisualizationComponent />
</Modal>
```

### Controlled modal with external trigger

```tsx
const [isOpen, setIsOpen] = useState(false);

// External trigger
<Button onClick={() => setIsOpen(true)}>
  Open Custom Modal
</Button>

// Modal component
<Modal
  noTriggerBtn={true}
  open={isOpen}
  setOpen={setIsOpen}
  size="medium"
  headerTitle="Externally Controlled"
  description="This modal is opened by an external trigger."
/>
```

### Loading state modal

```tsx
<Modal
  headerTitle="Processing..."
  description="Please wait while we process your request."
  showSecondaryBtn={false}
  primaryButtonProps={{
    title: "Processing...",
    disabled: true,
    kind: "primary",
  }}
>
  <div className="flex justify-center py-8">
    <LoadingSpinner />
  </div>
</Modal>
```

---

## 10. Accessibility

The Modal component includes comprehensive accessibility features:

- Focus trap within modal content
- Keyboard navigation support (Escape to close)
- Proper ARIA attributes and roles
- Focus restoration to trigger element
- Screen reader announcements

```tsx
<Modal
  headerTitle="Accessible Modal"
  description="This modal follows accessibility best practices"
  role="dialog"
  aria-labelledby="modal-title"
  aria-describedby="modal-description"
>
  <AccessibleContent />
</Modal>
```

---

## 11. Design Tokens

The Modal component uses the following design system tokens:

**Sizing:**

- XSmall: `sm:max-w-[560px]`
- Small: `sm:max-w-[754px]`
- Medium: `sm:max-w-[950px]`
- Large: `sm:max-w-[1392px]`
- Full: `sm:max-w-full`

**Spacing:**

- Header padding: `py-gd-12 px-gd-16`
- Content padding: `px-gd-20 py-gd-16` (when not `noPadding`)
- Footer padding: `py-gd-16 px-gd-24`
- Content gap: `gap-gd-12`

**Colors:**

- Header background: `bg-color-background-surface-20`
- Footer background: `bg-color-background-surface-0`
- Shadow: `shadow-[0px_4px_16px_0px_hsla(0,0%,0%,0.16)]`

**Layout:**

- Border radius: `rounded-t-gd-16` (header), `rounded-b-gd-16` (footer)
- Content max height: `max-h-[494px]` with `overflow-y-auto`
- Footer shadow: `shadow-top` when content overflows

---

Consider using Modal with:

- **Form** — For complex input dialogs
- **Confirmation** — For destructive actions
- **Settings** — For configuration panels
- **Viewer** — For content preview
- **Wizard** — For multi-step processes
