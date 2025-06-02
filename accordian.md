# Accordion

A vertically stacked set of interactive headings that each reveal an associated section of content. Built on top of Radix UI's Accordion primitive, this component provides a fully accessible and customizable accordion interface.

---

## 1. Quick start

```tsx
import { Accordion, AccordionItem, AccordionTrigger, AccordionContent } from "gends";

function Example() {
  return (
    <Accordion type="single" collapsible>
      <AccordionItem value="item-1">
        <AccordionTrigger>Is it accessible?</AccordionTrigger>
        <AccordionContent>Yes. It adheres to the WAI-ARIA Accordion Pattern.</AccordionContent>
      </AccordionItem>
    </Accordion>
  );
}
```

---

## 2. Types

The Accordion component supports two types of behavior:

| Type       | Description                               | Use case                   |
| ---------- | ----------------------------------------- | -------------------------- |
| `single`   | Only one item can be open at a time       | FAQ sections, simple lists |
| `multiple` | Multiple items can be open simultaneously | Complex documentation      |

```tsx
// Single item open at a time
<Accordion type="single" collapsible>
  {/* ... items ... */}
</Accordion>

// Multiple items can be open
<Accordion type="multiple">
  {/* ... items ... */}
</Accordion>
```

---

## 3. Collapsible Behavior

The `collapsible` prop determines whether all items can be closed:

```tsx
// All items can be closed
<Accordion type="single" collapsible>
  {/* ... items ... */}
</Accordion>

// At least one item must be open
<Accordion type="single">
  {/* ... items ... */}
</Accordion>
```

---

## 4. Default Value

Set which items are open by default:

```tsx
// Single type with default value
<Accordion type="single" defaultValue="item-1">
  <AccordionItem value="item-1">
    <AccordionTrigger>First Item</AccordionTrigger>
    <AccordionContent>Content 1</AccordionContent>
  </AccordionItem>
</Accordion>

// Multiple type with default values
<Accordion type="multiple" defaultValue={["item-1", "item-2"]}>
  <AccordionItem value="item-1">
    <AccordionTrigger>First Item</AccordionTrigger>
    <AccordionContent>Content 1</AccordionContent>
  </AccordionItem>
  <AccordionItem value="item-2">
    <AccordionTrigger>Second Item</AccordionTrigger>
    <AccordionContent>Content 2</AccordionContent>
  </AccordionItem>
</Accordion>
```

---

## 5. Controlled State

Manage the open state programmatically:

```tsx
const [value, setValue] = useState<string | string[]>("item-1");

<Accordion type="single" value={value} onValueChange={setValue}>
  <AccordionItem value="item-1">
    <AccordionTrigger>First Item</AccordionTrigger>
    <AccordionContent>Content 1</AccordionContent>
  </AccordionItem>
</Accordion>;
```

---

## 6. Custom Styling

Apply custom styles to each part of the accordion:

```tsx
// Custom item styling
<AccordionItem className="border-2 border-blue-500">
  <AccordionTrigger className="text-blue-500">Custom Styled Trigger</AccordionTrigger>
  <AccordionContent className="bg-gray-50">Custom styled content</AccordionContent>
</AccordionItem>
```

---

## 7. Full Prop Reference

### Accordion Root

| Prop            | Type                                  | Default    | Description                                     |
| --------------- | ------------------------------------- | ---------- | ----------------------------------------------- |
| `type`          | `'single' \| 'multiple'`              | `'single'` | Determines if one or multiple items can be open |
| `collapsible`   | `boolean`                             | `false`    | Whether all items can be closed                 |
| `defaultValue`  | `string \| string[]`                  | -          | The value of the item(s) to open by default     |
| `value`         | `string \| string[]`                  | -          | The controlled value of the item(s) to open     |
| `onValueChange` | `(value: string \| string[]) => void` | -          | Callback fired when the value changes           |
| `className`     | `string`                              | -          | Additional CSS classes                          |

