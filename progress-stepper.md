# ProgressStepper Component Documentation

## Overview

The `ProgressStepper` component is a sophisticated stepper UI element built with **Gends** (Genesis Design System) and optimized for **MCP (Modular Component Platform)** servers powered by **Contex 7**. This component provides a visual representation of multi-step processes with real-time progress tracking, status indicators, and flexible customization options.

As part of the Gends atomic design system, ProgressStepper serves as a specialized atom-level component that integrates seamlessly with MCP server architectures, enabling developers to create intuitive workflow visualizations and process monitoring interfaces.

## Purpose in Gends-MCP-Contex7 Ecosystem

Within the **Gends-MCP-Contex7** ecosystem, the ProgressStepper component serves multiple critical functions:

### MCP Server Integration

- **Process Orchestration**: Visualize complex server workflows and task pipelines
- **Real-time Monitoring**: Track background operations, data processing, and deployment states
- **Service Health Visualization**: Display microservice startup sequences and health checks
- **Configuration Workflows**: Guide users through multi-step server configurations

### Contex 7 Compatibility

- **Theme Integration**: Fully compatible with Contex 7's theming engine and CSS variables
- **Performance Optimization**: Leverages Contex 7's rendering optimizations for smooth animations
- **State Management**: Integrates with Contex 7's state management patterns for real-time updates
- **Accessibility Standards**: Meets Contex 7's accessibility requirements out of the box

## Installation & Import

### Standard Gends Import

```typescript
import { ProgressStepper } from "gends";
```

### Alternative Import (Local Development)

```typescript
import { ProgressStepper } from "gends";
```

## Component Variants

### 1. **Orientation Variants**

#### Horizontal Layout (Default)

- **Use Case**: Main content areas, dashboard headers, workflow timelines
- **Best For**: Desktop interfaces, wide content areas
- **Responsive**: Stacks vertically on mobile devices

#### Vertical Layout

- **Use Case**: Sidebars, narrow panels, step-by-step wizards
- **Best For**: Navigation panels, compact layouts
- **Responsive**: Maintains vertical orientation across devices

### 2. **Size Variants**

#### Small (`sm`)

- **Indicator Size**: 20px diameter
- **Typography**: 14px font size
- **Use Case**: Compact UIs, dense information displays, mobile interfaces
- **Spacing**: Reduced padding and margins for space efficiency

#### Medium (`md`) - Default

- **Indicator Size**: 24px diameter
- **Typography**: 16px font size
- **Use Case**: Standard desktop interfaces, primary content areas
- **Spacing**: Standard Genesis spacing tokens

### 3. **Status Variants**

#### Success State

- **Visual**: Green checkmark icon with success-colored dividers
- **Purpose**: Completed steps, successful operations
- **MCP Context**: Completed server processes, successful deployments

#### Warning State

- **Visual**: Orange warning icon with warning-colored dividers
- **Purpose**: Steps requiring attention, non-critical issues
- **MCP Context**: Configuration warnings, performance alerts

#### Error State

- **Visual**: Red error icon with error-colored dividers
- **Purpose**: Failed steps, critical errors
- **MCP Context**: Failed deployments, system errors

#### Default/In-Progress State

- **Visual**: Circular progress indicator with customizable percentage
- **Purpose**: Active steps, ongoing processes
- **MCP Context**: Currently executing server operations

## Props API

### Core Configuration Props

| Prop                | Type                         | Default        | Required | Description                                                     |
| ------------------- | ---------------------------- | -------------- | -------- | --------------------------------------------------------------- |
| `steps`             | `ProgressStepConfig[]`       | -              | ✅       | Array of step configurations defining the complete stepper flow |
| `orientation`       | `"horizontal" \| "vertical"` | `"horizontal"` | ❌       | Layout orientation of the stepper component                     |
| `size`              | `"sm" \| "md"`               | `"md"`         | ❌       | Size variant affecting icons, typography, and spacing           |
| `defaultValue`      | `number`                     | `0`            | ❌       | Default active step (zero-based index) for uncontrolled mode    |
| `value`             | `number`                     | `undefined`    | ❌       | Controlled active step (zero-based index)                       |
| `onValueChange`     | `(value: number) => void`    | `undefined`    | ❌       | Callback fired when the active step changes                     |
| `circleStrokeWidth` | `number`                     | `2`            | ❌       | Default stroke width (px) for progress circle indicators        |

### Styling & Customization Props

