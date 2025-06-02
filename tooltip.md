# Tooltip

A flexible tooltip component built on Radix UI that provides contextual information or hints when hovering over or focusing on an element—with support for custom positioning, animations, and styling.

---

## 1. Quick start

```tsx
import { Tooltip, TooltipTrigger, TooltipContent, TooltipProvider } from "gends";

function Example() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger>Hover me</TooltipTrigger>
        <TooltipContent>Tooltip content</TooltipContent>
      </Tooltip>
    </TooltipProvider>
  );
}
```

Wrap your app with `TooltipProvider` once, then compose tooltip elements as needed.

---

## 2. Positioning

The tooltip can be positioned relative to its trigger in various ways:

| Position | Description      | Use Case                    |
| -------- | ---------------- | --------------------------- |
| `top`    | Above trigger    | Default position            |
| `bottom` | Below trigger    | When space above is limited |
| `left`   | Left of trigger  | For right-aligned content   |
| `right`  | Right of trigger | For left-aligned content    |

```tsx
<Tooltip>
  <TooltipTrigger>Hover me</TooltipTrigger>
  <TooltipContent side="top" align="center">
    Top tooltip
  </TooltipContent>
</Tooltip>
```

---

## 3. Animations

Built-in animations for smooth transitions:

- Fade in/out
- Zoom in/out
- Slide from direction
- State-based animations

```tsx
// Default animations applied:
// - fade-in-0 / fade-out-0
// - zoom-in-95 / zoom-out-95
// - slide-in-from-{direction}-2
```

---

## 4. Customization

### Custom Styling

```tsx
<TooltipContent className="bg-primary text-white p-4">Custom styled tooltip</TooltipContent>
```

### With Arrow

```tsx
<Tooltip>
  <TooltipTrigger>With Arrow</TooltipTrigger>
  <TooltipContent>
    Tooltip content
    <TooltipArrow />
  </TooltipContent>
</Tooltip>
```

### Custom Offset

```tsx
<TooltipContent sideOffset={8}>Offset from trigger</TooltipContent>
```

---

## 5. Full prop reference

### TooltipProvider

| Prop                      | Type      | Default | Description                                      |
| ------------------------- | --------- | ------- | ------------------------------------------------ |
| `delayDuration`           | `number`  | `700`   | Hover delay before showing                       |
| `skipDelayDuration`       | `number`  | `300`   | Skip delay if another tooltip was shown recently |
| `disableHoverableContent` | `boolean` | `false` | Disable hover on content                         |

### TooltipContent

| Prop              | Type                                     | Default    | Description               |
| ----------------- | ---------------------------------------- | ---------- | ------------------------- |
| `side`            | `'top' \| 'right' \| 'bottom' \| 'left'` | `'top'`    | Placement side            |
| `sideOffset`      | `number`                                 | `4`        | Offset from trigger       |
| `align`           | `'start' \| 'center' \| 'end'`           | `'center'` | Alignment on side         |
| `alignOffset`     | `number`                                 | -          | Alignment offset          |
| `avoidCollisions` | `boolean`                                | `true`     | Avoid viewport collisions |
| `className`       | `string`                                 | -          | Custom classes            |

---

## 6. Recipes

### Info Icon with Tooltip

```tsx
function InfoTooltip({ content }: { content: string }) {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger>
          <InfoIcon className="w-4 h-4" />
        </TooltipTrigger>
        <TooltipContent>{content}</TooltipContent>
      </Tooltip>
    </TooltipProvider>
  );
}
```

### Form Field Helper

```tsx
function FormField() {
  return (
    <div className="field">
      <label>
        Username
        <Tooltip>
          <TooltipTrigger>
            <QuestionIcon className="ml-1" />
          </TooltipTrigger>
          <TooltipContent>Choose a unique username that will identify you</TooltipContent>
        </Tooltip>
      </label>
      <input type="text" />
    </div>
  );
}
```

### Interactive Content

```tsx
function ActionTooltip() {
  return (
    <Tooltip>
      <TooltipTrigger>Actions</TooltipTrigger>
      <TooltipContent>
        <div className="flex flex-col gap-2">
          <button>Edit</button>
          <button>Delete</button>
        </div>
      </TooltipContent>
    </Tooltip>
  );
}
```

---

## 7. Accessibility considerations

- Uses ARIA attributes automatically
- Keyboard navigation support
- Screen reader announcements
- Focus management
- Hover and focus triggers

```tsx
// Automatically handles:
// - aria-describedby
// - role="tooltip"
// - Focus management
// - Keyboard interactions
```

---

## 8. Design patterns

### Placement Patterns

- Consider available space
- Avoid viewport collisions
- Maintain readability
- Consistent positioning

### Content Patterns

- Keep content concise
- Use clear language
- Maintain readability
- Consider mobile touch targets

### Interaction Patterns

- Appropriate delay duration
- Smooth animations
- Clear hover states
- Touch device support

---
