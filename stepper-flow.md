# StepperFlow Component Documentation

## Overview

The `StepperFlow` component is a sophisticated, highly configurable stepper interface built with **Gends** (Genesis Design System) and optimized for **MCP (Modular Component Platform)** servers powered by **Contex 7**. This component provides a comprehensive solution for creating interactive, multi-step workflows with advanced customization options, state management, and accessibility features.

As a foundational atom-level component in the Gends design system, StepperFlow serves as the base layer for complex workflow visualizations, enabling developers to build intuitive user journey interfaces that integrate seamlessly with MCP server architectures.

## Purpose in Gends-MCP-Contex7 Ecosystem

Within the **Gends-MCP-Contex7** ecosystem, the StepperFlow component serves as the foundation for workflow management:

### MCP Server Integration

- **Complex Workflow Orchestration**: Handle multi-step server processes with advanced state management
- **Process Visualization**: Create detailed visual representations of server operations and pipelines
- **Interactive User Flows**: Enable user-driven workflows for configuration, setup, and administration
- **State Synchronization**: Real-time synchronization between client UI and server-side process states

### Contex 7 Compatibility

- **Advanced Theming**: Full integration with Contex 7's sophisticated theming engine
- **Performance Optimized**: Leverages Contex 7's rendering pipeline for smooth step transitions
- **Context-Aware**: Integrates with Contex 7's context management for complex state scenarios
- **Accessibility Compliant**: Meets and exceeds Contex 7's accessibility standards

## Installation & Import

### Standard Gends Import

```typescript
import { StepperFlow } from "gends";
import type { StepConfig, StepperFlowProps, StepState } from "gends";
import {
  IcConfirm,
  IcError,
  IcAlert,
  IcDatabase,
  IcCode,
  IcGlobe,
  IcShield,
  IcRefresh,
} from "gends";
```

### Alternative Import (Local Development)

```typescript
import { StepperFlow } from "gends";
import type { StepConfig, StepperFlowProps } from "gends";
import type { StepState } from "gends";
import {
  IcConfirm,
  IcError,
  IcAlert,
  IcDatabase,
  IcCode,
  IcGlobe,
  IcShield,
  IcRefresh,
  IcWarning,
} from "@/components/genesis/Icons/Icons";
```

## Component Variants

### 1. **Orientation Variants**

#### Horizontal Layout (Default)

- **Use Case**: Main workflows, progress tracking, dashboard timelines
- **Best For**: Wide content areas, desktop interfaces, linear processes
- **Features**: Auto-adjusting step widths, responsive separator scaling

#### Vertical Layout

- **Use Case**: Sidebar workflows, step-by-step wizards, narrow containers
- **Best For**: Navigation panels, detailed step descriptions, mobile-first designs
- **Features**: Vertical separators, optimized for scrolling content

### 2. **Step State Variants**

#### Active State

- **Visual**: Highlighted indicator with accent colors
- **Purpose**: Currently active/focused step
- **MCP Context**: Current server operation or user focus

#### Completed State

- **Visual**: Success icon with completion styling
- **Purpose**: Successfully finished steps
- **MCP Context**: Completed server processes, successful operations

#### Current State

- **Visual**: Primary accent styling with emphasis
- **Purpose**: Step currently being executed
- **MCP Context**: Active server process, real-time operation

#### Error State

- **Visual**: Error icon with alert styling
- **Purpose**: Failed or problematic steps
- **MCP Context**: Failed server operations, error states

#### Loading State

- **Visual**: Animated spinner or progress indicator
- **Purpose**: Steps currently processing
- **MCP Context**: Server operations in progress

#### Disabled State

- **Visual**: Muted colors, reduced opacity
- **Purpose**: Unavailable or locked steps
- **MCP Context**: Conditional steps, permission-restricted operations

#### Upcoming State

