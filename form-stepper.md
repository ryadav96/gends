# FormStepper Component Documentation

## Overview

The `FormStepper` component is a specialized stepper interface built with **Gends** (Genesis Design System) and optimized for **MCP (Modular Component Platform)** servers powered by **Contex 7**. This molecule-level component provides a streamlined solution for creating form-specific, multi-step workflows with enhanced accessibility, keyboard navigation, and real-time state management.

As a form-focused molecule component in the Gends design system, FormStepper serves as the foundation for creating intuitive form workflows that guide users through complex data collection processes in MCP server environments.

## Purpose in Gends-MCP-Contex7 Ecosystem

Within the **Gends-MCP-Contex7** ecosystem, the FormStepper component serves as the cornerstone for form workflow management:

### MCP Server Integration

- **Form Process Orchestration**: Handle complex multi-step form workflows with real-time validation
- **Data Collection Visualization**: Create clear visual representation of form progress and completion status
- **User-Guided Workflows**: Enable structured data collection for configuration, onboarding, and user management
- **Form State Synchronization**: Real-time synchronization between form progress and server-side validation states

### Contex 7 Compatibility

- **Enhanced Form Theming**: Full integration with Contex 7's form-specific theming capabilities
- **Performance Optimized**: Leverages Contex 7's optimized rendering for smooth step transitions
- **Form Context Management**: Integrates with Contex 7's form state management for complex validation scenarios
- **Accessibility First**: Exceeds Contex 7's accessibility standards with comprehensive keyboard navigation

## Installation & Import

### Standard Gends Import

```typescript
import { FormStepper } from "gends";
import type { StepConfig, StepperProps } from "gends";
import { IcConfirm } from "gends";
```

### Alternative Import (Local Development)

```typescript
import FormStepper from "@/components/genesis/molecules/form-stepper/form-stepper";
import type {
  StepConfig,
  StepperProps,
} from "@/components/genesis/molecules/form-stepper/form-stepper";
import { IcConfirm } from "@/assets/icon-components";
```

## Component Variants

### 1. **Layout Variants**

#### Horizontal Layout (Default)

- **Use Case**: Wide form containers, multi-step registration, checkout processes
- **Best For**: Desktop interfaces, linear form progression, overview display
- **Features**: Inline step display, optimal for 3-6 steps, responsive spacing

#### Vertical Layout

- **Use Case**: Sidebar forms, narrow containers, detailed step descriptions
- **Best For**: Navigation panels, step-by-step wizards, mobile-first forms
- **Features**: Stacked step display, optimized for scrolling, enhanced readability

### 2. **Step State Variants**

#### Completed State

- **Visual**: Success icon with completion styling and checkmark
- **Purpose**: Successfully finished and validated steps
- **MCP Context**: Validated form sections, successful data submission

#### Active State

- **Visual**: Primary accent styling with emphasized indicators
- **Purpose**: Currently active/focused step in the workflow
- **MCP Context**: Current form section, active data collection phase

#### Upcoming State

- **Visual**: Neutral styling indicating future steps
- **Purpose**: Steps not yet reached in the form flow
- **MCP Context**: Pending form sections, future data collection phases

#### Disabled State

- **Visual**: Muted colors, reduced opacity, non-interactive
- **Purpose**: Unavailable or conditionally locked steps
- **MCP Context**: Conditional form sections, permission-restricted fields

### 3. **Interactive Variants**

#### Clickable Steps

- **Use Case**: Non-linear form navigation, review and edit workflows
- **Behavior**: Allow users to navigate between completed steps
- **Best For**: Review processes, form editing, data verification

#### Read-Only Steps

- **Use Case**: Linear form progression, guided workflows
- **Behavior**: Display progress without allowing backward navigation
- **Best For**: Sequential forms, onboarding flows, data collection

## Props API

### Core Configuration Props

