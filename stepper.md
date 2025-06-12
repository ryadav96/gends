# Stepper Component

## Overview

The Stepper component is a comprehensive and flexible multi-step navigation system designed to guide users through sequential processes. Built with Genesis Design System tokens and Radix UI primitives, it offers multiple variants including basic steppers, progress steppers with circular indicators, and stepper flows with customizable separators. The component supports both horizontal and vertical orientations, multiple step states, custom indicators, and full accessibility features for optimal user experience.

## Component API

### Stepper Props

| Prop            | Type                         | Default        | Description                           |
| --------------- | ---------------------------- | -------------- | ------------------------------------- |
| `defaultValue`  | `number`                     | `0`            | Initial active step (zero-indexed)    |
| `value`         | `number`                     | `undefined`    | Controlled active step value          |
| `onValueChange` | `(value: number) => void`    | `undefined`    | Callback when the active step changes |
| `orientation`   | `"horizontal" \| "vertical"` | `"horizontal"` | Layout orientation of the stepper     |
| `className`     | `string`                     | `undefined`    | Additional CSS classes                |
| `children`      | `React.ReactNode`            | `undefined`    | Stepper items and separators          |

### StepperItem Props

| Prop        | Type                        | Default      | Description                                   |
| ----------- | --------------------------- | ------------ | --------------------------------------------- |
| `step`      | `number`                    | `undefined`  | Step index number (required)                  |
| `stepState` | `StepState`                 | `"upcoming"` | Visual state of the step                      |
| `completed` | `boolean`                   | `false`      | Whether the step is completed                 |
| `disabled`  | `boolean`                   | `false`      | Whether the step is disabled                  |
| `loading`   | `boolean`                   | `false`      | Whether the step is in loading state          |
| `stepIcon`  | `React.ReactNode`           | `undefined`  | Custom icon for the step indicator            |
| `stepText`  | `string \| React.ReactNode` | `undefined`  | Custom text or content for the step indicator |
| `className` | `string`                    | `undefined`  | Additional CSS classes                        |
| `children`  | `React.ReactNode`           | `undefined`  | Step trigger and content                      |

### StepperIndicator Props

| Prop         | Type               | Default     | Description                                 |
| ------------ | ------------------ | ----------- | ------------------------------------------- |
| `icon`       | `React.ReactNode`  | `undefined` | Custom icon to display in the indicator     |
| `stepText`   | `string`           | `undefined` | Text to display in the indicator            |
| `showBorder` | `boolean`          | `true`      | Whether to show border around the indicator |
| `size`       | `number \| string` | `"32px"`    | Size of the indicator (CSS value)           |
| `className`  | `string`           | `undefined` | Additional CSS classes                      |

### StepState Type

```typescript
type StepState =
  | "active" // Interactive step with default styling
  | "completed" // Finished step with success indicator
  | "current" // Currently active step with filled indicator
  | "disabled" // Non-interactive step with muted styling
  | "error" // Step with error state and error indicator
  | "inactive" // Default inactive step
  | "loading" // Step showing loading spinner
  | "upcoming"; // Future step with default styling
```

## Stepper Variants

### 1. Basic Stepper

The basic stepper provides fundamental step navigation with customizable indicators and content.

```typescript
import { Stepper } from "gends";

// Basic horizontal stepper
<Stepper defaultValue={1} orientation="horizontal">
  <StepperItem step={0} stepState="completed">
    <StepperTrigger>
      <StepperIndicator />
      <div>
        <StepperTitle>Account Setup</StepperTitle>
        <StepperDescription>Create your credentials</StepperDescription>
      </div>
    </StepperTrigger>
  </StepperItem>

  <StepperSeparator />

  <StepperItem step={1} stepState="current">
    <StepperTrigger>
      <StepperIndicator />
      <div>
        <StepperTitle>Profile Information</StepperTitle>
        <StepperDescription>Add personal details</StepperDescription>
      </div>
    </StepperTrigger>
  </StepperItem>

  <StepperSeparator />

  <StepperItem step={2} stepState="upcoming">
    <StepperTrigger>
      <StepperIndicator />
      <div>
        <StepperTitle>Preferences</StepperTitle>
        <StepperDescription>Set your preferences</StepperDescription>
      </div>
    </StepperTrigger>
  </StepperItem>
</Stepper>
```