- **Visual**: Neutral styling indicating future steps
- **Purpose**: Steps not yet reached
- **MCP Context**: Pending server operations, queued processes

### 3. **Separator Variants**

#### Solid Separators (Default)

- **Use Case**: Clean, professional interfaces
- **Styling**: Solid lines connecting steps
- **Best For**: Formal workflows, production environments

#### Dotted Separators

- **Use Case**: Draft states, preview modes, informal workflows
- **Styling**: Dotted lines for visual distinction
- **Best For**: Configuration wizards, temporary states

### 4. **Indicator Size Variants**

#### Standard Size (32px)

- **Use Case**: Regular workflows, standard interfaces
- **Best For**: Most applications, balanced visual hierarchy

#### Custom Sizes

- **Use Case**: Emphasis, compact layouts, accessibility needs
- **Range**: Any CSS size value (px, rem, em, %)
- **Best For**: Specialized interfaces, responsive designs

## Props API

### Core Configuration Props

| Prop              | Type                         | Default        | Required | Description                                                     |
| ----------------- | ---------------------------- | -------------- | -------- | --------------------------------------------------------------- |
| `steps`           | `StepConfig[]`               | -              | ✅       | Array of step configurations defining the complete stepper flow |
| `orientation`     | `"horizontal" \| "vertical"` | `"horizontal"` | ❌       | Layout orientation of the stepper component                     |
| `defaultValue`    | `number`                     | `0`            | ❌       | Default active step (zero-based index) for uncontrolled mode    |
| `value`           | `number`                     | `undefined`    | ❌       | Controlled active step (zero-based index)                       |
| `onValueChange`   | `(value: number) => void`    | `undefined`    | ❌       | Callback fired when the active step changes                     |
| `borderedIcon`    | `boolean`                    | `true`         | ❌       | Whether step indicators should display borders                  |
| `indicatorSize`   | `number \| string`           | `"32px"`       | ❌       | Global indicator size applied to all steps unless overridden    |
| `dottedSeparator` | `boolean`                    | `false`        | ❌       | Whether to use dotted separators instead of solid lines         |

### Content & Behavior Props

| Prop              | Type      | Default     | Required | Description                                      |
| ----------------- | --------- | ----------- | -------- | ------------------------------------------------ |
| `showStepContent` | `boolean` | `undefined` | ❌       | Whether to display additional step content areas |

### Styling & Customization Props

| Prop               | Type     | Default | Required | Description                                           |
| ------------------ | -------- | ------- | -------- | ----------------------------------------------------- |
| `className`        | `string` | `""`    | ❌       | Additional CSS classes for the root stepper container |
| `stepClassName`    | `string` | `""`    | ❌       | CSS classes applied to individual step containers     |
| `triggerClassName` | `string` | `""`    | ❌       | CSS classes applied to step trigger/clickable areas   |
| `contentClassName` | `string` | `""`    | ❌       | CSS classes applied to step content and descriptions  |

## Type Definitions

### StepConfig Interface

```typescript
interface StepConfig extends Omit<StepperItemProps, "title"> {
  step: number; // Unique step identifier/number
  title: string | ReactNode; // Main step title (supports JSX)
  description?: ReactNode; // Optional step description (supports JSX)
  stepState?: StepState; // Current state of the step
  completed?: boolean; // Whether the step is completed
  disabled?: boolean; // Whether the step is interactive/clickable
  loading?: boolean; // Whether the step is currently loading
  descriptionStyle?: React.CSSProperties; // Custom styles for description
  stepIcon?: React.ReactNode; // Custom icon for the step
  stepText?: string; // Custom text for the step indicator
  stepIconStyle?: React.CSSProperties; // Custom styles for the step icon
  dividerColor?: string; // Custom color for the divider after this step
  indicatorSize?: number | string; // Custom indicator size for this specific step
}
```

### StepState Union Type

