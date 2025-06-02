# FormNavigation

A navigation component that provides synchronized scrolling between a sidebar navigation menu and form sections, with automatic active state management based on viewport intersection.

---

## 1. Quick start

```tsx
import { FormNavigation } from "gends";

function Example() {
  const sections = ["Personal Info", "Contact Details", "Preferences"];

  return (
    <FormNavigation navTitles={sections} viewThreshold={0.5}>
      <PersonalInfoSection />
      <ContactDetailsSection />
      <PreferencesSection />
    </FormNavigation>
  );
}
```

---

## 2. Navigation behavior

The FormNavigation component provides intelligent scroll synchronization:

| behavior          | Description                       | Trigger                 |
| ----------------- | --------------------------------- | ----------------------- |
| Auto-detection    | Active section updates on scroll  | Viewport intersection   |
| Manual navigation | Click to jump to section          | Navigation item click   |
| Smooth scrolling  | Animated scroll transitions       | Programmatic navigation |
| Threshold-based   | Configurable visibility threshold | `viewThreshold` prop    |

```tsx
// Basic navigation with default threshold
<FormNavigation navTitles={["Section 1", "Section 2", "Section 3"]}>
  <div>Section 1 Content</div>
  <div>Section 2 Content</div>
  <div>Section 3 Content</div>
</FormNavigation>

// Custom visibility threshold
<FormNavigation navTitles={sections} viewThreshold={0.8}>
  {sectionComponents}
</FormNavigation>
```

---

## 3. Layout structure

The component provides a fixed sidebar navigation with scrollable content:

| area      | Properties                      | Description                |
| --------- | ------------------------------- | -------------------------- |
| Container | 1136px width, centered, gap-24  | Main layout wrapper        |
| Sidebar   | 298px width, sticky positioning | Navigation menu (fixed)    |
| Content   | Flexible width, scrollable      | Form sections (scrollable) |

```tsx
// Standard layout
<FormNavigation navTitles={navTitles}>
  <FormSection1 />
  <FormSection2 />
  <FormSection3 />
</FormNavigation>
```

---

## 4. Navigation states

| state      | Description                 | Visual treatment            |
| ---------- | --------------------------- | --------------------------- |
| `active`   | Currently visible section   | Blue background, bold text  |
| `inactive` | Non-active navigation items | Default text, no background |

```tsx
// Active state styling automatically applied based on scroll position
<FormNavigation navTitles={["Overview", "Details", "Summary"]}>
  {/* Active section gets bg-color-primary-20 automatically */}
  <OverviewSection />
  <DetailsSection />
  <SummarySection />
</FormNavigation>
```

---

## 5. Scroll configuration

```tsx
// Custom threshold for section activation
<FormNavigation
  navTitles={sections}
  viewThreshold={0.3} // Section becomes active when 30% visible
>
  {sectionComponents}
</FormNavigation>

// Multiple sections with different content heights
<FormNavigation navTitles={["Short Section", "Long Form", "Quick Summary"]}>
  <div className="h-64">Short content</div>
  <div className="h-screen">Long form with many fields</div>
  <div className="h-32">Brief summary</div>
</FormNavigation>
```

---

## 6. Advanced features

The component includes intersection observer optimization and smooth transitions:

```tsx
// Debounced scroll handling for performance
<FormNavigation navTitles={navTitles} viewThreshold={0.5}>
  {/* Automatic debouncing and smooth transitions */}
  <ComplexFormSection />
  <AnotherFormSection />
</FormNavigation>;

// Manual scroll control (internal implementation)
const handleSectionClick = index => {
  // Smooth scroll to section with temporary observer disable
  contentRefs.current[index].scrollIntoView({
    behavior: "smooth",
    block: "start",
  });
};
```

---

## 7. Full prop reference

### Basic Props

| Prop            | Type          | Description                         |
| --------------- | ------------- | ----------------------------------- |
| `navTitles`     | `string[]`    | Array of navigation section titles  |
| `children`      | `ReactNode[]` | Array of section components         |
| `viewThreshold` | `number`      | Intersection threshold (0.0 to 1.0) |

### Navigation Titles

| Property    | Type     | Description                        |
| ----------- | -------- | ---------------------------------- |
| Array items | `string` | Section titles for navigation menu |

### Children Components

| Property    | Type        | Description                         |
| ----------- | ----------- | ----------------------------------- |
| Array items | `ReactNode` | Content components for each section |

### Threshold Configuration

| Value range | Description                          |
| ----------- | ------------------------------------ |
| `0.0`       | Section active when any part visible |
| `0.5`       | Section active when 50% visible      |
| `1.0`       | Section active when fully visible    |