### 2. Progress Stepper

Enhanced stepper with circular progress indicators and status-based styling.

```typescript
import { ProgressStepper } from "gends";

const steps: ProgressStepConfig[] = [
  {
    step: 1,
    title: "Order Placed",
    description: "May 2, 2025 - 10:30 AM",
    status: "success",
  },
  {
    step: 2,
    title: "Processing",
    description: "May 2, 2025 - 11:15 AM",
    status: "default",
    progress: {
      percentage: 50,
      type: "success",
    },
  },
  {
    step: 3,
    title: "Shipped",
    description: "Estimated delivery",
    status: "default",
    progress: {
      percentage: 0,
      type: "default",
    },
  },
];

// Progress stepper with circular indicators
<ProgressStepper
  steps={steps}
  orientation="horizontal"
  size="md"
  defaultValue={1}
  circleStrokeWidth={2}
/>
```

### 3. Stepper Flow

Advanced stepper with enhanced customization options and separator styles.

```typescript
import { StepperFlow } from "gends";

const steps: StepConfig[] = [
  {
    step: 0,
    title: "Order Placed",
    description: "Order confirmation and details",
    stepState: "completed",
  },
  {
    step: 1,
    title: "Processing",
    description: "Preparing your shipment",
    stepState: "current",
  },
  {
    step: 2,
    title: "Shipped",
    description: "Package in transit",
    stepState: "upcoming",
  },
];

// Stepper flow with dotted separators
<StepperFlow
  steps={steps}
  orientation="horizontal"
  defaultValue={1}
  dottedSeparator={true}
  borderedIcon={true}
  indicatorSize="40px"
/>
```

## Orientation Options

### Horizontal Layout

Ideal for forms, checkout processes, and primary navigation flows.

```typescript
// Horizontal stepper with responsive layout
<Stepper orientation="horizontal" className="w-full max-w-4xl">
  {steps.map((step, index) => (
    <React.Fragment key={step.id}>
      <StepperItem step={index} stepState={step.state}>
        <StepperTrigger className="flex-col items-center">
          <StepperIndicator stepText={String(index + 1)} />
          <div className="text-center">
            <StepperTitle className="text-sm font-medium">
              {step.title}
            </StepperTitle>
            <StepperDescription className="text-xs text-muted-foreground">
              {step.description}
            </StepperDescription>
          </div>
        </StepperTrigger>
      </StepperItem>
      {index < steps.length - 1 && <StepperSeparator />}
    </React.Fragment>
  ))}
</Stepper>
```

### Vertical Layout

Perfect for sidebars, mobile interfaces, and detailed step descriptions.

```typescript
// Vertical stepper with detailed descriptions
<Stepper orientation="vertical" className="max-w-md">
  {steps.map((step, index) => (
    <StepperItem key={index} step={index} stepState={step.state}>
      <StepperTrigger className="items-start text-left">
        <StepperIndicator
          icon={step.icon}
          showBorder={true}
          size="40px"
        />
        <div className="ml-4">
          <StepperTitle className="font-semibold">
            {step.title}
          </StepperTitle>
          <StepperDescription className="mt-1 text-sm">
            {step.description}
          </StepperDescription>
          {step.additionalInfo && (
            <div className="mt-2 text-xs text-muted-foreground">
              {step.additionalInfo}
            </div>
          )}
        </div>
      </StepperTrigger>
    </StepperItem>
  ))}
</Stepper>
```

## Step States

### State Indicators

Different visual states communicate step status to users:

