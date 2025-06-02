# Popover

A flexible popover component for displaying contextual content, forms, and confirmations with customizable headers, bodies, and footers.

---

## 1. Quick start

```tsx
import { Popover } from "gends";

function Example() {
  const [open, setOpen] = useState(false);

  return (
    <Popover
      open={open}
      onOpenChange={setOpen}
      title="Confirm Action"
      trigger={<Button>Open Popover</Button>}
      bodySlotContent="Are you sure you want to proceed?"
      primaryButtonLabel="Confirm"
      onPrimaryButtonClick={() => {
        console.log("Confirmed");
        setOpen(false);
      }}
    />
  );
}
```

---

## 2. Sizes

| size    | Width | Padding | Use case                        |
| ------- | ----- | ------- | ------------------------------- |
| `small` | 364px | 12px    | Simple forms, confirmations     |
| `large` | 364px | 16px    | Complex forms, detailed content |

```tsx
<Popover size="small" title="Small Popover" trigger={<Button>Small</Button>} />
<Popover size="large" title="Large Popover" trigger={<Button>Large</Button>} />
```

---

## 3. Content sections

The popover consists of three main sections:

| Section  | Purpose            | Features                            |
| -------- | ------------------ | ----------------------------------- |
| `Header` | Title and controls | Title, custom content, close button |
| `Body`   | Main content area  | Scrollable, custom content          |
| `Footer` | Action buttons     | Primary/secondary buttons           |

```tsx
// All sections enabled (default)
<Popover
  hasHeader={true}
  hasFooter={true}
  title="Complete Popover"
  trigger={<Button>Open</Button>}
  bodySlotContent="Main content goes here"
/>

// Header only
<Popover
  hasHeader={true}
  hasFooter={false}
  title="Header Only"
  trigger={<Button>Open</Button>}
  bodySlotContent="Content without footer"
/>
```

---

## 4. Scrollable content

```tsx
// Enable scrolling for long content
<Popover
  title="Scrollable Content"
  scrollable={true}
  trigger={<Button>Open</Button>}
  bodySlotContent={<div style={{ height: "800px" }}>Long content that will scroll...</div>}
/>
```

---

## 5. Actions and buttons

```tsx
// Both primary and secondary actions
<Popover
  title="Action Popover"
  trigger={<Button>Open</Button>}
  bodySlotContent="Choose an action"
  hasSecondaryButton={true}
  primaryButtonLabel="Save"
  secondaryButtonLabel="Cancel"
  onPrimaryButtonClick={() => handleSave()}
  onSecondaryButtonClick={() => handleCancel()}
/>

// Primary action only
<Popover
  title="Single Action"
  trigger={<Button>Open</Button>}
  bodySlotContent="Click to confirm"
  hasSecondaryButton={false}
  primaryButtonLabel="OK"
  onPrimaryButtonClick={() => handleOK()}
/>

// Custom button states
<Popover
  title="Custom States"
  trigger={<Button>Open</Button>}
  bodySlotContent="Form content"
  primaryButtonLabel="Submit"
  primaryButtonDisabled={!isFormValid}
  primaryButtonIcon={<SaveIcon />}
/>
```

---

## 6. Header customization

```tsx
// Custom header content
<Popover
  title="Custom Header"
  hasHeaderSlot={true}
  headerSlotContent={<Badge>New</Badge>}
  trigger={<Button>Open</Button>}
  bodySlotContent="Content with custom header"
/>

// Hide close button
<Popover
  title="No Close Button"
  showCloseIcon={false}
  trigger={<Button>Open</Button>}
  bodySlotContent="Cannot be closed with X"
/>
```

---

## 7. Intermediate states

```tsx
// Show intermediate state during processing
<Popover
  title="Processing"
  trigger={<Button>Open</Button>}
  bodySlotContent="Click submit to see intermediate state"
  primaryButtonLabel="Submit"
  intermediateState={
    <div className="text-center py-4">
      <Spinner />
      <p>Processing your request...</p>
    </div>
  }
  onIntermediateStateComplete={() => {
    // Called after 2 seconds
    console.log("Processing complete");
  }}
/>
```

---

## 8. Full prop reference

### Basic Props

| Prop           | Type                      | Default   | Description                   |
| -------------- | ------------------------- | --------- | ----------------------------- |
| `title`        | `string`                  | `"Title"` | Popover title text            |
| `open`         | `boolean`                 | `false`   | Controlled open state         |
| `onOpenChange` | `(open: boolean) => void` | -         | Open state change handler     |
| `trigger`      | `ReactNode`               | -         | Element that triggers popover |
| `size`         | `'small' \| 'large'`      | `'small'` | Popover size                  |

### Content Props

| Prop                | Type        | Default | Description                     |
| ------------------- | ----------- | ------- | ------------------------------- |
| `children`          | `ReactNode` | -       | Main body content               |
| `bodySlotContent`   | `ReactNode` | -       | Alternative body content        |
| `headerSlotContent` | `ReactNode` | -       | Custom header content           |
| `intermediateState` | `ReactNode` | -       | Content shown during processing |

### Layout Props

| Prop            | Type      | Default | Description                  |
| --------------- | --------- | ------- | ---------------------------- |
| `hasHeader`     | `boolean` | `true`  | Show header section          |
| `hasFooter`     | `boolean` | `true`  | Show footer section          |
| `scrollable`    | `boolean` | `false` | Enable body scrolling        |
| `showCloseIcon` | `boolean` | `true`  | Show close button in header  |
| `hasHeaderSlot` | `boolean` | `true`  | Enable custom header content |

### Button Props