---

## 8. Recipes

### Basic form navigation

```tsx
const formSections = [
  "Personal Information",
  "Address Details",
  "Contact Information",
  "Preferences",
];

<FormNavigation navTitles={formSections} viewThreshold={0.5}>
  <PersonalInfoForm />
  <AddressForm />
  <ContactForm />
  <PreferencesForm />
</FormNavigation>;
```

### Multi-step wizard navigation

```tsx
const wizardSteps = ["Account Setup", "Company Details", "Billing Information", "Review & Submit"];

<FormNavigation navTitles={wizardSteps} viewThreshold={0.6}>
  <AccountSetupStep />
  <CompanyDetailsStep />
  <BillingStep />
  <ReviewStep />
</FormNavigation>;
```

### Settings page navigation

```tsx
const settingsCategories = [
  "General Settings",
  "Security & Privacy",
  "Notifications",
  "Integrations",
  "Advanced Options",
];

<FormNavigation navTitles={settingsCategories} viewThreshold={0.4}>
  <GeneralSettings />
  <SecuritySettings />
  <NotificationSettings />
  <IntegrationsSettings />
  <AdvancedSettings />
</FormNavigation>;
```

### Documentation navigation

```tsx
const docSections = [
  "Getting Started",
  "API Reference",
  "Examples",
  "Best Practices",
  "Troubleshooting",
];

<FormNavigation navTitles={docSections} viewThreshold={0.3}>
  <GettingStartedDocs />
  <ApiReferenceDocs />
  <ExamplesDocs />
  <BestPracticesDocs />
  <TroubleshootingDocs />
</FormNavigation>;
```

### Variable content heights

```tsx
const mixedSections = [
  "Quick Overview", // Short section
  "Detailed Configuration", // Long section
  "Final Steps", // Medium section
];

<FormNavigation navTitles={mixedSections} viewThreshold={0.5}>
  <div className="h-48 p-4">Brief overview content</div>
  <div className="min-h-screen p-4">
    {/* Long form with many fields */}
    <DetailedConfigurationForm />
  </div>
  <div className="h-96 p-4">Final steps content</div>
</FormNavigation>;
```

### Custom styled navigation

```tsx
<div className="custom-navigation-wrapper">
  <FormNavigation navTitles={sections} viewThreshold={0.5}>
    <div className="bg-white rounded-lg shadow p-6">
      <SectionOne />
    </div>
    <div className="bg-gray-50 rounded-lg shadow p-6">
      <SectionTwo />
    </div>
    <div className="bg-blue-50 rounded-lg shadow p-6">
      <SectionThree />
    </div>
  </FormNavigation>
</div>
```

---

## 9. Accessibility

The FormNavigation component includes accessibility features:

- Semantic navigation structure with anchor elements
- Keyboard navigation support for menu items
- Focus management during scroll interactions
- Screen reader friendly section identification

```tsx
<FormNavigation navTitles={["Accessible Section 1", "Accessible Section 2"]} viewThreshold={0.5}>
  <section aria-labelledby="section-1-title">
    <h2 id="section-1-title">Accessible Section 1</h2>
    {/* Section content */}
  </section>
  <section aria-labelledby="section-2-title">
    <h2 id="section-2-title">Accessible Section 2</h2>
    {/* Section content */}
  </section>
</FormNavigation>
```

---

## 10. Design Tokens

The FormNavigation component uses the following design system tokens:

**Layout:**

- Container width: `1136px`
- Container spacing: `gap-gd-24` (24px gap)
- Sidebar width: `298px`
- Content height: `90vh` with `overflow-y-auto`

**Sidebar Styling:**

- Background: `bg-white`
- Border: `border border-solid border-gray-300`
- Border radius: `rounded-gd-16`
- Position: `sticky top-6 left-0`
- Height: `fit-content`

**Navigation Items:**

- Margin: `m-gd-16`
- Padding: `py-[10px] px-gd-12`
- Gap: `gap-gd-12`
- Border radius: `rounded-gd-8`

**Active State:**

- Background: `bg-color-primary-20`
- Text: `text-en-desktop-body-m-prominent text-color-neutral-grey-100`

**Inactive State:**

- Text: `text-en-desktop-body-m text-color-text-subdued-1`

**Spacing:**

- Section gap: `gap-gd-24` (24px between sections)
- Navigation item spacing: `gd-12` (12px internal spacing)

---

Consider using FormNavigation with:

- **Form** — For multi-section forms
- **Settings** — For configuration pages
- **Documentation** — For long-form content
- **Wizard** — For step-by-step processes
- **Survey** — For multi-page questionnaires