```typescript
type StepState =
  | "active" // Currently focused step
  | "completed" // Successfully finished step
  | "inactive" // Inactive step
  | "loading" // Step currently processing
  | "current" // Current step being executed
  | "disabled" // Unavailable step
  | "error" // Failed step
  | "upcoming"; // Future step not yet reached
```

### StepperFlowProps Interface

```typescript
interface StepperFlowProps {
  steps: StepConfig[];
  orientation?: "horizontal" | "vertical";
  defaultValue?: number;
  value?: number;
  borderedIcon?: boolean;
  onValueChange?: (value: number) => void;
  showStepContent?: boolean;
  className?: string;
  stepClassName?: string;
  triggerClassName?: string;
  contentClassName?: string;
  dottedSeparator?: boolean;
  indicatorSize?: number | string;
}
```

## Usage Examples

### 1. Basic Server Deployment Workflow

```tsx
import { StepperFlow } from "gends";
import { useState } from "react";
import { IcConfirm, IcSpinner, IcAlert } from "gends";

function ServerDeploymentFlow() {
  const [currentStep, setCurrentStep] = useState(1);

  const deploymentSteps = [
    {
      step: 0,
      title: "Code Preparation",
      description: "Preparing source code and dependencies",
      stepState: "completed" as const,
      stepIcon: <IcConfirm className="w-4 h-4" />,
    },
    {
      step: 1,
      title: "Building Application",
      description: "Compiling and packaging the application",
      stepState: "loading" as const,
      loading: true,
    },
    {
      step: 2,
      title: "Deploy to MCP",
      description: "Deploying to Contex 7 cluster",
      stepState: "upcoming" as const,
    },
    {
      step: 3,
      title: "Health Verification",
      description: "Verifying deployment health",
      stepState: "upcoming" as const,
    },
  ];

  return (
    <div className="deployment-container p-6">
      <h2 className="text-heading-xl mb-6">MCP Server Deployment</h2>
      <StepperFlow
        steps={deploymentSteps}
        value={currentStep}
        onValueChange={setCurrentStep}
        orientation="horizontal"
        className="mb-8"
      />
    </div>
  );
}
```

### 2. Vertical Configuration Wizard

```tsx
import { StepperFlow } from "gends";
import { useState } from "react";

function ConfigurationWizard() {
  const [activeStep, setActiveStep] = useState(0);

  const configSteps = [
    {
      step: 0,
      title: "Environment Setup",
      description: (
        <div className="space-y-2">
          <p>Configure your Contex 7 environment</p>
          <ul className="text-sm text-muted-foreground">
            <li>• Set environment variables</li>
            <li>• Configure API endpoints</li>
            <li>• Set up authentication</li>
          </ul>
        </div>
      ),
      stepState: "current" as const,
    },
    {
      step: 1,
      title: "Database Connection",
      description: "Establish secure database connectivity",
      stepState: "upcoming" as const,
    },
    {
      step: 2,
      title: "Service Integration",
      description: "Connect external services and APIs",
      stepState: "upcoming" as const,
    },
    {
      step: 3,
      title: "Security Configuration",
      description: "Set up security policies and permissions",
      stepState: "upcoming" as const,
    },
  ];

  return (
    <div className="config-wizard w-96">
      <StepperFlow
        steps={configSteps}
        value={activeStep}
        onValueChange={setActiveStep}
        orientation="vertical"
        showStepContent={true}
        stepClassName="pb-6"
      />
    </div>
  );
}
```

### 3. Error Handling and Recovery Flow