| Prop           | Type                          | Default        | Required | Description                                                      |
| -------------- | ----------------------------- | -------------- | -------- | ---------------------------------------------------------------- |
| `steps`        | `StepConfig[]`                | `[]`           | ✅       | Array of step configurations defining the complete form workflow |
| `layout`       | `"horizontal" \| "vertical"`  | `"horizontal"` | ❌       | Layout orientation of the form stepper component                 |
| `activeIndex`  | `number`                      | `0`            | ✅       | Zero-based index of the currently active step                    |
| `onStepChange` | `(stepIndex: number) => void` | `undefined`    | ✅       | Callback fired when a step is selected or navigation occurs      |

### Content & Customization Props

| Prop                 | Type              | Default     | Required | Description                                           |
| -------------------- | ----------------- | ----------- | -------- | ----------------------------------------------------- |
| `titleHtml`          | `React.ReactNode` | `undefined` | ❌       | Custom JSX content to replace default step titles     |
| `icon`               | `React.ReactNode` | `undefined` | ❌       | Custom icon to replace default step indicators        |
| `containerClassName` | `string`          | `""`        | ❌       | Additional CSS classes for individual step containers |

## Type Definitions

### StepConfig Interface

```typescript
interface StepConfig {
  title: string; // Main step title/label
  completed: boolean; // Whether the step has been completed
  disabled?: boolean; // Whether the step is interactive (optional, defaults to false)
}
```

### StepperProps Interface

```typescript
interface StepperProps {
  steps: StepConfig[]; // Array of step configurations
  layout: "horizontal" | "vertical"; // Layout orientation
  activeIndex: number; // Currently active step index
  onStepChange: (stepIndex: number) => void; // Step selection callback
  titleHtml?: React.ReactNode; // Custom title content
  icon?: React.ReactNode; // Custom step icon
  containerClassName?: string; // Additional container styling
}
```

## Usage Examples

### 1. Basic User Registration Form

```tsx
import { FormStepper } from "gends";
import { useState } from "react";

function UserRegistrationFlow() {
  const [currentStep, setCurrentStep] = useState(0);
  const [formData, setFormData] = useState({
    personal: {},
    account: {},
    verification: {},
  });

  const registrationSteps = [
    {
      title: "Personal Information",
      completed: currentStep > 0,
      disabled: false,
    },
    {
      title: "Account Setup",
      completed: currentStep > 1,
      disabled: currentStep < 1,
    },
    {
      title: "Email Verification",
      completed: currentStep > 2,
      disabled: currentStep < 2,
    },
    {
      title: "Complete Registration",
      completed: false,
      disabled: currentStep < 3,
    },
  ];

  const handleStepChange = (stepIndex: number) => {
    // Only allow navigation to accessible steps
    if (!registrationSteps[stepIndex].disabled) {
      setCurrentStep(stepIndex);
    }
  };

  return (
    <div className="registration-container max-w-4xl mx-auto p-6">
      <h2 className="text-en-desktop-heading-2xl mb-6">Create Your Account</h2>

      <FormStepper
        steps={registrationSteps}
        layout="horizontal"
        activeIndex={currentStep}
        onStepChange={handleStepChange}
        containerClassName="mb-8"
      />

      <div className="form-content bg-background-surface-10 p-6 rounded-gd-12">
        {currentStep === 0 && <PersonalInformationForm data={formData.personal} />}
        {currentStep === 1 && <AccountSetupForm data={formData.account} />}
        {currentStep === 2 && <EmailVerificationForm />}
        {currentStep === 3 && <RegistrationComplete />}
      </div>
    </div>
  );
}
```

### 2. Vertical Checkout Process

