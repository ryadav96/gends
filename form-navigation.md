# Form Navigation Component

## Overview

The Form Navigation component is a sophisticated and accessible form navigation system built with Genesis Design System tokens. It provides a sticky sidebar navigation with smooth scrolling between form sections, automatic section tracking, and comprehensive keyboard navigation. The component is designed for multi-step forms, long-form content, and complex data entry scenarios with complete accessibility support.

## Component API

### FormNav Props

| Prop          | Type                | Default  | Description                                        |
| ------------- | ------------------- | -------- | -------------------------------------------------- |
| navTitles     | `string[]`          | Required | Array of navigation titles for each section        |
| children      | `React.ReactNode[]` | Required | Array of form sections/content to be displayed     |
| viewThreshold | `number`            | `0.5`    | Intersection threshold for section detection (0-1) |

### Import Statement

```typescript
import { FormNav } from "gends";
```

## Basic Usage

### Multi-Step Form

The default implementation with three form sections and navigation.

```tsx
<FormNav navTitles={["Personal Information", "Contact Details", "Additional Information"]}>
  {[
    // Section 1: Personal Information
    <div key="personal" className="cards">
      <Card title="Personal Information">
        <Input label="Full Name" placeholder="Enter your full name" required />
        <div className="grid grid-cols-2 gap-4">
          <Input label="Date of Birth" type="date" />
          <Input label="Gender" placeholder="Select gender" />
        </div>
        <TextArea label="Brief Bio" placeholder="Tell us about yourself..." rows={4} />
        <div className="flex justify-end mt-4">
          <Button>Next</Button>
        </div>
      </Card>
    </div>,

    // Section 2: Contact Details
    <div key="contact" className="cards">
      <Card title="Contact Details">
        <Input label="Email Address" placeholder="Enter your email" type="email" required />
        <Input label="Phone Number" placeholder="Enter your phone number" />
        <div className="grid grid-cols-2 gap-4">
          <Input label="Country" placeholder="Select country" />
          <Input label="City" placeholder="Enter city" />
        </div>
        <Input label="Address" placeholder="Enter your address" />
        <div className="flex justify-between mt-4">
          <Button kind="secondary">Previous</Button>
          <Button>Next</Button>
        </div>
      </Card>
    </div>,

    // Section 3: Additional Information
    <div key="additional" className="cards">
      <Card title="Additional Information">
        <Input label="Occupation" placeholder="Enter your occupation" />
        <Input label="Company" placeholder="Enter company name" />
        <div className="grid grid-cols-2 gap-4">
          <Input label="Years of Experience" type="number" min={0} />
          <Input label="Skills" placeholder="Enter your skills" />
        </div>
        <TextArea label="Additional Notes" placeholder="Any additional information..." rows={4} />
        <div className="flex justify-between mt-4">
          <Button kind="secondary">Previous</Button>
          <Button kind="primary">Submit</Button>
        </div>
      </Card>
    </div>,
  ]}
</FormNav>
```

## Advanced Features

### Form Validation Integration

Integration with form validation and state management.

```tsx
const FormWithValidation = () => {
  const [formData, setFormData] = React.useState({
    name: "",
    email: "",
    message: "",
  });

  const handleChange = (field: string, value: string) => {
    setFormData(prev => ({ ...prev, [field]: value }));
  };

  return (
    <FormNav navTitles={["Basic Details", "Contact Info", "Review & Submit"]}>
      {[
        // Section 1: Basic Details
        <div key="basic" className="cards">
          <Card title="Basic Details">
            <Input
              label="Full Name"
              placeholder="Enter your full name"
              required
              value={formData.name}
              onValueChange={val => handleChange("name", val.toString())}
              validationState={formData.name ? "success" : "error"}
              validationMessage={formData.name ? "Looks good!" : "Name is required"}
            />
            <div className="flex justify-end mt-4">
              <Button>Continue</Button>
            </div>
          </Card>
        </div>,

        // Section 2: Contact Info
        <div key="contact" className="cards">
          <Card title="Contact Information">
            <Input
              label="Email Address"
              type="email"
              placeholder="Enter your email"
              required
              value={formData.email}
              onValueChange={val => handleChange("email", val.toString())}
              validationState={formData.email.includes("@") ? "success" : "error"}
              validationMessage={
                formData.email.includes("@") ? "Valid email" : "Please enter a valid email"
              }
            />
            <div className="flex justify-between mt-4">
              <Button kind="secondary">Back</Button>
              <Button>Continue</Button>
            </div>
          </Card>
        </div>,
      ]}
    </FormNav>
  );
};
```

### Custom Section Tracking

Adjusting the intersection threshold for section detection.