```tsx
import { StepperFlow } from "gends";
import { IcAlert, IcRefresh } from "gends";

function DataProcessingFlow() {
  const [retryAttempt, setRetryAttempt] = useState(0);

  const processingSteps = [
    {
      step: 0,
      title: "Data Ingestion",
      description: "Loading data from external sources",
      stepState: "completed" as const,
    },
    {
      step: 1,
      title: "Data Validation",
      description: "Validation failed - incorrect data format",
      stepState: "error" as const,
      stepIcon: <IcAlert className="w-4 h-4 text-red-500" />,
      dividerColor: "#F50031",
    },
    {
      step: 2,
      title: "Data Transformation",
      description: "Processing and transforming data",
      stepState: "disabled" as const,
      disabled: true,
    },
    {
      step: 3,
      title: "Data Export",
      description: "Exporting processed data",
      stepState: "disabled" as const,
      disabled: true,
    },
  ];

  const handleRetry = () => {
    setRetryAttempt(prev => prev + 1);
    // Implement retry logic
  };

  return (
    <div className="processing-flow">
      <StepperFlow
        steps={processingSteps}
        defaultValue={1}
        orientation="horizontal"
        className="mb-6"
      />
      <div className="flex gap-3">
        <button
          onClick={handleRetry}
          className="flex items-center gap-2 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
        >
          <IcRefresh className="w-4 h-4" />
          Retry Validation (Attempt {retryAttempt + 1})
        </button>
      </div>
    </div>
  );
}
```

### 4. Custom Icons and Styling

```tsx
import { StepperFlow } from "gends";
import { IcDatabase, IcCode, IcGlobe, IcShield } from "gends";

function CustomStyledFlow() {
  const customSteps = [
    {
      step: 0,
      title: "Database Setup",
      description: "Initialize database connections",
      stepState: "completed" as const,
      stepIcon: <IcDatabase className="w-5 h-5 text-blue-500" />,
      indicatorSize: "40px",
      dividerColor: "#10B981",
    },
    {
      step: 1,
      title: "Code Deployment",
      description: "Deploy application code",
      stepState: "current" as const,
      stepIcon: <IcCode className="w-5 h-5 text-green-500" />,
      indicatorSize: "40px",
    },
    {
      step: 2,
      title: "Public Access",
      description: "Configure public endpoints",
      stepState: "upcoming" as const,
      stepIcon: <IcGlobe className="w-5 h-5 text-purple-500" />,
      indicatorSize: "40px",
    },
    {
      step: 3,
      title: "Security Hardening",
      description: "Apply security configurations",
      stepState: "upcoming" as const,
      stepIcon: <IcShield className="w-5 h-5 text-red-500" />,
      indicatorSize: "40px",
    },
  ];

  return (
    <StepperFlow
      steps={customSteps}
      orientation="horizontal"
      borderedIcon={true}
      className="custom-stepper"
      stepClassName="px-4"
    />
  );
}
```

### 5. Dotted Separators for Draft States

```tsx
import { StepperFlow } from "gends";

function DraftWorkflow() {
  const draftSteps = [
    {
      step: 0,
      title: "Draft Preparation",
      description: "Preparing draft configuration",
      stepState: "current" as const,
    },
    {
      step: 1,
      title: "Review Process",
      description: "Pending review and approval",
      stepState: "upcoming" as const,
    },
    {
      step: 2,
      title: "Final Deployment",
      description: "Deploy to production",
      stepState: "upcoming" as const,
    },
  ];

  return (
    <div className="draft-container">
      <div className="mb-4 p-3 bg-yellow-50 border border-yellow-200 rounded">
        <p className="text-sm text-yellow-800">📝 This workflow is in draft mode</p>
      </div>
      <StepperFlow
        steps={draftSteps}
        orientation="horizontal"
        dottedSeparator={true}
        defaultValue={0}
      />
    </div>
  );
}
```

### 6. Interactive Step Navigation