```tsx
import { FormStepper } from "gends";
import { useState, useEffect } from "react";

function CheckoutProcess() {
  const [activeStep, setActiveStep] = useState(0);
  const [completedSteps, setCompletedSteps] = useState(new Set<number>());

  const checkoutSteps = [
    {
      title: "Shopping Cart",
      completed: completedSteps.has(0),
      disabled: false,
    },
    {
      title: "Shipping Information",
      completed: completedSteps.has(1),
      disabled: false,
    },
    {
      title: "Payment Details",
      completed: completedSteps.has(2),
      disabled: !completedSteps.has(1),
    },
    {
      title: "Order Review",
      completed: completedSteps.has(3),
      disabled: !completedSteps.has(2),
    },
  ];

  const markStepCompleted = (stepIndex: number) => {
    setCompletedSteps(prev => new Set([...prev, stepIndex]));
    if (stepIndex < checkoutSteps.length - 1) {
      setActiveStep(stepIndex + 1);
    }
  };

  return (
    <div className="checkout-container flex gap-gd-24 max-w-6xl mx-auto p-6">
      {/* Vertical stepper sidebar */}
      <div className="stepper-sidebar w-64 flex-shrink-0">
        <h3 className="text-en-desktop-heading-xl mb-6">Checkout Progress</h3>
        <FormStepper
          steps={checkoutSteps}
          layout="vertical"
          activeIndex={activeStep}
          onStepChange={setActiveStep}
        />
      </div>

      {/* Main checkout content */}
      <div className="checkout-content flex-1 bg-background-surface-10 p-6 rounded-gd-12">
        <CheckoutStepContent
          step={activeStep}
          onStepComplete={() => markStepCompleted(activeStep)}
        />
      </div>
    </div>
  );
}
```

### 3. MCP Server Configuration Wizard

```tsx
import { FormStepper } from "gends";
import { useState } from "react";

function ServerConfigurationWizard() {
  const [configStep, setConfigStep] = useState(0);
  const [configData, setConfigData] = useState({
    environment: null,
    database: null,
    services: null,
    security: null,
  });

  const configSteps = [
    {
      title: "Environment Setup",
      completed: !!configData.environment,
      disabled: false,
    },
    {
      title: "Database Configuration",
      completed: !!configData.database,
      disabled: !configData.environment,
    },
    {
      title: "Service Integration",
      completed: !!configData.services,
      disabled: !configData.database,
    },
    {
      title: "Security Settings",
      completed: !!configData.security,
      disabled: !configData.services,
    },
  ];

  const updateConfigData = (section: string, data: any) => {
    setConfigData(prev => ({
      ...prev,
      [section]: data,
    }));
  };

  return (
    <div className="config-wizard max-w-5xl mx-auto p-6">
      <div className="wizard-header mb-8">
        <h2 className="text-en-desktop-heading-2xl mb-2">MCP Server Configuration</h2>
        <p className="text-en-desktop-body-l text-text-subdued-1">
          Configure your Contex 7 server environment step by step
        </p>
      </div>

      <FormStepper
        steps={configSteps}
        layout="horizontal"
        activeIndex={configStep}
        onStepChange={setConfigStep}
        containerClassName="mb-8"
      />

      <div className="config-form bg-background-surface-10 p-6 rounded-gd-12">
        {configStep === 0 && (
          <EnvironmentConfigForm
            data={configData.environment}
            onSave={data => updateConfigData("environment", data)}
          />
        )}
        {configStep === 1 && (
          <DatabaseConfigForm
            data={configData.database}
            onSave={data => updateConfigData("database", data)}
          />
        )}
        {configStep === 2 && (
          <ServiceConfigForm
            data={configData.services}
            onSave={data => updateConfigData("services", data)}
          />
        )}
        {configStep === 3 && (
          <SecurityConfigForm
            data={configData.security}
            onSave={data => updateConfigData("security", data)}
          />
        )}
      </div>
    </div>
  );
}
```

### 4. Form with Custom Icons and Styling