| Prop               | Type     | Default | Required | Description                                           |
| ------------------ | -------- | ------- | -------- | ----------------------------------------------------- |
| `className`        | `string` | `""`    | ❌       | Additional CSS classes for the root stepper container |
| `stepClassName`    | `string` | `""`    | ❌       | CSS classes applied to individual step containers     |
| `triggerClassName` | `string` | `""`    | ❌       | CSS classes applied to step trigger/clickable areas   |
| `contentClassName` | `string` | `""`    | ❌       | CSS classes applied to step content and descriptions  |

### Advanced Behavior Props

| Prop              | Type                      | Default     | Required | Description                                      |
| ----------------- | ------------------------- | ----------- | -------- | ------------------------------------------------ |
| `showStepContent` | `boolean`                 | `undefined` | ❌       | Whether to display additional step content areas |
| `variant`         | `"default" \| "progress"` | `undefined` | ❌       | Visual variant affecting overall component style |

## Type Definitions

### ProgressStepConfig Interface

```typescript
interface ProgressStepConfig extends StepConfig {
  step: number; // Unique step identifier/number
  title: ReactNode; // Main step title (supports JSX)
  description?: ReactNode; // Optional step description (supports JSX)
  status?: ProgressType; // Current status determining visual state
  progress?: ProgressData; // Progress data for in-progress steps
  disabled?: boolean; // Whether step is interactive/clickable
}
```

### ProgressData Interface

```typescript
interface ProgressData {
  percentage: number; // Progress percentage (0-100)
  type?: ProgressType; // Visual style of progress indicator
  strokeWidth?: number; // Custom stroke width for this step's circle
}
```

### ProgressType Union

```typescript
type ProgressType = "success" | "warning" | "error" | "default";
```

### SizeType Union

```typescript
type sizeType = "sm" | "md";
```

## Usage Examples

### 1. Basic MCP Server Startup Sequence

```tsx
import { ProgressStepper } from "gends";
import { useState, useEffect } from "react";

function MCPServerStartup() {
  const [currentStep, setCurrentStep] = useState(0);

  const serverStartupSteps = [
    {
      step: 1,
      title: "Contex 7 Initialization",
      description: "Starting Contex 7 runtime environment",
      status: "success" as const,
    },
    {
      step: 2,
      title: "MCP Server Bootstrap",
      description: "Loading MCP server configurations",
      status: "default" as const,
      progress: { percentage: 85, type: "success" as const },
    },
    {
      step: 3,
      title: "Service Registration",
      description: "Registering microservices with discovery",
      status: "default" as const,
      progress: { percentage: 0, type: "default" as const },
    },
  ];

  // Simulate server startup progress
  useEffect(() => {
    const timer = setInterval(() => {
      setCurrentStep(prev => Math.min(prev + 1, serverStartupSteps.length - 1));
    }, 2000);

    return () => clearInterval(timer);
  }, []);

  return (
    <div className="p-6 bg-surface-10 rounded-lg">
      <h2 className="text-heading-xl mb-4">MCP Server Startup</h2>
      <ProgressStepper
        steps={serverStartupSteps}
        value={currentStep}
        onValueChange={setCurrentStep}
        orientation="horizontal"
        size="md"
      />
    </div>
  );
}
```

### 2. Deployment Pipeline with Real-time Updates

```tsx
import { ProgressStepper } from "gends";
import { useMCPDeployment } from "@/hooks/useMCPDeployment";

function DeploymentPipeline() {
  const { deploymentState, currentStep } = useMCPDeployment();

  const deploymentSteps = [
    {
      step: 1,
      title: "Code Validation",
      description: "Running linting and type checks",
      status: deploymentState.validation,
    },
    {
      step: 2,
      title: "Build & Package",
      description: "Compiling and bundling application",
      status: deploymentState.build === "in_progress" ? "default" : deploymentState.build,
      progress:
        deploymentState.build === "in_progress"
          ? { percentage: deploymentState.buildProgress, type: "success" }
          : undefined,
    },
    {
      step: 3,
      title: "Deploy to Contex 7",
      description: "Deploying to production cluster",
      status: deploymentState.deploy,
      progress:
        deploymentState.deploy === "default" ? { percentage: 0, type: "default" } : undefined,
    },
  ];

  return (
    <div className="deployment-pipeline">
      <ProgressStepper
        steps={deploymentSteps}
        value={currentStep}
        orientation="vertical"
        size="sm"
        className="w-80"
        stepClassName="py-3"
      />
    </div>
  );
}
```

