# Slider Component

## Overview

The Slider component is a versatile and accessible input control that allows users to select values by dragging along a track. Built with Genesis Design System tokens and Radix UI primitives, it offers multiple variants including single value, range selection, center-based, and tick-marked sliders. The component provides extensive customization options for different use cases and maintains full accessibility support.

## Component API

### Slider Props

| Prop          | Type                                                                | Default     | Description                              |
| ------------- | ------------------------------------------------------------------- | ----------- | ---------------------------------------- |
| variant       | `"single" \| "range" \| "center" \| "ticks" \| "ticks-with-labels"` | `"single"`  | Type of slider to display                |
| size          | `"small" \| "large"`                                                | `"small"`   | Size variant of the slider               |
| showValue     | `boolean`                                                           | `true`      | Whether to show the current value input  |
| label         | `string`                                                            | `undefined` | Label text for the slider                |
| disabled      | `boolean`                                                           | `false`     | Whether the slider is disabled           |
| unit          | `SliderUnit`                                                        | `"px"`      | Unit to display with the value           |
| inputState    | `InputState`                                                        | `"default"` | State of the input field                 |
| tickCount     | `number`                                                            | `10`        | Number of tick marks (for tick variants) |
| min           | `number`                                                            | `0`         | Minimum value                            |
| max           | `number`                                                            | `100`       | Maximum value                            |
| step          | `number`                                                            | `1`         | Step increment                           |
| onChangeStart | `(value: number[]) => void`                                         | `undefined` | Callback when slider value change starts |
| onChangeEnd   | `(value: number[]) => void`                                         | `undefined` | Callback when slider value change ends   |

### Type Definitions

```typescript
type SliderUnit = "px" | "em" | "rem" | "%" | "vh" | "°";
type InputState = "default" | "success" | "error" | "warning" | "focused";
```

### Import Statement

```typescript
import { Slider } from "gends";
```

## Basic Usage

### Default Slider

```tsx
import { Slider } from "gends";

function MyComponent() {
  return (
    <div className="w-96">
      <Slider label="Brightness" min={0} max={100} step={1} />
    </div>
  );
}
```

## Variants

### Single Value Slider (default)

```tsx
<div className="w-96">
  <Slider variant="single" label="Volume" min={0} max={100} step={1} unit="%" />
</div>
```

### Range Slider

```tsx
<div className="w-96">
  <Slider
    variant="range"
    label="Price Range"
    min={0}
    max={1000}
    step={10}
    defaultValue={[200, 800]}
    unit="$"
  />
</div>
```

### Center Slider

```tsx
<div className="w-96">
  <Slider variant="center" label="Balance" min={-50} max={50} step={1} defaultValue={[0]} />
</div>
```

### Slider with Ticks

```tsx
<div className="w-96 pb-8">
  <Slider variant="ticks" label="Opacity" min={0} max={100} step={1} tickCount={10} unit="%" />
</div>
```

### Slider with Ticks and Labels

```tsx
<div className="w-96 pb-12">
  <Slider
    variant="ticks-with-labels"
    label="Quality"
    min={0}
    max={100}
    step={1}
    tickCount={11}
    unit="%"
  />
</div>
```

## Size Variants

### Small Size

```tsx
<div className="w-96">
  <Slider size="small" label="Volume" min={0} max={100} />
</div>
```

### Large Size

```tsx
<div className="w-96">
  <Slider size="large" label="Zoom" min={0} max={200} step={5} />
</div>
```

## States

### Disabled State

```tsx
<div className="w-96">
  <Slider label="Brightness" disabled defaultValue={[50]} />
</div>
```

## Real-World Usage Examples

### Color Picker Controls

```tsx
function ColorPicker() {
  const [red, setRed] = useState([255]);
  const [green, setGreen] = useState([0]);
  const [blue, setBlue] = useState([0]);

  return (
    <div className="space-y-4 w-96">
      <Slider label="Red" min={0} max={255} value={red} onValueChange={setRed} unit="" />
      <Slider label="Green" min={0} max={255} value={green} onValueChange={setGreen} unit="" />
      <Slider label="Blue" min={0} max={255} value={blue} onValueChange={setBlue} unit="" />
    </div>
  );
}
```