```typescript
// Completed step with success icon
<StepperItem step={0} stepState="completed">
  <StepperTrigger>
    <StepperIndicator icon={<CheckCircle className="w-5 h-5" />} />
    <StepperTitle>Account Created</StepperTitle>
  </StepperTrigger>
</StepperItem>

// Current active step
<StepperItem step={1} stepState="current">
  <StepperTrigger>
    <StepperIndicator stepText="2" />
    <StepperTitle>Profile Setup</StepperTitle>
  </StepperTrigger>
</StepperItem>

// Error step with alert icon
<StepperItem step={2} stepState="error">
  <StepperTrigger>
    <StepperIndicator icon={<AlertCircle className="w-5 h-5" />} />
    <StepperTitle>Verification Failed</StepperTitle>
  </StepperTrigger>
</StepperItem>

// Loading step with spinner
<StepperItem step={3} stepState="loading" loading={true}>
  <StepperTrigger>
    <StepperIndicator />
    <StepperTitle>Processing Payment</StepperTitle>
  </StepperTrigger>
</StepperItem>

// Disabled step
<StepperItem step={4} stepState="disabled" disabled={true}>
  <StepperTrigger>
    <StepperIndicator />
    <StepperTitle>Final Review</StepperTitle>
  </StepperTrigger>
</StepperItem>
```

### Progress States

For Progress Stepper, use status-based indicators:

```typescript
const statusSteps: ProgressStepConfig[] = [
  {
    step: 1,
    title: "Successful Step",
    description: "Completed successfully",
    status: "success",
  },
  {
    step: 2,
    title: "Warning Step",
    description: "Completed with warnings",
    status: "warning",
  },
  {
    step: 3,
    title: "Error Step",
    description: "Failed to complete",
    status: "error",
  },
  {
    step: 4,
    title: "In Progress",
    description: "Currently processing",
    status: "default",
    progress: {
      percentage: 75,
      type: "success",
    },
  },
];
```

## Size Variants

### Progress Stepper Sizes

```typescript
// Small size stepper
<ProgressStepper
  steps={steps}
  size="sm"
  orientation="horizontal"
  circleStrokeWidth={1}
/>

// Medium size stepper (default)
<ProgressStepper
  steps={steps}
  size="md"
  orientation="horizontal"
  circleStrokeWidth={2}
/>
```

### Custom Indicator Sizes

```typescript
// Stepper flow with custom indicator sizes
<StepperFlow
  steps={steps}
  indicatorSize="48px"  // Global size
  borderedIcon={true}
/>

// Individual step with custom size
const customSteps: StepConfig[] = [
  {
    step: 0,
    title: "Large Step",
    indicatorSize: "56px",  // Override global size
    stepIcon: <CustomIcon className="w-8 h-8" />,
  },
  {
    step: 1,
    title: "Normal Step",
    // Uses global indicatorSize
  },
];
```

## Separator Customization

### Solid Separators

```typescript
// Default solid separators
<StepperFlow
  steps={steps}
  dottedSeparator={false}
/>

// Custom separator colors
const coloredSteps: StepConfig[] = [
  {
    step: 0,
    title: "Step 1",
    dividerColor: "#22c55e", // Green separator
  },
  {
    step: 1,
    title: "Step 2",
    dividerColor: "#f59e0b", // Orange separator
  },
];
```

### Dotted Separators

```typescript
// Dotted style separators
<StepperFlow
  steps={steps}
  dottedSeparator={true}
  orientation="horizontal"
/>

// Vertical dotted separators
<StepperFlow
  steps={steps}
  dottedSeparator={true}
  orientation="vertical"
/>
```

## Real-World Examples

### 1. E-commerce Checkout Flow