### 3. Responsive Configuration Wizard

```tsx
import { ProgressStepper } from "gends";
import { useBreakpoint } from "@/hooks/useBreakpoint";

function ConfigurationWizard() {
  const { isMobile } = useBreakpoint();
  const [activeStep, setActiveStep] = useState(0);

  const configSteps = [
    {
      step: 1,
      title: "Environment Setup",
      description: "Configure Contex 7 environment variables",
      status: "success" as const,
    },
    {
      step: 2,
      title: "Database Connection",
      description: "Establish database connectivity",
      status: "default" as const,
      progress: { percentage: 60, type: "success" as const },
    },
    {
      step: 3,
      title: "Security Configuration",
      description: "Set up authentication and authorization",
      status: "default" as const,
      progress: { percentage: 0, type: "default" as const },
    },
  ];

  return (
    <div className="config-wizard">
      <ProgressStepper
        steps={configSteps}
        value={activeStep}
        onValueChange={setActiveStep}
        orientation={isMobile ? "vertical" : "horizontal"}
        size={isMobile ? "sm" : "md"}
        className={isMobile ? "w-full" : "max-w-4xl mx-auto"}
      />
    </div>
  );
}
```

### 4. Error Handling and Recovery

```tsx
import { ProgressStepper } from "gends";

function DataProcessingPipeline() {
  const processingSteps = [
    {
      step: 1,
      title: "Data Ingestion",
      description: "Loading data from external sources",
      status: "success" as const,
    },
    {
      step: 2,
      title: "Data Transformation",
      description: "Processing failed - validation error",
      status: "error" as const,
    },
    {
      step: 3,
      title: "Data Export",
      description: "Export to destination systems",
      status: "default" as const,
      progress: { percentage: 0, type: "default" as const },
      disabled: true, // Disabled due to previous error
    },
  ];

  const handleRetry = () => {
    // Implement retry logic for failed step
    console.log("Retrying failed step...");
  };

  return (
    <div className="processing-pipeline">
      <ProgressStepper steps={processingSteps} defaultValue={1} size="md" />
      <div className="mt-4 flex gap-2">
        <button onClick={handleRetry} className="btn-primary">
          Retry Failed Step
        </button>
      </div>
    </div>
  );
}
```

### 5. Custom Stroke Widths for Visual Emphasis

```tsx
import { ProgressStepper } from "gends";

function PriorityBasedProcessing() {
  const prioritySteps = [
    {
      step: 1,
      title: "High Priority Task",
      description: "Critical system operation",
      status: "default" as const,
      progress: {
        percentage: 90,
        type: "success" as const,
        strokeWidth: 3, // Thick stroke for high priority
      },
    },
    {
      step: 2,
      title: "Medium Priority Task",
      description: "Standard processing operation",
      status: "default" as const,
      progress: {
        percentage: 45,
        type: "success" as const,
        strokeWidth: 2, // Standard stroke
      },
    },
    {
      step: 3,
      title: "Low Priority Task",
      description: "Background maintenance task",
      status: "default" as const,
      progress: {
        percentage: 15,
        type: "warning" as const,
        strokeWidth: 1, // Thin stroke for low priority
      },
    },
  ];

  return (
    <ProgressStepper
      steps={prioritySteps}
      defaultValue={0}
      circleStrokeWidth={2} // Default stroke width
      orientation="horizontal"
      size="md"
    />
  );
}
```

## Contex 7-Specific Integration

### Theme Integration

```tsx
import { ProgressStepper } from "gends";

function ThemedProgressStepper() {
  const { theme, mode } = useContex7Theme();

  return (
    <div className={`theme-${theme} mode-${mode}`}>
      <ProgressStepper
        steps={steps}
        className="themed-stepper"
        // Component automatically adapts to Contex 7 theme variables
      />
    </div>
  );
}
```

### State Management Integration

```tsx
import { ProgressStepper } from "gends";

function StateManagedStepper() {
  const [processState, updateProcessState] = useContex7State("deployment-process");

  const handleStepChange = (step: number) => {
    updateProcessState({ currentStep: step, timestamp: Date.now() });
  };

  return (
    <ProgressStepper
      steps={processState.steps}
      value={processState.currentStep}
      onValueChange={handleStepChange}
    />
  );
}
```

### Real-time Updates with Contex 7 Streams