```tsx
import { StepperFlow } from "gends";
import { useState } from "react";

function InteractiveWorkflow() {
  const [currentStep, setCurrentStep] = useState(0);
  const [completedSteps, setCompletedSteps] = useState<Set<number>>(new Set());

  const workflowSteps = [
    {
      step: 0,
      title: "Account Creation",
      description: "Create your MCP account",
      stepState: completedSteps.has(0)
        ? ("completed" as const)
        : currentStep === 0
          ? ("current" as const)
          : ("upcoming" as const),
    },
    {
      step: 1,
      title: "Profile Setup",
      description: "Configure your profile settings",
      stepState: completedSteps.has(1)
        ? ("completed" as const)
        : currentStep === 1
          ? ("current" as const)
          : ("upcoming" as const),
    },
    {
      step: 2,
      title: "Team Invitation",
      description: "Invite team members",
      stepState: completedSteps.has(2)
        ? ("completed" as const)
        : currentStep === 2
          ? ("current" as const)
          : ("upcoming" as const),
    },
  ];

  const handleStepComplete = () => {
    setCompletedSteps(prev => new Set([...prev, currentStep]));
    if (currentStep < workflowSteps.length - 1) {
      setCurrentStep(prev => prev + 1);
    }
  };

  const handleStepChange = (step: number) => {
    // Only allow navigation to completed steps or the next step
    if (completedSteps.has(step) || step <= Math.max(...completedSteps) + 1) {
      setCurrentStep(step);
    }
  };

  return (
    <div className="interactive-workflow">
      <StepperFlow
        steps={workflowSteps}
        value={currentStep}
        onValueChange={handleStepChange}
        orientation="horizontal"
        className="mb-6"
      />
      <div className="step-content p-6 bg-gray-50 rounded-lg">
        <h3 className="text-lg font-semibold mb-3">{workflowSteps[currentStep].title}</h3>
        <p className="text-gray-600 mb-4">{workflowSteps[currentStep].description}</p>
        <button
          onClick={handleStepComplete}
          disabled={completedSteps.has(currentStep)}
          className="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-600 disabled:opacity-50"
        >
          {completedSteps.has(currentStep) ? "Completed" : "Complete Step"}
        </button>
      </div>
    </div>
  );
}
```

## Contex 7-Specific Integration

### Theme Integration

```tsx
import { StepperFlow } from "gends";
import { useContex7Theme } from "@contex7/react";

function ThemedStepperFlow() {
  const { theme, mode } = useContex7Theme();

  return (
    <div className={`theme-${theme} mode-${mode}`}>
      <StepperFlow
        steps={steps}
        className="themed-stepper-flow"
        // Component automatically adapts to Contex 7 theme variables
      />
    </div>
  );
}
```

### Real-time State Management

```tsx
import { StepperFlow } from "gends";
import { useContex7State } from "@contex7/state";

function StateManagedStepperFlow() {
  const [workflowState, updateWorkflowState] = useContex7State("server-workflow");

  const handleStepChange = (step: number) => {
    updateWorkflowState({
      currentStep: step,
      timestamp: Date.now(),
      userId: getCurrentUserId(),
    });
  };

  return (
    <StepperFlow
      steps={workflowState.steps}
      value={workflowState.currentStep}
      onValueChange={handleStepChange}
      orientation={workflowState.orientation}
    />
  );
}
```

### Server-Side Event Integration

```tsx
import { StepperFlow } from "gends";
import { useContex7Events } from "@contex7/events";

function EventDrivenStepperFlow() {
  const { subscribe, emit } = useContex7Events();
  const [steps, setSteps] = useState(initialSteps);

  useEffect(() => {
    const unsubscribe = subscribe("workflow:step-updated", event => {
      setSteps(prevSteps =>
        prevSteps.map(step =>
          step.step === event.stepId ? { ...step, stepState: event.newState } : step
        )
      );
    });

    return unsubscribe;
  }, [subscribe]);

  const handleStepChange = (step: number) => {
    emit("workflow:step-changed", { stepId: step, timestamp: Date.now() });
  };

  return <StepperFlow steps={steps} onValueChange={handleStepChange} />;
}
```

## MCP Server Integration Guide

### 1. Server Setup Requirements