```typescript
const CheckoutStepper = () => {
  const [currentStep, setCurrentStep] = useState(0);

  const checkoutSteps: StepConfig[] = [
    {
      step: 0,
      title: "Cart Review",
      description: "Review your items",
      stepState: currentStep > 0 ? "completed" : "current",
    },
    {
      step: 1,
      title: "Shipping",
      description: "Delivery information",
      stepState: currentStep > 1 ? "completed" : currentStep === 1 ? "current" : "upcoming",
    },
    {
      step: 2,
      title: "Payment",
      description: "Payment details",
      stepState: currentStep > 2 ? "completed" : currentStep === 2 ? "current" : "upcoming",
    },
    {
      step: 3,
      title: "Confirmation",
      description: "Order summary",
      stepState: currentStep === 3 ? "current" : "upcoming",
    },
  ];

  return (
    <div className="max-w-4xl mx-auto p-6">
      <StepperFlow
        steps={checkoutSteps}
        value={currentStep}
        onValueChange={setCurrentStep}
        orientation="horizontal"
        borderedIcon={true}
        className="mb-8"
      />

      <div className="bg-white p-6 rounded-lg border">
        {/* Step content based on currentStep */}
      </div>
    </div>
  );
};
```

### 2. Multi-Step Form Wizard

```typescript
const FormWizard = () => {
  const [activeStep, setActiveStep] = useState(0);
  const [formData, setFormData] = useState({});
  const [validation, setValidation] = useState({});

  const formSteps: ProgressStepConfig[] = [
    {
      step: 1,
      title: "Personal Information",
      description: "Basic details",
      status: validation.personal ? "success" : activeStep > 0 ? "error" : "default",
    },
    {
      step: 2,
      title: "Address Details",
      description: "Location information",
      status: validation.address ? "success" : activeStep > 1 ? "error" : "default",
      progress: activeStep === 1 ? { percentage: 50, type: "success" } : undefined,
    },
    {
      step: 3,
      title: "Preferences",
      description: "Customize settings",
      status: "default",
      progress: activeStep === 2 ? { percentage: 25, type: "default" } : undefined,
    },
  ];

  return (
    <div className="max-w-2xl mx-auto p-6">
      <ProgressStepper
        steps={formSteps}
        value={activeStep}
        onValueChange={setActiveStep}
        orientation="horizontal"
        size="md"
        className="mb-8"
      />

      <form className="space-y-6">
        {/* Dynamic form content */}
      </form>
    </div>
  );
};
```

### 3. Order Status Tracker

```typescript
const OrderTracker = ({ orderId, orderStatus }) => {
  const trackingSteps: ProgressStepConfig[] = [
    {
      step: 1,
      title: "Order Placed",
      description: orderStatus.placed ? orderStatus.placed.date : "Pending",
      status: orderStatus.placed ? "success" : "default",
    },
    {
      step: 2,
      title: "Processing",
      description: orderStatus.processing ? orderStatus.processing.date : "In queue",
      status: orderStatus.processing
        ? "success"
        : orderStatus.placed
        ? "default"
        : "default",
      progress: orderStatus.processing
        ? { percentage: 100, type: "success" }
        : orderStatus.placed
        ? { percentage: 30, type: "default" }
        : undefined,
    },
    {
      step: 3,
      title: "Shipped",
      description: orderStatus.shipped
        ? `Tracking: ${orderStatus.shipped.tracking}`
        : "Awaiting shipment",
      status: orderStatus.shipped ? "success" : "default",
      progress: orderStatus.shipped
        ? { percentage: 100, type: "success" }
        : orderStatus.processing
        ? { percentage: 60, type: "default" }
        : undefined,
    },
    {
      step: 4,
      title: "Delivered",
      description: orderStatus.delivered
        ? orderStatus.delivered.date
        : "Estimated delivery",
      status: orderStatus.delivered ? "success" : "default",
      progress: orderStatus.delivered
        ? { percentage: 100, type: "success" }
        : orderStatus.shipped
        ? { percentage: 80, type: "default" }
        : undefined,
    },
  ];

  return (
    <div className="max-w-3xl mx-auto p-6">
      <div className="mb-6">
        <h2 className="text-2xl font-bold">Order #{orderId}</h2>
        <p className="text-muted-foreground">Track your order status</p>
      </div>

      <ProgressStepper
        steps={trackingSteps}
        orientation="vertical"
        size="md"
        circleStrokeWidth={2}
        className="max-w-md"
      />
    </div>
  );
};
```