```tsx
import { ProgressStepper } from "gends";

function RealtimeProcessMonitor() {
  const processData = useContex7Stream("server-process-updates");

  return (
    <ProgressStepper
      steps={processData.steps}
      value={processData.currentStep}
      // Automatically updates when stream receives new data
    />
  );
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
      components: ["ProgressStepper"], // Explicitly enable ProgressStepper
      optimizations: true,
    }),
  ],
});
```

### 2. Component Registration

```typescript
// client/app.tsx
import { MCPProvider } from '@mcp/react';
import { Contex7Provider } from '@contex7/react';
import { GenesisProvider } from 'gends';

function App() {
  return (
    <MCPProvider server={mcpServer}>
      <Contex7Provider>
        <GenesisProvider>
          {/* Your app components using ProgressStepper */}
          <ProcessDashboard />
        </GenesisProvider>
      </Contex7Provider>
    </MCPProvider>
  );
}
```

### 3. Environment Configuration

```bash
# .env.local
MCP_SERVER_URL=http://localhost:3001
CONTEX7_THEME_MODE=light
GENDS_OPTIMIZATION_LEVEL=high
PROGRESS_STEPPER_DEFAULT_SIZE=md
```

### 4. Build Configuration

```typescript
// vite.config.ts / webpack.config.js
export default {
  plugins: [
    // ... other plugins
    gendsOptimizer({
      components: ["ProgressStepper"],
      treeShaking: true,
      cssOptimization: true,
    }),
    contex7Integration({
      themeGeneration: true,
      runtimeOptimization: true,
    }),
  ],
};
```

## Integration Tips for MCP Server Teams

### Performance Optimization

1. **Lazy Loading**: Use dynamic imports for ProgressStepper in large applications
2. **Memoization**: Wrap step configurations in `useMemo` for complex step arrays
3. **Debouncing**: Debounce `onValueChange` callbacks for rapid state updates
4. **Virtual Scrolling**: Consider virtualization for steppers with 20+ steps

### State Management Best Practices

1. **Controlled vs Uncontrolled**: Use controlled mode for server-synced state
2. **Step Validation**: Implement step validation before allowing progression
3. **Error Recovery**: Provide clear error recovery mechanisms for failed steps
4. **Persistence**: Persist stepper state across browser sessions when appropriate

### Accessibility Considerations

1. **Screen Readers**: Ensure step descriptions are comprehensive
2. **Keyboard Navigation**: Test full keyboard navigation flows
3. **Focus Management**: Manage focus properly when steps change
4. **High Contrast**: Test with high contrast mode enabled

### Testing Integration

```typescript
// tests/progress-stepper.test.tsx
import { render, screen } from '@testing-library/react';
import { ProgressStepper } from 'gends';
import { MCPTestProvider } from '@mcp/testing';

describe('ProgressStepper MCP Integration', () => {
  it('should integrate with MCP server state', async () => {
    render(
      <MCPTestProvider mockServer={mockMCPServer}>
        <ProgressStepper steps={testSteps} />
      </MCPTestProvider>
    );

    // Test MCP-specific functionality
    expect(screen.getByRole('progressbar')).toBeInTheDocument();
  });
});
```

## Related Gends Components

- **`StepperFlow`**: Base stepper functionality and flow control
- **`ProgressBar`**: Circular and linear progress indicators
- **`Badge`**: Status and notification badges
- **`Button`**: Navigation and action buttons
- **`Toast`**: Success/error notifications for step completion

## Browser Support

Compatible with all browsers supported by the Contex 7 runtime:

- **Chrome**: 88+ (full feature support)
- **Firefox**: 85+ (full feature support)
- **Safari**: 14+ (full feature support)
- **Edge**: 88+ (full feature support)
- **Mobile**: iOS 14+, Android Chrome 88+

## Troubleshooting

### Common Issues

1. **Import Errors**: Ensure Gends is properly installed and configured
2. **Theme Issues**: Verify Contex 7 theme provider is wrapping the component
3. **Performance**: Use controlled mode sparingly for large step arrays
4. **Styling**: Check that Genesis CSS variables are loaded correctly

### Debug Mode

```tsx
// Enable debug mode for development
<ProgressStepper
  steps={steps}
  className="debug-stepper" // Adds debug styling
  onValueChange={step => {
    console.log("[DEBUG] Step changed:", step);
    // Your step change logic
  }}
/>
```

---

**Note**: This component is part of the Genesis Design System (Gends) and is optimized for MCP server architectures powered by Contex 7. For additional support, customization requests, or integration assistance, refer to the [Gends Documentation Portal](https://gends.docs.dev) or contact the MCP development team.