```tsx
import { FormStepper } from "gends";
import { IcUser, IcCreditCard, IcShield, IcConfirm } from "gends";

function CustomStyledFormStepper() {
  const [currentStep, setCurrentStep] = useState(1);

  const customSteps = [
    {
      title: "Profile Setup",
      completed: true,
      disabled: false,
    },
    {
      title: "Payment Method",
      completed: false,
      disabled: false,
    },
    {
      title: "Security Settings",
      completed: false,
      disabled: false,
    },
    {
      title: "Account Verification",
      completed: false,
      disabled: true,
    },
  ];

  const getCustomIcon = (stepIndex: number, isCompleted: boolean) => {
    if (isCompleted) {
      return <IcConfirm className="w-4 h-4 text-feedback-success-50" />;
    }

    const icons = [
      <IcUser className="w-4 h-4" />,
      <IcCreditCard className="w-4 h-4" />,
      <IcShield className="w-4 h-4" />,
      <IcConfirm className="w-4 h-4" />,
    ];

    return icons[stepIndex];
  };

  return (
    <div className="custom-form-stepper max-w-4xl mx-auto p-6">
      <FormStepper
        steps={customSteps}
        layout="horizontal"
        activeIndex={currentStep}
        onStepChange={setCurrentStep}
        containerClassName="custom-step-container"
        icon={getCustomIcon(currentStep, customSteps[currentStep]?.completed)}
      />

      <style jsx>{`
        .custom-step-container {
          background: linear-gradient(135deg, var(--gd-primary-10) 0%, var(--gd-secondary-10) 100%);
          border: 2px solid var(--gd-primary-20);
        }
      `}</style>
    </div>
  );
}
```

### 5. Progressive Form with Validation

```tsx
import { FormStepper } from "gends";
import { useState, useEffect } from "react";

function ProgressiveFormStepper() {
  const [activeStep, setActiveStep] = useState(0);
  const [stepValidation, setStepValidation] = useState({
    0: false, // Personal info
    1: false, // Address
    2: false, // Preferences
  });

  const progressiveSteps = [
    {
      title: "Personal Information",
      completed: stepValidation[0],
      disabled: false,
    },
    {
      title: "Address Details",
      completed: stepValidation[1],
      disabled: !stepValidation[0],
    },
    {
      title: "Preferences",
      completed: stepValidation[2],
      disabled: !stepValidation[1],
    },
  ];

  const validateStep = async (stepIndex: number, formData: any) => {
    // Simulate form validation
    const isValid = Object.values(formData).every(value => value && value.length > 0);

    setStepValidation(prev => ({
      ...prev,
      [stepIndex]: isValid,
    }));

    return isValid;
  };

  const handleStepChange = (stepIndex: number) => {
    // Only allow navigation to unlocked steps
    if (!progressiveSteps[stepIndex].disabled) {
      setActiveStep(stepIndex);
    }
  };

  const handleFormSubmit = async (stepIndex: number, formData: any) => {
    const isValid = await validateStep(stepIndex, formData);

    if (isValid && stepIndex < progressiveSteps.length - 1) {
      setActiveStep(stepIndex + 1);
    }
  };

  return (
    <div className="progressive-form max-w-4xl mx-auto p-6">
      <div className="form-header mb-6">
        <h2 className="text-en-desktop-heading-2xl mb-2">User Profile Setup</h2>
        <div className="progress-indicator">
          <span className="text-en-desktop-body-s text-text-subdued-1">
            Step {activeStep + 1} of {progressiveSteps.length}
          </span>
        </div>
      </div>

      <FormStepper
        steps={progressiveSteps}
        layout="horizontal"
        activeIndex={activeStep}
        onStepChange={handleStepChange}
        containerClassName="mb-8"
      />

      <div className="form-content">
        <FormStepContent
          step={activeStep}
          onSubmit={formData => handleFormSubmit(activeStep, formData)}
          onValidationChange={isValid =>
            setStepValidation(prev => ({ ...prev, [activeStep]: isValid }))
          }
        />
      </div>
    </div>
  );
}
```

### 6. Keyboard Navigation Focused Form

