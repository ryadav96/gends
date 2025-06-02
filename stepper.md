# Stepper

A flexible stepper component that guides users through a sequence of steps or stages, with support for multiple states, orientations, and customizable indicators—perfect for multi-step forms, wizards, and progress tracking.

---

## 1. Quick start

```tsx
import {
  Stepper,
  StepperItem,
  StepperTrigger,
  StepperIndicator,
  StepperTitle,
  StepperDescription,
  StepperSeparator,
} from "gends";

function Example() {
  return (
    <Stepper defaultValue={0}>
      <StepperItem step={0} stepState="completed">
        <StepperTrigger>
          <StepperIndicator />
          <div>
            <StepperTitle>Step 1</StepperTitle>
            <StepperDescription>Personal details</StepperDescription>
          </div>
        </StepperTrigger>
      </StepperItem>
      <StepperSeparator />
      <StepperItem step={1} stepState="current">
        <StepperTrigger>
          <StepperIndicator />
          <div>
            <StepperTitle>Step 2</StepperTitle>
            <StepperDescription>Address information</StepperDescription>
          </div>
        </StepperTrigger>
      </StepperItem>
    </Stepper>
  );
}
```

Compose stepper elements to create a customized multi-step interface.

---

## 2. Step States

| State       | Description       | Visual Style     | Use Case         |
| ----------- | ----------------- | ---------------- | ---------------- |
| `active`    | Currently focused | Default styling  | Interactive step |
| `completed` | Step finished     | Green check icon | Completed steps  |
| `current`   | Current step      | Filled indicator | Current position |
| `disabled`  | Not interactive   | Grayed out       | Locked steps     |
| `error`     | Error state       | Error icon       | Invalid steps    |
| `inactive`  | Not active        | Default styling  | Other steps      |
| `loading`   | Processing        | Loading spinner  | Async operations |
| `upcoming`  | Future step       | Default styling  | Pending steps    |

```tsx
<StepperItem stepState="completed" />
<StepperItem stepState="current" />
<StepperItem stepState="error" />
<StepperItem stepState="disabled" />
```

---

## 3. Orientations

| Orientation  | Description          | Use Case                         |
| ------------ | -------------------- | -------------------------------- |
| `horizontal` | Left to right layout | Default flow, header navigation  |
| `vertical`   | Top to bottom layout | Sidebar navigation, mobile views |

```tsx
<Stepper orientation="horizontal">
  {/* Steps */}
</Stepper>

<Stepper orientation="vertical">
  {/* Steps */}
</Stepper>
```

---

## 4. Indicators

Customize step indicators with icons, numbers, or custom content:

```tsx
// Default indicator
<StepperIndicator />

// Custom icon
<StepperIndicator icon={<CustomIcon />} />

// Step number
<StepperIndicator stepText="1" />

// Custom size
<StepperIndicator size="40px" />

// Custom styling
<StepperIndicator showBorder={false} className="bg-primary" />
```

---

## 5. Full prop reference

### Stepper Component

| Prop            | Type                         | Default        | Description            |
| --------------- | ---------------------------- | -------------- | ---------------------- |
| `defaultValue`  | `number`                     | `0`            | Initial active step    |
| `value`         | `number`                     | -              | Controlled active step |
| `onValueChange` | `(value: number) => void`    | -              | Step change handler    |
| `orientation`   | `"horizontal" \| "vertical"` | `"horizontal"` | Layout direction       |

### StepperItem

| Prop        | Type                  | Default      | Description         |
| ----------- | --------------------- | ------------ | ------------------- |
| `step`      | `number`              | -            | Step index          |
| `stepState` | `StepState`           | `"upcoming"` | Current state       |
| `disabled`  | `boolean`             | `false`      | Disable interaction |
| `loading`   | `boolean`             | `false`      | Show loading state  |
| `stepIcon`  | `ReactNode`           | -            | Custom step icon    |
| `stepText`  | `string \| ReactNode` | -            | Step text/content   |

### StepperIndicator

| Prop         | Type               | Default  | Description      |
| ------------ | ------------------ | -------- | ---------------- |
| `icon`       | `ReactNode`        | -        | Custom icon      |
| `stepText`   | `string`           | -        | Text content     |
| `showBorder` | `boolean`          | `true`   | Show border      |
| `size`       | `number \| string` | `"32px"` | Indicator size   |
| `asChild`    | `boolean`          | `false`  | Merge with child |

---

## 6. Recipes

### Basic wizard stepper

```tsx
function WizardStepper({ steps, currentStep }) {
  return (
    <Stepper value={currentStep} className="w-full max-w-3xl mx-auto">
      {steps.map((step, index) => (
        <React.Fragment key={index}>
          <StepperItem
            step={index}
            stepState={
              index < currentStep ? "completed" : index === currentStep ? "current" : "upcoming"
            }
          >
            <StepperTrigger>
              <StepperIndicator />
              <div>
                <StepperTitle>{step.title}</StepperTitle>
                <StepperDescription>{step.description}</StepperDescription>
              </div>
            </StepperTrigger>
          </StepperItem>
          {index < steps.length - 1 && <StepperSeparator />}
        </React.Fragment>
      ))}
    </Stepper>
  );
}
```

### Form stepper with validation

```tsx
function FormStepper({ steps, activeStep, errors }) {
  return (
    <Stepper value={activeStep} orientation="vertical">
      {steps.map((step, index) => (
        <StepperItem
          key={index}
          step={index}
          stepState={
            errors[step.id]
              ? "error"
              : index < activeStep
                ? "completed"
                : index === activeStep
                  ? "current"
                  : "upcoming"
          }
        >
          <StepperTrigger>
            <StepperIndicator />
            <div>
              <StepperTitle>{step.title}</StepperTitle>
              {errors[step.id] && (
                <StepperDescription className="text-error-500">
                  {errors[step.id]}
                </StepperDescription>
              )}
            </div>
          </StepperTrigger>
        </StepperItem>
      ))}
    </Stepper>
  );
}
```

### Async step processing

```tsx
function AsyncStepper({ onStepComplete }) {
  const [loading, setLoading] = useState(false);
  const [currentStep, setCurrentStep] = useState(0);

  const handleStepClick = async step => {
    setLoading(true);
    await onStepComplete(step);
    setLoading(false);
    setCurrentStep(step + 1);
  };

  return (
    <Stepper value={currentStep}>
      <StepperItem step={0} stepState={loading ? "loading" : "current"} loading={loading}>
        <StepperTrigger onClick={() => handleStepClick(0)}>
          <StepperIndicator />
          <StepperTitle>Process Step</StepperTitle>
        </StepperTrigger>
      </StepperItem>
    </Stepper>
  );
}
```

---

## 7. Accessibility considerations

- Uses semantic HTML structure
- Supports keyboard navigation
- Maintains focus management
- Provides ARIA attributes
- Indicates current step

```tsx
<Stepper aria-label="Registration process">
  <StepperItem role="tab" aria-selected={isCurrent}>
    <StepperTrigger aria-label="Step 1: Personal Details">{/* Content */}</StepperTrigger>
  </StepperItem>
</Stepper>
```

---

## 8. Design patterns

### Layout patterns

- Consistent spacing
- Clear visual hierarchy
- Proper alignment
- Responsive design

### State patterns

- Clear state indication
- Smooth transitions
- Loading feedback
- Error states

### Content patterns

- Clear step labels
- Concise descriptions
- Meaningful icons
- Progress indication

---