### 4. Onboarding Progress

```typescript
const OnboardingFlow = () => {
  const [currentStep, setCurrentStep] = useState(0);
  const [completedSteps, setCompletedSteps] = useState(new Set());

  const onboardingSteps: StepConfig[] = [
    {
      step: 0,
      title: "Welcome",
      description: "Get started with our platform",
      stepState: "completed",
      stepIcon: <CheckCircle className="w-5 h-5" />,
    },
    {
      step: 1,
      title: "Setup Profile",
      description: "Add your personal information",
      stepState: currentStep === 1 ? "current" : completedSteps.has(1) ? "completed" : "upcoming",
      stepText: "2",
    },
    {
      step: 2,
      title: "Connect Accounts",
      description: "Link your external accounts",
      stepState: currentStep === 2 ? "current" : completedSteps.has(2) ? "completed" : "upcoming",
      stepText: "3",
    },
    {
      step: 3,
      title: "Customize Dashboard",
      description: "Personalize your workspace",
      stepState: currentStep === 3 ? "current" : completedSteps.has(3) ? "completed" : "upcoming",
      stepText: "4",
    },
  ];

  const handleStepComplete = (stepIndex) => {
    setCompletedSteps(prev => new Set([...prev, stepIndex]));
    if (stepIndex < onboardingSteps.length - 1) {
      setCurrentStep(stepIndex + 1);
    }
  };

  return (
    <div className="min-h-screen bg-background">
      <div className="max-w-4xl mx-auto p-6">
        <div className="mb-8">
          <StepperFlow
            steps={onboardingSteps}
            value={currentStep}
            orientation="horizontal"
            borderedIcon={false}
            dottedSeparator={false}
            indicatorSize="36px"
          />
        </div>

        <div className="bg-card p-8 rounded-lg border">
          {/* Step-specific content */}
          <OnboardingStepContent
            step={currentStep}
            onComplete={() => handleStepComplete(currentStep)}
          />
        </div>
      </div>
    </div>
  );
};
```

### 5. Project Workflow Tracker

```typescript
const WorkflowTracker = ({ projectId, workflow }) => {
  const workflowSteps: StepConfig[] = workflow.steps.map((step, index) => ({
    step: index,
    title: step.name,
    description: `${step.assignee} • ${step.estimatedTime}`,
    stepState:
      step.status === "completed" ? "completed" :
      step.status === "in_progress" ? "current" :
      step.status === "blocked" ? "error" :
      step.status === "pending" ? "upcoming" : "disabled",
    stepIcon: step.status === "completed" ? <CheckCircle className="w-4 h-4" /> :
              step.status === "blocked" ? <AlertCircle className="w-4 h-4" /> : undefined,
    loading: step.status === "in_progress",
    dividerColor: step.priority === "high" ? "#ef4444" :
                  step.priority === "medium" ? "#f59e0b" : "#6b7280",
  }));

  return (
    <div className="max-w-5xl mx-auto p-6">
      <div className="mb-6">
        <h1 className="text-3xl font-bold">{workflow.name}</h1>
        <p className="text-muted-foreground">Project #{projectId}</p>
      </div>

      <StepperFlow
        steps={workflowSteps}
        orientation="vertical"
        borderedIcon={true}
        dottedSeparator={false}
        indicatorSize="44px"
        stepClassName="pb-6"
      />
    </div>
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab**: Navigate between interactive steps
- **Enter/Space**: Activate the focused step
- **Arrow Keys**: Move between steps in keyboard navigation mode
- **Home/End**: Jump to first/last step

### Screen Reader Support

```typescript
// Enhanced accessibility with ARIA attributes
<Stepper
  aria-label="Multi-step form progress"
  role="group"