```tsx
import { FormStepper } from "gends";
import { useState, useRef, useEffect } from "react";

function KeyboardNavigationForm() {
  const [currentStep, setCurrentStep] = useState(0);
  const stepperRef = useRef<HTMLDivElement>(null);

  const keyboardSteps = [
    {
      title: "Basic Information",
      completed: currentStep > 0,
      disabled: false,
    },
    {
      title: "Contact Details",
      completed: currentStep > 1,
      disabled: false,
    },
    {
      title: "Review & Submit",
      completed: false,
      disabled: false,
    },
  ];

  // Auto-focus stepper on mount for keyboard users
  useEffect(() => {
    if (stepperRef.current) {
      const firstStep = stepperRef.current.querySelector('[role="tab"]') as HTMLElement;
      firstStep?.focus();
    }
  }, []);

  const handleStepChange = (stepIndex: number) => {
    setCurrentStep(stepIndex);

    // Announce step change to screen readers
    const announcement = `Now on step ${stepIndex + 1}: ${keyboardSteps[stepIndex].title}`;
    const announcer = document.createElement("div");
    announcer.setAttribute("aria-live", "polite");
    announcer.setAttribute("aria-atomic", "true");
    announcer.className = "sr-only";
    announcer.textContent = announcement;
    document.body.appendChild(announcer);

    setTimeout(() => document.body.removeChild(announcer), 1000);
  };

  return (
    <div className="keyboard-form max-w-4xl mx-auto p-6">
      <div className="instructions mb-6 p-4 bg-primary-10 rounded-gd-8">
        <h3 className="text-en-desktop-heading-l mb-2">Keyboard Navigation</h3>
        <ul className="text-en-desktop-body-s space-y-1">
          <li>
            • <kbd className="px-1 py-0.5 bg-background-surface-20 rounded">Tab</kbd> - Focus
            stepper
          </li>
          <li>
            • <kbd className="px-1 py-0.5 bg-background-surface-20 rounded">Arrow Keys</kbd> -
            Navigate steps
          </li>
          <li>
            • <kbd className="px-1 py-0.5 bg-background-surface-20 rounded">Enter/Space</kbd> -
            Select step
          </li>
          <li>
            • <kbd className="px-1 py-0.5 bg-background-surface-20 rounded">Home/End</kbd> -
            First/Last step
          </li>
        </ul>
      </div>

      <div ref={stepperRef}>
        <FormStepper
          steps={keyboardSteps}
          layout="horizontal"
          activeIndex={currentStep}
          onStepChange={handleStepChange}
          containerClassName="mb-8"
        />
      </div>

      <div className="form-section" role="tabpanel" aria-labelledby={`step-${currentStep}`}>
        <KeyboardFormContent step={currentStep} />
      </div>
    </div>
  );
}
```

## Contex 7-Specific Integration

### Theme Integration

```tsx
import { FormStepper } from "gends";
import { useContex7Theme } from "@contex7/react";

function ThemedFormStepper() {
  const { theme, mode } = useContex7Theme();

  return (
    <div className={`theme-${theme} mode-${mode}`}>
      <FormStepper
        steps={steps}
        layout="horizontal"
        activeIndex={currentStep}
        onStepChange={handleStepChange}
        containerClassName="themed-form-stepper"
        // Component automatically adapts to Contex 7 theme variables
      />
    </div>
  );
}
```

### Form State Management

```tsx
import { FormStepper } from "gends";
import { useContex7Form } from "@contex7/forms";

function ManagedFormStepper() {
  const form = useContex7Form({
    schema: multiStepFormSchema,
    onStepChange: step => {
      analytics.track("form_step_changed", { step, timestamp: Date.now() });
    },
  });

  return (
    <FormStepper
      steps={form.steps}
      activeIndex={form.currentStep}
      onStepChange={form.goToStep}
      layout={form.layout}
    />
  );
}
```

### Real-time Validation Integration

```tsx
import { FormStepper } from "gends";
import { useContex7Validation } from "@contex7/validation";

function ValidatedFormStepper() {
  const validation = useContex7Validation({
    steps: formSteps,
    realTimeValidation: true,
    serverSideValidation: true,
  });

  const steps = formSteps.map((step, index) => ({
    ...step,
    completed: validation.isStepValid(index),
    disabled: !validation.isStepAccessible(index),
  }));

  return (
    <FormStepper
      steps={steps}
      activeIndex={validation.currentStep}
      onStepChange={validation.goToStep}
      layout="horizontal"
    />
  );
}
```

## MCP Server Integration Guide

### 1. Server Setup Requirements

