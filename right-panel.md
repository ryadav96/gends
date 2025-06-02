# RightPanel

A flexible right-side panel component that supports multiple sizes, customizable headers and footers, extension behavior, and comprehensive content management.

---

## 1. Quick start

```tsx
import { RightPanel } from "gends";

function Example() {
  return (
    <RightPanel
      title="Page Label"
      width="s"
      showFooter={true}
      showPrimaryBtn={true}
      showSecondaryBtn={true}
    >
      Content goes here
    </RightPanel>
  );
}
```

---

## 2. Sizes

| size | Width | Description       | Use case               |
| ---- | ----- | ----------------- | ---------------------- |
| `xs` | 362px | Extra small panel | Quick views            |
| `s`  | 475px | Small panel       | Simple forms           |
| `m`  | 700px | Medium panel      | Standard content       |
| `l`  | 925px | Large panel       | Complex forms          |
| `f`  | 100%  | Full width        | Full-screen experience |

```tsx
<RightPanel width="xs" title="Quick View" />
<RightPanel width="s" title="Simple Form" />
<RightPanel width="m" title="Standard Content" />
<RightPanel width="l" title="Complex Form" />
<RightPanel width="f" title="Full Experience" />
```

---

## 3. Header configurations

| header feature | Description             | Use case               |
| -------------- | ----------------------- | ---------------------- |
| Title          | Main panel title        | Basic identification   |
| Subtitle       | Supporting description  | Additional context     |
| Tag            | Feature tag             | Feature identification |
| Back button    | Navigation control      | Multi-step workflows   |
| Extension      | Expand/collapse control | Resizable panels       |

```tsx
// Basic header with title
<RightPanel title="Basic Header" />

// Header with subtitle
<RightPanel
  title="Main Title"
  subTitle="Supporting description"
  showSubTitle={true}
/>

// Header with tag
<RightPanel
  title="Feature Panel"
  tagText="Beta"
  showTag={true}
/>

// Header with back button
<RightPanel
  title="Step 2"
  showBack={true}
  backAction={() => handleBack()}
/>

// Extensible header
<RightPanel
  title="Resizable Panel"
  extension={true}
  maxWidth="l"
/>
```

---

## 4. Footer configurations

| footer feature   | Description        | Use case          |
| ---------------- | ------------------ | ----------------- |
| Primary button   | Main action button | Primary actions   |
| Secondary button | Alternative action | Secondary actions |
| No footer        | Content-only panel | View-only content |

```tsx
// Default footer with both buttons
<RightPanel
  showFooter={true}
  showPrimaryBtn={true}
  showSecondaryBtn={true}
  primaryAction={() => handlePrimary()}
  secondaryAction={() => handleSecondary()}
/>

// Primary button only
<RightPanel
  showFooter={true}
  showPrimaryBtn={true}
  showSecondaryBtn={false}
/>

// No footer
<RightPanel showFooter={false}>
  Content only
</RightPanel>
```

---

## 5. Trigger options

```tsx
// Default trigger button
<RightPanel title="With Default Trigger">
  Content
</RightPanel>

// Custom trigger
<RightPanel
  trigger={<Button>Custom Open</Button>}
  title="Custom Trigger Panel"
>
  Content
</RightPanel>

// No trigger (controlled externally)
<RightPanel
  noTriggerBtn={true}
  open={isOpen}
  setOpen={setOpen}
  title="Controlled Panel"
>
  Content
</RightPanel>
```

---

## 6. Extension behavior

```tsx
// Resizable panel
<RightPanel
  extension={true}
  width="s"
  maxWidth="l"
  title="Resizable Panel"
>
  Content that can be viewed in expanded mode
</RightPanel>

// Fixed width panel
<RightPanel
  extension={false}
  width="m"
  title="Fixed Width Panel"
>
  Content with fixed width
</RightPanel>
```

---

## 7. Full prop reference

### Basic Props

| Prop        | Type                               | Default        | Description             |
| ----------- | ---------------------------------- | -------------- | ----------------------- |
| `title`     | `string`                           | `"Page Label"` | Panel title             |
| `width`     | `'xs' \| 's' \| 'm' \| 'l' \| 'f'` | `'s'`          | Panel width variant     |
| `maxWidth`  | `'xs' \| 's' \| 'm' \| 'l' \| 'f'` | `'l'`          | Maximum extension width |
| `extension` | `boolean`                          | `false`        | Enable width extension  |
| `children`  | `ReactNode`                        | -              | Panel content           |

### Header Props