>
  <StepperItem
    step={0}
    stepState="completed"
    aria-label="Step 1 of 4: Personal Information - Completed"
  >
    <StepperTrigger
      aria-current={false}
      aria-describedby="step-1-description"
    >
      <StepperIndicator aria-hidden="true" />
      <div>
        <StepperTitle>Personal Information</StepperTitle>
        <StepperDescription id="step-1-description">
          Enter your basic details
        </StepperDescription>
      </div>
    </StepperTrigger>
  </StepperItem>
</Stepper>
```

### Visual Accessibility

- High contrast mode support
- Proper color coding for different states
- Clear visual hierarchy with typography
- Focus indicators for keyboard navigation
- Loading states with appropriate feedback

## Design System Integration

### Genesis Design Tokens

The Stepper component uses Genesis Design System tokens for consistent styling:

```css
/* Step indicators */
--step-indicator-size: var(--gd-spacing-32);
--step-indicator-border: var(--gd-border-width-1);
--step-indicator-radius: var(--gd-border-radius-full);

/* Colors */
--step-completed-bg: var(--gd-color-success-50);
--step-current-bg: var(--gd-color-primary-50);
--step-error-bg: var(--gd-color-error-50);
--step-disabled-bg: var(--gd-neutral-grey-30);

/* Separators */
--separator-color: var(--gd-neutral-grey-40);
--separator-thickness: 2px;

/* Typography */
--step-title-font: var(--gd-font-weight-600);
--step-description-font: var(--gd-font-weight-400);
--step-description-color: var(--gd-text-subdued-1);
```

### Theme Support

```typescript
// Dark mode compatible
<Stepper className="dark:bg-gray-900">
  <StepperItem stepState="completed">
    <StepperIndicator className="dark:bg-green-600 dark:text-white" />
  </StepperItem>
</Stepper>

// Custom theme integration
<StepperFlow
  steps={steps}
  className="falcon-theme"
  stepClassName="custom-step-styling"
/>
```

## Best Practices

### Performance Optimization

- Use `useMemo` for large step arrays
- Implement virtualization for 50+ steps
- Lazy load step content when possible
- Optimize separator rendering

```typescript
const OptimizedStepper = ({ steps }) => {
  const memoizedSteps = useMemo(() =>
    steps.map(step => ({
      ...step,
      component: lazy(() => import(`./steps/${step.component}`))
    })),
    [steps]
  );

  return (
    <Stepper>
      {memoizedSteps.map((step, index) => (
        <StepperItem key={step.id} step={index}>
          <Suspense fallback={<StepSkeleton />}>
            <step.component />
          </Suspense>
        </StepperItem>
      ))}
    </Stepper>
  );
};
```

### UX Guidelines

- **Logical Flow**: Arrange steps in a logical sequence
- **Clear Labels**: Use descriptive titles and descriptions
- **Progress Indication**: Show completion status clearly
- **Error Handling**: Provide clear error states and recovery paths
- **Responsive Design**: Adapt to different screen sizes

### State Management

```typescript
// Comprehensive state management for complex steppers
const useStepperState = initialSteps => {
  const [currentStep, setCurrentStep] = useState(0);
  const [stepStates, setStepStates] = useState(
    initialSteps.reduce(
      (acc, step, index) => ({
        ...acc,
        [index]: index === 0 ? "current" : "upcoming",
      }),
      {}
    )
  );
  const [stepData, setStepData] = useState({});

  const completeStep = (stepIndex, data) => {
    setStepData(prev => ({ ...prev, [stepIndex]: data }));
    setStepStates(prev => ({
      ...prev,
      [stepIndex]: "completed",
      [stepIndex + 1]: "current",
    }));
    setCurrentStep(stepIndex + 1);
  };

  const markStepError = (stepIndex, error) => {
    setStepStates(prev => ({ ...prev, [stepIndex]: "error" }));
    setStepData(prev => ({
      ...prev,
      [stepIndex]: { ...prev[stepIndex], error },
    }));
  };

  return {
    currentStep,
    stepStates,
    stepData,
    completeStep,
    markStepError,
    setCurrentStep,
  };
};
```

## Troubleshooting

### Common Issues

**Step indicators not displaying correctly**

```typescript
// Ensure proper step numbering (zero-indexed)
<StepperItem step={0} /> // First step
<StepperItem step={1} /> // Second step