### Media Player Controls

```tsx
function MediaPlayer() {
  const [volume, setVolume] = useState([75]);
  const [balance, setBalance] = useState([0]);

  return (
    <div className="space-y-4 w-96">
      <Slider label="Volume" min={0} max={100} value={volume} onValueChange={setVolume} unit="%" />
      <Slider
        variant="center"
        label="Balance"
        min={-50}
        max={50}
        value={balance}
        onValueChange={setBalance}
      />
    </div>
  );
}
```

### Form Settings

```tsx
function SettingsForm() {
  const [priceRange, setPriceRange] = useState([100, 500]);
  const [rating, setRating] = useState([3]);

  return (
    <div className="space-y-4 w-96">
      <Slider
        variant="range"
        label="Price Range"
        min={0}
        max={1000}
        value={priceRange}
        onValueChange={setPriceRange}
        unit="$"
      />
      <Slider
        variant="ticks-with-labels"
        label="Minimum Rating"
        min={1}
        max={5}
        value={rating}
        onValueChange={setRating}
        tickCount={5}
        unit="⭐"
      />
    </div>
  );
}
```

### Image Editor

```tsx
function ImageEditor() {
  const [brightness, setBrightness] = useState([50]);
  const [contrast, setContrast] = useState([50]);
  const [saturation, setSaturation] = useState([50]);

  return (
    <div className="space-y-4 w-96">
      <Slider
        label="Brightness"
        min={0}
        max={100}
        value={brightness}
        onValueChange={setBrightness}
        unit="%"
      />
      <Slider
        label="Contrast"
        min={0}
        max={100}
        value={contrast}
        onValueChange={setContrast}
        unit="%"
      />
      <Slider
        label="Saturation"
        min={0}
        max={100}
        value={saturation}
        onValueChange={setSaturation}
        unit="%"
      />
    </div>
  );
}
```

## Accessibility Features

### Keyboard Navigation

- **Arrow Keys**: Increase/decrease value in small increments
- **Page Up/Down**: Increase/decrease value in large increments
- **Home/End**: Jump to minimum/maximum values
- **Focus Management**: Proper focus handling and visual indicators

### Screen Reader Support

- **ARIA Labels**: Clear identification of slider role and purpose
- **Value Announcements**: Current values announced on change
- **Range Information**: Min/max values and current position communicated

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Focus Indicators**: Clear visual feedback for keyboard users
- **Motion**: Respects reduced motion preferences

## Design System Integration

### Genesis Design Tokens

**Sizing:**

- Small Track Height: `h-[2px]`
- Large Track Height: `h-[4px]`
- Small Thumb: `h-[16px] w-[16px]`
- Large Thumb: `h-[20px] w-[20px]`

**Colors:**

- Track Background: `bg-color-neutral-grey-40`
- Range/Progress: `bg-color-primary-50`
- Thumb: `bg-color-primary-50`
- Disabled: `bg-color-neutral-grey-60`

**Interactive States:**

- Hover: `hover:after:border-color-primary-20`
- Focus: `focus-visible:ring-color-primary-70`
- Active: `active:bg-color-primary-60`

## Best Practices

### Performance

- Use controlled components when needed
- Optimize re-renders for complex forms
- Handle cleanup properly

### User Experience

- Provide clear labels and units
- Use appropriate step values
- Consider mobile touch targets
- Handle edge cases gracefully

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle validation errors

## Troubleshooting

### Common Issues

**Value Updates:**

- Check controlled vs uncontrolled patterns
- Verify onValueChange handlers
- Review defaultValue vs value props

**Styling:**

- Check custom styles
- Verify design tokens
- Review responsive behavior

**Accessibility:**

- Verify ARIA attributes
- Test keyboard navigation
- Check screen reader announcements

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Slider component provides a flexible and accessible way to handle value selection. Choose the appropriate variant and configuration based on your specific use case and requirements.