### AccordionItem

| Prop        | Type     | Default | Description               |
| ----------- | -------- | ------- | ------------------------- |
| `value`     | `string` | -       | Unique value for the item |
| `className` | `string` | -       | Additional CSS classes    |

### AccordionTrigger

| Prop        | Type     | Default | Description            |
| ----------- | -------- | ------- | ---------------------- |
| `className` | `string` | -       | Additional CSS classes |

### AccordionContent

| Prop        | Type     | Default | Description            |
| ----------- | -------- | ------- | ---------------------- |
| `className` | `string` | -       | Additional CSS classes |

---

## 8. Recipes

### FAQ Section

```tsx
<Accordion type="single" collapsible>
  <AccordionItem value="faq-1">
    <AccordionTrigger>What is GenDS?</AccordionTrigger>
    <AccordionContent>
      GenDS is a comprehensive design system that provides accessible and customizable components.
    </AccordionContent>
  </AccordionItem>
  <AccordionItem value="faq-2">
    <AccordionTrigger>How do I get started?</AccordionTrigger>
    <AccordionContent>Install the package and import the components you need.</AccordionContent>
  </AccordionItem>
</Accordion>
```

### Documentation Navigation

```tsx
<Accordion type="multiple" defaultValue={["getting-started"]}>
  <AccordionItem value="getting-started">
    <AccordionTrigger>Getting Started</AccordionTrigger>
    <AccordionContent>
      <ul className="space-y-2">
        <li>Installation</li>
        <li>Basic Usage</li>
        <li>Configuration</li>
      </ul>
    </AccordionContent>
  </AccordionItem>
  <AccordionItem value="components">
    <AccordionTrigger>Components</AccordionTrigger>
    <AccordionContent>
      <ul className="space-y-2">
        <li>Button</li>
        <li>Input</li>
        <li>Select</li>
      </ul>
    </AccordionContent>
  </AccordionItem>
</Accordion>
```

### Nested Accordions

```tsx
<Accordion type="single" collapsible>
  <AccordionItem value="parent-1">
    <AccordionTrigger>Parent Section</AccordionTrigger>
    <AccordionContent>
      <Accordion type="single" collapsible>
        <AccordionItem value="child-1">
          <AccordionTrigger>Child Section 1</AccordionTrigger>
          <AccordionContent>Nested content 1</AccordionContent>
        </AccordionItem>
        <AccordionItem value="child-2">
          <AccordionTrigger>Child Section 2</AccordionTrigger>
          <AccordionContent>Nested content 2</AccordionContent>
        </AccordionItem>
      </Accordion>
    </AccordionContent>
  </AccordionItem>
</Accordion>
```

---

## 9. Accessibility

The Accordion component follows WAI-ARIA Accordion Pattern guidelines:

- Proper ARIA attributes for expanded/collapsed states
- Keyboard navigation support:
  - Tab: Move focus between accordion headers
  - Enter/Space: Toggle the focused section
  - Arrow keys: Navigate between headers
- Focus management with visible focus indicators
- Screen reader announcements for state changes

---

## 10. Design Tokens

The Accordion component uses the following design system tokens:

**Spacing:**

- Padding: `py-4` (vertical padding for triggers)
- Content padding: `pb-4 pt-0`

**Typography:**

- Font weight: `font-medium` for triggers
- Text size: `text-sm` for content

**Colors:**

- Border color: Default border color for items
- Text color: Inherited from parent

**Transitions:**

- Duration: `duration-200` for smooth animations
- Transform: `rotate-180` for chevron icon

**Animations:**

- `animate-accordion-up`: Collapse animation
- `animate-accordion-down`: Expand animation

---

Consider using Accordion with:

- **Typography** — For consistent text styling
- **Icons** — For visual indicators
- **Card** — For contained sections
- **Navigation** — For collapsible menus
- **Form** — For collapsible form sections