```typescript
// server/form-config.ts
import { MCPFormServer } from "@mcp/forms";
import { Contex7FormPlugin } from "@contex7/mcp-forms";
import { GenesisFormPlugin } from "@gends/mcp-forms";

const formServer = new MCPFormServer({
  plugins: [
    new Contex7FormPlugin({
      theme: "falcon",
      validation: {
        realTime: true,
        serverSide: true,
      },
    }),
    new GenesisFormPlugin({
      components: ["FormStepper"],
      accessibility: "enhanced",
      keyboardNavigation: true,
    }),
  ],
});
```

### 2. Form Workflow Management

```typescript
// form/workflow-manager.ts
import { FormWorkflowManager } from "@mcp/form-workflow";

export class MCPFormWorkflowManager extends FormWorkflowManager {
  async validateStep(formId: string, stepIndex: number, formData: any) {
    const validation = await this.runValidation(formId, stepIndex, formData);

    await this.updateFormState(formId, {
      [`steps.${stepIndex}.completed`]: validation.isValid,
      [`steps.${stepIndex}.errors`]: validation.errors,
      lastValidated: new Date().toISOString(),
    });

    // Emit real-time validation update
    this.emit("form:step-validated", {
      formId,
      stepIndex,
      isValid: validation.isValid,
      errors: validation.errors,
      timestamp: Date.now(),
    });

    return validation;
  }

  async completeStep(formId: string, stepIndex: number) {
    await this.updateFormState(formId, {
      [`steps.${stepIndex}.completed`]: true,
      currentStep: Math.min(stepIndex + 1, this.getStepCount(formId) - 1),
    });
  }
}
```

### 3. Environment Configuration

```bash
# .env.local
MCP_FORM_SERVER_URL=http://localhost:3002
CONTEX7_FORM_VALIDATION=real-time
GENDS_FORM_ACCESSIBILITY=enhanced
FORM_STEPPER_DEFAULT_LAYOUT=horizontal
FORM_AUTO_SAVE=true
FORM_KEYBOARD_NAVIGATION=true
```

### 4. Build Configuration

```typescript
// vite.config.ts / webpack.config.js
export default {
  plugins: [
    gendsOptimizer({
      components: ["FormStepper"],
      formComponents: true,
      accessibilityOptimization: true,
    }),
    contex7Integration({
      formSupport: true,
      validationPipeline: true,
      keyboardEnhancement: true,
    }),
  ],
  resolve: {
    alias: {
      "@gends/forms": path.resolve(__dirname, "src/components/genesis/molecules"),
    },
  },
};
```

## Integration Tips for MCP Server Teams

### Form Management Best Practices

1. **Step Validation**: Implement both client and server-side validation
2. **Auto-Save**: Persist form data automatically between steps
3. **Accessibility**: Ensure comprehensive keyboard navigation and screen reader support
4. **Progressive Enhancement**: Design forms to work without JavaScript

### Performance Optimization

1. **Lazy Loading**: Load form steps dynamically as needed
2. **State Persistence**: Use optimized storage for form state
3. **Validation Debouncing**: Debounce real-time validation to reduce server load
4. **Component Memoization**: Memoize form components to prevent unnecessary re-renders

### Accessibility Considerations

1. **ARIA Labels**: Provide comprehensive labeling for screen readers
2. **Keyboard Navigation**: Full keyboard support with logical tab order
3. **Focus Management**: Proper focus handling during step transitions
4. **Screen Reader Announcements**: Live announcements for step changes

### Testing Integration