```tsx
<FormNav
  navTitles={["Section 1", "Section 2", "Section 3"]}
  viewThreshold={0.75} // More strict section detection
>
  {sections}
</FormNav>
```

## Real-World Usage Examples

### Registration Form

```tsx
const RegistrationForm = () => {
  return (
    <FormNav navTitles={["Account Setup", "Personal Details", "Preferences", "Confirmation"]}>
      {[
        // Account Setup Section
        <div key="account" className="cards">
          <Card title="Create Your Account">
            <Input label="Username" placeholder="Choose a username" required />
            <Input label="Password" type="password" placeholder="Create a password" required />
            <Input
              label="Confirm Password"
              type="password"
              placeholder="Confirm your password"
              required
            />
            <div className="flex justify-end mt-4">
              <Button>Next</Button>
            </div>
          </Card>
        </div>,

        // Personal Details Section
        <div key="personal" className="cards">
          <Card title="Your Information">
            <Input label="Full Name" placeholder="Enter your full name" required />
            <Input label="Date of Birth" type="date" required />
            <div className="grid grid-cols-2 gap-4">
              <Input label="Country" placeholder="Select your country" required />
              <Input label="Phone Number" placeholder="Enter your phone number" />
            </div>
            <div className="flex justify-between mt-4">
              <Button kind="secondary">Back</Button>
              <Button>Next</Button>
            </div>
          </Card>
        </div>,
      ]}
    </FormNav>
  );
};
```

### Settings Configuration

```tsx
const SettingsForm = () => {
  return (
    <FormNav
      navTitles={[
        "General Settings",
        "Notification Preferences",
        "Privacy Settings",
        "Advanced Options",
      ]}
    >
      {[
        // General Settings Section
        <div key="general" className="cards">
          <Card title="General Settings">
            <Input label="Display Name" placeholder="Enter display name" />
            <Input label="Language" placeholder="Select language" />
            <Input label="Time Zone" placeholder="Select time zone" />
            <div className="flex justify-end mt-4">
              <Button>Save Changes</Button>
            </div>
          </Card>
        </div>,

        // Notification Preferences Section
        <div key="notifications" className="cards">
          <Card title="Notification Settings">
            <div className="space-y-4">
              <Toggle label="Email Notifications" description="Receive email updates" />
              <Toggle label="Push Notifications" description="Receive push notifications" />
              <Toggle label="SMS Notifications" description="Receive SMS updates" />
            </div>
            <div className="flex justify-end mt-4">
              <Button>Save Preferences</Button>
            </div>
          </Card>
        </div>,
      ]}
    </FormNav>
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab Navigation**: Focus management through navigation items and form fields
- **Arrow Keys**: Navigate between sections
- **Enter/Space**: Activate focused navigation item
- **Focus Management**: Maintains focus within active section

### Screen Reader Support

- **ARIA Attributes**: Proper roles and states for navigation and sections
- **Live Regions**: Announcements for section changes
- **Focus Management**: Maintains focus within active section

### Visual Accessibility

- **Focus Indicators**: Clear focus states for all interactive elements
- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Text Scaling**: Supports text size adjustments

## Design System Integration

### Genesis Design Tokens

**Colors:**

- `var(--gd-primary-20)`: Active navigation background
- `var(--gd-neutral-grey-100)`: Active navigation text
- `var(--gd-text-subdued-1)`: Inactive navigation text

**Spacing:**

- `gd-12`: Standard padding and gaps
- `gd-16`: Navigation item padding
- `gd-24`: Section spacing

**Typography:**

- `text-en-desktop-body-m`: Navigation text
- `text-en-desktop-body-m-prominent`: Active navigation text

**Border Radius:**

- `rounded-gd-8`: Navigation items
- `rounded-gd-16`: Navigation container

## Best Practices

### Performance

- Use proper form state management
- Implement efficient section tracking
- Optimize re-renders with proper state management

### User Experience

- Provide clear section titles
- Implement proper form validation
- Use appropriate button labels
- Consider mobile responsiveness

### Integration

- Handle form state properly
- Implement proper validation
- Consider mobile responsiveness
- Test with screen readers

## Troubleshooting

### Common Issues

**Section Tracking Issues:**

- Adjust viewThreshold value
- Check section heights
- Verify intersection observer setup

**Navigation Problems:**

- Verify section IDs
- Check scroll behavior
- Ensure proper section structure

**Form State Issues:**

- Implement proper state management
- Handle form validation correctly
- Manage section transitions

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test keyboard navigation
- Verify accessibility features

Remember: The Form Navigation component provides a flexible and accessible way to implement multi-step forms and complex navigation. Choose the appropriate configuration based on your specific use case and requirements.