```typescript
// server/setup.ts
import { MCPServer } from "@mcp/core";
import { Contex7Plugin } from "@contex7/mcp-plugin";
import { GenesisUIPlugin } from "@gends/mcp-plugin";

const server = new MCPServer({
  plugins: [
    new Contex7Plugin({
      theme: "falcon", // or 'phoenix', 'jarvis'
      mode: "light", // or 'dark'
    }),
    new GenesisUIPlugin({
      components: ["StepperFlow"], // Explicitly enable StepperFlow
      optimizations: true,
    }),
  ],
});
```

### 2. Workflow State Management

```typescript
// workflow/manager.ts
import { WorkflowManager } from "@mcp/workflow";
import { StepState } from "gends";

export class MCPWorkflowManager extends WorkflowManager {
  async updateStepState(workflowId: string, stepId: number, state: StepState) {
    await this.updateWorkflow(workflowId, {
      [`steps.${stepId}.stepState`]: state,
      lastUpdated: new Date().toISOString(),
    });

    // Emit real-time update
    this.emit("workflow:step-updated", {
      workflowId,
      stepId,
      state,
      timestamp: Date.now(),
    });
  }

  async markStepCompleted(workflowId: string, stepId: number) {
    await this.updateStepState(workflowId, stepId, "completed");

    // Auto-advance to next step if configured
    const workflow = await this.getWorkflow(workflowId);
    if (workflow.autoAdvance && stepId < workflow.steps.length - 1) {
      await this.updateStepState(workflowId, stepId + 1, "current");
    }
  }
}
```

### 3. Environment Configuration

```bash
# .env.local
MCP_SERVER_URL=http://localhost:3001
CONTEX7_THEME_MODE=light
GENDS_OPTIMIZATION_LEVEL=high
STEPPER_FLOW_DEFAULT_ORIENTATION=horizontal
WORKFLOW_AUTO_SAVE=true
WORKFLOW_REAL_TIME_UPDATES=true
```

### 4. Build Configuration

```typescript
// vite.config.ts / webpack.config.js
export default {
  plugins: [
    // ... other plugins
    gendsOptimizer({
      components: ["StepperFlow"],
      treeShaking: true,
      cssOptimization: true,
    }),
    contex7Integration({
      themeGeneration: true,
      runtimeOptimization: true,
      workflowSupport: true,
    }),
  ],
  resolve: {
    alias: {
      "@gends/stepper": path.resolve(__dirname, "src/components/genesis/atoms/stepper"),
    },
  },
};
```

## Integration Tips for MCP Server Teams

### Performance Optimization

1. **Lazy Loading**: Use dynamic imports for StepperFlow in large applications
2. **Memoization**: Memoize step configurations to prevent unnecessary re-renders
3. **Virtual Scrolling**: For workflows with 50+ steps, consider virtualization
4. **State Batching**: Batch multiple step state updates for better performance

### Workflow Management Best Practices

1. **Step Validation**: Implement validation before allowing step progression
2. **Auto-Save**: Persist workflow state automatically
3. **Conflict Resolution**: Handle concurrent user interactions gracefully
4. **Rollback Capability**: Provide rollback mechanisms for critical workflows

### Accessibility Considerations

1. **Keyboard Navigation**: Ensure full keyboard accessibility
2. **Screen Reader Support**: Provide comprehensive ARIA labels and descriptions
3. **High Contrast**: Test with high contrast themes
4. **Focus Management**: Manage focus properly during step transitions

### Testing Integration