```typescript
// tests/form-stepper.test.tsx
import { render, screen, fireEvent } from "@testing-library/react";
import { FormStepper } from "gends";
import { MCPFormProvider } from "@mcp/testing";

describe("FormStepper MCP Integration", () => {
  it("should handle step navigation", async () => {
    const mockSteps = [
      { title: "Step 1", completed: true, disabled: false },
      { title: "Step 2", completed: false, disabled: false },
    ];

    const handleStepChange = jest.fn();

    render(
      <MCPFormProvider mockServer={mockFormServer}>
        <FormStepper
          steps={mockSteps}
          activeIndex={0}
          onStepChange={handleStepChange}
          layout="horizontal"
        />
      </MCPFormProvider>
    );

    const stepTwo = screen.getByText("Step 2");
    fireEvent.click(stepTwo);

    expect(handleStepChange).toHaveBeenCalledWith(1);
  });

  it("should support keyboard navigation", () => {
    render(
      <FormStepper
        steps={mockSteps}
        activeIndex={0}
        onStepChange={handleStepChange}
      />
    );

    const firstStep = screen.getByRole("tab", { name: /step 1/i });
    firstStep.focus();

    fireEvent.keyDown(firstStep, { key: "ArrowRight" });
    expect(handleStepChange).toHaveBeenCalledWith(1);
  });
});
```

## Related Gends Components

- **`StepperFlow`**: Advanced stepper with complex workflow management
- **`ProgressStepper`**: Progress-focused stepper with completion indicators
- **`Stepper`**: Base stepper primitive components
- **`Form`**: Form container and validation components
- **`Button`**: Navigation and form action buttons
- **`Badge`**: Status and validation indicators

## Browser Support

Compatible with all browsers supported by the Contex 7 runtime:

- **Chrome**: 88+ (full feature support including advanced accessibility)
- **Firefox**: 85+ (full feature support with keyboard navigation)
- **Safari**: 14+ (full feature support with VoiceOver integration)
- **Edge**: 88+ (full feature support with Narrator integration)
- **Mobile**: iOS 14+, Android Chrome 88+ (touch-optimized)

## Troubleshooting

### Common Issues

1. **Step State Not Updating**: Ensure `activeIndex` and `onStepChange` are properly managed
2. **Keyboard Navigation**: Verify that disabled steps don't interfere with navigation flow
3. **Theme Issues**: Check that Contex 7 theme provider wraps the FormStepper
4. **Form Validation**: Ensure step completion state aligns with form validation results

### Debug Mode

```tsx
// Enable debug mode for development
<FormStepper
  steps={steps}
  activeIndex={currentStep}
  onStepChange={step => {
    console.log("[DEBUG] FormStepper step changed:", step);
    console.log("[DEBUG] Current step state:", steps[step]);
    console.log("[DEBUG] Form validation state:", formValidation);
    handleStepChange(step);
  }}
  containerClassName="debug-form-stepper"
/>
```

### Accessibility Testing

```tsx
import { axe, toHaveNoViolations } from "jest-axe";

expect.extend(toHaveNoViolations);

describe("FormStepper Accessibility", () => {
  it("should have no accessibility violations", async () => {
    const { container } = render(
      <FormStepper steps={steps} activeIndex={0} onStepChange={jest.fn()} />
    );
    const results = await axe(container);
    expect(results).toHaveNoViolations();
  });
});
```

## Advanced Customization

### Custom Step Rendering

```tsx
const customSteps = [
  {
    title: "Account Setup",
    completed: true,
    disabled: false,
  },
];

<FormStepper
  steps={customSteps}
  activeIndex={0}
  onStepChange={handleStepChange}
  titleHtml={
    <div className="custom-step-title">
      <span className="step-number">01</span>
      <span className="step-name">Account Setup</span>
      <span className="step-status">✓ Complete</span>
    </div>
  }
/>;
```

### Dynamic Step Generation

```tsx
function DynamicFormStepper({ formConfig }) {
  const generateSteps = useCallback(() => {
    return formConfig.sections.map((section, index) => ({
      title: section.name,
      completed: section.isValid && section.isComplete,
      disabled: !section.isAccessible,
    }));
  }, [formConfig]);

  return (
    <FormStepper
      steps={generateSteps()}
      activeIndex={formConfig.currentSection}
      onStepChange={formConfig.goToSection}
      layout={formConfig.layout}
    />
  );
}
```

---

**Note**: This component is part of the Genesis Design System (Gends) and is optimized for MCP server architectures powered by Contex 7. For additional support, form integration assistance, or accessibility guidance, refer to the [Gends Documentation Portal](https://gends.docs.dev) or contact the MCP development team.