// Check for missing StepperIndicator
<StepperTrigger>
  <StepperIndicator /> {/* Required for visual indicator */}
  <StepperTitle>Step Title</StepperTitle>
</StepperTrigger>
```

**Separators not appearing between steps**

```typescript
// Add StepperSeparator between StepperItems
<StepperItem step={0}>...</StepperItem>
<StepperSeparator /> {/* Required between steps */}
<StepperItem step={1}>...</StepperItem>
```

**Vertical layout issues**

```typescript
// Ensure proper container height for vertical steppers
<div className="min-h-screen"> {/* Or appropriate height */}
  <Stepper orientation="vertical">
    {/* Steps */}
  </Stepper>
</div>
```

**Step state synchronization**

```typescript
// Use controlled mode for dynamic step states
const [activeStep, setActiveStep] = useState(0);
const [completedSteps, setCompletedSteps] = useState(new Set());

const getStepState = index => {
  if (completedSteps.has(index)) return "completed";
  if (index === activeStep) return "current";
  return "upcoming";
};
```

### Performance Issues

**Large number of steps**

```typescript
// Implement step virtualization for 50+ steps
import { FixedSizeList as List } from 'react-window';

const VirtualizedStepper = ({ steps }) => (
  <List
    height={400}
    itemCount={steps.length}
    itemSize={80}
    itemData={steps}
  >
    {({ index, style, data }) => (
      <div style={style}>
        <StepperItem step={index} stepState={data[index].state}>
          {/* Step content */}
        </StepperItem>
      </div>
    )}
  </List>
);
```

**Slow step transitions**

```typescript
// Optimize with proper memoization
const MemoizedStepperItem = memo(({ step, state, title }) => (
  <StepperItem step={step} stepState={state}>
    <StepperTrigger>
      <StepperIndicator />
      <StepperTitle>{title}</StepperTitle>
    </StepperTrigger>
  </StepperItem>
));
```

## Migration Guide

### From Basic Stepper to Progress Stepper

```typescript
// Before (Basic Stepper)
<Stepper defaultValue={1}>
  <StepperItem step={0} stepState="completed">
    <StepperTrigger>
      <StepperIndicator />
      <StepperTitle>Step 1</StepperTitle>
    </StepperTrigger>
  </StepperItem>
</Stepper>

// After (Progress Stepper)
const steps: ProgressStepConfig[] = [
  {
    step: 1,
    title: "Step 1",
    status: "success",
  },
];

<ProgressStepper steps={steps} defaultValue={0} />
```

### From Manual Step Management to Stepper Flow

```typescript
// Before (Manual management)
{steps.map((step, index) => (
  <React.Fragment key={index}>
    <StepperItem step={index} stepState={step.state}>
      {/* Manual step configuration */}
    </StepperItem>
    {index < steps.length - 1 && <StepperSeparator />}
  </React.Fragment>
))}

// After (Stepper Flow)
<StepperFlow
  steps={steps}
  orientation="horizontal"
  defaultValue={0}
/>
```

## Summary

The Stepper component provides a comprehensive solution for multi-step interfaces with three main variants:

- **Basic Stepper**: Full customization with individual components
- **Progress Stepper**: Circular indicators with progress tracking
- **Stepper Flow**: Enhanced features with separator customization

Key features include multiple orientations, extensive state management, custom indicators, accessibility support, and seamless Genesis Design System integration. Use the basic stepper for maximum flexibility, progress stepper for status tracking, and stepper flow for streamlined implementation with advanced features.