```typescript
// tests/stepper-flow.test.tsx
import { render, screen, fireEvent } from "@testing-library/react";
import { StepperFlow } from "gends";
import { MCPTestProvider } from "@mcp/testing";

describe("StepperFlow MCP Integration", () => {
  it("should handle step state changes", async () => {
    const mockSteps = [
      { step: 0, title: "Step 1", stepState: "current" },
      { step: 1, title: "Step 2", stepState: "upcoming" },
    ];

    const handleStepChange = jest.fn();

    render(
      <MCPTestProvider mockServer={mockMCPServer}>
        <StepperFlow
          steps={mockSteps}
          onValueChange={handleStepChange}
        />
      </MCPTestProvider>
    );

    const stepTrigger = screen.getByText("Step 2");
    fireEvent.click(stepTrigger);

    expect(handleStepChange).toHaveBeenCalledWith(1);
  });

  it("should integrate with Contex 7 themes", () => {
    render(
      <Contex7Provider theme="falcon" mode="dark">
        <StepperFlow steps={mockSteps} />
      </Contex7Provider>
    );

    const stepper = screen.getByTestId("stepper-flow");
    expect(stepper).toHaveClass("theme-falcon", "mode-dark");
  });
});
```

## Related Gends Components

- **`ProgressStepper`**: Specialized stepper with progress indicators
- **`FormStepper`**: Form-specific stepper with validation
- **`Stepper`**: Base stepper primitive components
- **`ProgressBar`**: Progress indicators and loading states
- **`Button`**: Navigation and action buttons
- **`Badge`**: Status and state indicators

## Browser Support

Compatible with all browsers supported by the Contex 7 runtime:

- **Chrome**: 88+ (full feature support)
- **Firefox**: 85+ (full feature support)
- **Safari**: 14+ (full feature support)
- **Edge**: 88+ (full feature support)
- **Mobile**: iOS 14+, Android Chrome 88+

## Troubleshooting

### Common Issues

1. **Step State Not Updating**: Ensure proper state management and re-render triggers
2. **Theme Issues**: Verify Contex 7 theme provider is wrapping the component
3. **Performance**: Use controlled mode sparingly for large step arrays
4. **Separator Alignment**: Check custom sizing doesn't break separator positioning

### Debug Mode

```tsx
// Enable debug mode for development
<StepperFlow
  steps={steps}
  className="debug-stepper-flow" // Adds debug styling
  onValueChange={step => {
    console.log("[DEBUG] StepperFlow step changed:", step);
    console.log("[DEBUG] Current steps state:", steps);
    // Your step change logic
  }}
/>
```

### Performance Monitoring

```tsx
import { useEffect } from "react";

function PerformanceMonitoredStepperFlow() {
  useEffect(() => {
    const observer = new PerformanceObserver(list => {
      list.getEntries().forEach(entry => {
        if (entry.name.includes("stepper-flow")) {
          console.log("StepperFlow performance:", entry);
        }
      });
    });

    observer.observe({ entryTypes: ["measure"] });

    return () => observer.disconnect();
  }, []);

  return <StepperFlow steps={steps} />;
}
```

## Advanced Customization

### Custom Step Indicators

```tsx
const customSteps = [
  {
    step: 0,
    title: "Custom Step",
    stepIcon: (
      <div className="w-6 h-6 rounded-full bg-gradient-to-r from-blue-500 to-purple-600 flex items-center justify-center">
        <span className="text-white text-xs font-bold">1</span>
      </div>
    ),
    indicatorSize: "40px",
  },
];
```

### Dynamic Step Generation

```tsx
function DynamicStepperFlow({ workflowConfig }) {
  const generateSteps = useCallback(() => {
    return workflowConfig.phases.map((phase, index) => ({
      step: index,
      title: phase.name,
      description: phase.description,
      stepState: phase.status,
      stepIcon: phase.icon,
      dividerColor: phase.themeColor,
    }));
  }, [workflowConfig]);

  return <StepperFlow steps={generateSteps()} orientation={workflowConfig.layout} />;
}
```

---

**Note**: This component is part of the Genesis Design System (Gends) and is optimized for MCP server architectures powered by Contex 7. For additional support, customization requests, or integration assistance, refer to the [Gends Documentation Portal](https://gends.docs.dev) or contact the MCP development team.