| Prop           | Type      | Default         | Description      |
| -------------- | --------- | --------------- | ---------------- |
| `subTitle`     | `string`  | `"description"` | Subtitle text    |
| `tagText`      | `string`  | `"tag"`         | Feature tag text |
| `showTag`      | `boolean` | `false`         | Show feature tag |
| `showSubTitle` | `boolean` | `false`         | Show subtitle    |
| `showBack`     | `boolean` | `false`         | Show back button |

### Footer Props

| Prop               | Type       | Default | Description              |
| ------------------ | ---------- | ------- | ------------------------ |
| `showFooter`       | `boolean`  | `true`  | Show footer section      |
| `showPrimaryBtn`   | `boolean`  | `true`  | Show primary button      |
| `showSecondaryBtn` | `boolean`  | `true`  | Show secondary button    |
| `primaryAction`    | `function` | `noop`  | Primary button handler   |
| `secondaryAction`  | `function` | `noop`  | Secondary button handler |

### Control Props

| Prop           | Type        | Default | Description            |
| -------------- | ----------- | ------- | ---------------------- |
| `noTriggerBtn` | `boolean`   | `false` | Hide default trigger   |
| `trigger`      | `ReactNode` | -       | Custom trigger element |
| `open`         | `boolean`   | -       | Controlled open state  |
| `setOpen`      | `function`  | `noop`  | Open state setter      |
| `backAction`   | `function`  | `noop`  | Back button handler    |

---

## 8. Recipes

### Basic right panel

```tsx
<RightPanel
  title="User Details"
  width="s"
  showFooter={true}
  showPrimaryBtn={true}
  primaryAction={() => handleSave()}
>
  <UserDetailsForm />
</RightPanel>
```

### Multi-step workflow panel

```tsx
<RightPanel
  title="Create Project"
  width="m"
  showBack={currentStep > 1}
  backAction={() => setCurrentStep(prev => prev - 1)}
  showFooter={true}
  showPrimaryBtn={true}
  showSecondaryBtn={true}
  primaryAction={() => handleNextStep()}
  secondaryAction={() => handleCancel()}
>
  <StepContent step={currentStep} />
</RightPanel>
```

### Feature preview panel

```tsx
<RightPanel
  title="New Feature"
  tagText="Beta"
  showTag={true}
  width="s"
  extension={true}
  maxWidth="l"
  showFooter={true}
  showPrimaryBtn={true}
  primaryAction={() => handleTryFeature()}
>
  <FeaturePreview />
</RightPanel>
```

### View-only panel

```tsx
<RightPanel
  title="Documentation"
  width="m"
  showFooter={false}
  trigger={<Button kind="secondary">View Docs</Button>}
>
  <DocumentationContent />
</RightPanel>
```

### Controlled panel with external trigger

```tsx
const [isOpen, setIsOpen] = useState(false);

<Button onClick={() => setIsOpen(true)}>
  Open Details
</Button>

<RightPanel
  noTriggerBtn={true}
  open={isOpen}
  setOpen={setIsOpen}
  title="Details View"
  width="s"
>
  <DetailsContent />
</RightPanel>
```

---

## 9. Accessibility

The RightPanel component includes accessibility features:

- Focus trap within panel content
- Keyboard navigation support (Escape to close)
- Proper ARIA attributes and roles
- Focus restoration on close
- Screen reader announcements

```tsx
<RightPanel title="Accessible Panel" role="dialog" aria-labelledby="panel-title">
  <AccessibleContent />
</RightPanel>
```

---

## 10. Design Tokens

The RightPanel component uses the following design system tokens:

**Sizing:**

- XSmall: `sm:max-w-[362px]`
- Small: `sm:max-w-[475px]`
- Medium: `sm:max-w-[700px]`
- Large: `sm:max-w-[925px]`
- Full: `sm:max-w-[100vw]`

**Spacing:**

- Header padding: `p-gd-16`
- Content background: `bg-color-background-surface-10`
- Footer padding: `p-gd-16`
- Gap: `gap-gd-4`, `gap-gd-8`, `gap-gd-16`

**Colors:**

- Background: `bg-color-background-surface-0`
- Border: `border-color-neutral-grey-40`
- Text: `text-color-neutral-grey-80`

**Typography:**

- Title: `text-en-desktop-heading-xl`
- Subtitle: `text-en-desktop-body-m`
- Tag: Feature tag styling

**Layout:**

- Border: `border-b-[1px]` (header), `border-t-[1px]` (footer)
- Flex layout with proper spacing
- Sticky header positioning

---

Consider using RightPanel with:

- **Form** — For data entry workflows
- **Details** — For record viewing
- **Settings** — For configuration panels
- **Preview** — For content inspection
- **Documentation** — For contextual help