| Prop                    | Type        | Default     | Description            |
| ----------------------- | ----------- | ----------- | ---------------------- |
| `hasSecondaryButton`    | `boolean`   | `true`      | Show secondary button  |
| `primaryButtonLabel`    | `ReactNode` | `"Confirm"` | Primary button text    |
| `secondaryButtonLabel`  | `string`    | `"Cancel"`  | Secondary button text  |
| `primaryButtonIcon`     | `ReactNode` | -           | Primary button icon    |
| `secondaryButtonIcon`   | `ReactNode` | -           | Secondary button icon  |
| `primaryButtonDisabled` | `boolean`   | `false`     | Disable primary button |

### Event Handlers

| Prop                          | Type         | Description                    |
| ----------------------------- | ------------ | ------------------------------ |
| `onPrimaryButtonClick`        | `() => void` | Primary button click handler   |
| `onSecondaryButtonClick`      | `() => void` | Secondary button click handler |
| `onCloseButtonClick`          | `() => void` | Close button click handler     |
| `onIntermediateStateComplete` | `() => void` | Intermediate state completion  |

### Styling Props

| Prop                   | Type     | Description                 |
| ---------------------- | -------- | --------------------------- |
| `className`            | `string` | Container CSS classes       |
| `contentClassName`     | `string` | Content area CSS classes    |
| `buttonColor`          | `string` | Primary button background   |
| `secondaryButtonColor` | `string` | Secondary button background |
| `footerColor`          | `string` | Footer background color     |

### Advanced Props

| Prop                     | Type                                   | Description                  |
| ------------------------ | -------------------------------------- | ---------------------------- |
| `stopContentPropagation` | `boolean`                              | Stop click event propagation |
| `bodyProps`              | `React.HTMLAttributes<HTMLDivElement>` | Body section props           |
| `contentProps`           | `React.HTMLAttributes<HTMLDivElement>` | Content container props      |
| `headerProps`            | `React.HTMLAttributes<HTMLDivElement>` | Header section props         |
| `footerProps`            | `React.HTMLAttributes<HTMLDivElement>` | Footer section props         |

---

## 9. Recipes

### Confirmation dialog

```tsx
<Popover
  title="Delete Item"
  trigger={<Button appearance="negative">Delete</Button>}
  bodySlotContent="Are you sure you want to delete this item? This action cannot be undone."
  primaryButtonLabel="Delete"
  secondaryButtonLabel="Cancel"
  buttonColor="#dc2626"
  onPrimaryButtonClick={() => handleDelete()}
/>
```

### Form popover

```tsx
<Popover
  title="Add New Item"
  size="large"
  trigger={<Button>Add Item</Button>}
  bodySlotContent={
    <form className="space-y-4">
      <Input label="Name" placeholder="Enter name" />
      <Input label="Email" placeholder="Enter email" type="email" />
      <Textarea label="Description" placeholder="Enter description" />
    </form>
  }
  primaryButtonLabel="Add Item"
  primaryButtonIcon={<PlusIcon />}
  primaryButtonDisabled={!isFormValid}
  onPrimaryButtonClick={() => handleSubmit()}
/>
```

### Information popover

```tsx
<Popover
  title="Help Information"
  trigger={<IconButton icon={<HelpIcon />} />}
  hasFooter={false}
  bodySlotContent={
    <div className="prose prose-sm">
      <p>This feature helps you manage your account settings.</p>
      <ul>
        <li>Update your profile</li>
        <li>Change preferences</li>
        <li>Manage notifications</li>
      </ul>
    </div>
  }
/>
```

### Processing popover with intermediate state

```tsx
<Popover
  title="Upload File"
  trigger={<Button>Upload</Button>}
  bodySlotContent={
    <div>
      <p>Select a file to upload</p>
      <FileInput onChange={setSelectedFile} />
    </div>
  }
  primaryButtonLabel="Upload"
  intermediateState={
    <div className="text-center py-8">
      <Spinner size="lg" />
      <p className="mt-4">Uploading file...</p>
    </div>
  }
  onPrimaryButtonClick={() => startUpload()}
  onIntermediateStateComplete={() => {
    notify({ title: "Upload complete!", variant: "success" });
  }}
/>
```

### Custom styled popover

```tsx
<Popover
  title="Custom Popover"
  trigger={<Button>Custom Style</Button>}
  className="border-2 border-purple-200"
  contentClassName="bg-gradient-to-br from-purple-50 to-pink-50"
  footerColor="#f3e8ff"
  buttonColor="#8b5cf6"
  bodySlotContent="This popover has custom styling"
/>
```

---

## 10. Accessibility

The Popover component includes comprehensive accessibility features:

- Proper ARIA attributes and roles
- Keyboard navigation support (Escape to close)
- Focus management and trapping
- Screen reader announcements
- Accessible button states

```tsx
<Popover
  title="Accessible Popover"
  trigger={<Button aria-describedby="popover-help">Open</Button>}
  bodySlotContent="This popover is fully accessible"
  aria-label="Help dialog"
  role="dialog"
/>
```

---

## 11. Design Tokens

The Popover component uses the following design system tokens:

**Layout:**

- Width: `364px` (both sizes)
- Border radius: `16px`
- Shadow: `shadow-gd-shadow-m`
- Z-index: `100`

**Header:**

- Small height: `40px`
- Large height: `56px`
- Background: `bg-color-background-surface-20`

**Body:**

- Small padding: `12px 16px`
- Large padding: `16px`
- Max height (scrollable): `656px`

**Footer:**

- Small padding: `8px 12px`
- Large padding: `12px 16px`

**Typography:**

- Title: `text-en-desktop-heading-xl font-600`

**Colors:**

- Background: `bg-color-neutral-white`
- Border: `border-0`

---

Consider using Popover with:

- **Button** — For trigger elements
- **IconButton** — For close actions
- **Form** — For input popovers
- **Tooltip** — For simple information
- **Modal** — For complex dialogs
