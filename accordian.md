# Accordion Component

## Overview

The Accordion component is a collapsible content container that allows users to show and hide sections of related content. It supports both single and multiple selection modes, custom icons, dividers, and flexible content rendering.

## Component API

### Props

| Prop            | Type                           | Default     | Description                                                                                |
| --------------- | ------------------------------ | ----------- | ------------------------------------------------------------------------------------------ |
| `items`         | `AccordionItem[]`              | `[]`        | Array of accordion items to render                                                         |
| `size`          | `"xs" \| "sm" \| "md" \| "lg"` | `"md"`      | Size variant of the accordion                                                              |
| `type`          | `"single" \| "multiple"`       | `"single"`  | Selection behavior - single allows only one item open, multiple allows multiple items open |
| `topDivider`    | `boolean`                      | `false`     | Show divider above the accordion                                                           |
| `bottomDivider` | `boolean`                      | `false`     | Show divider below the accordion                                                           |
| `header`        | `boolean`                      | `false`     | Whether this is a header accordion or list accordion                                       |
| `defaultValue`  | `string \| string[]`           | `undefined` | Default expanded item(s) - string for single type, array for multiple type                 |
| `width`         | `string`                       | `undefined` | Custom width for the accordion container                                                   |

### AccordionItem Interface

```typescript
interface AccordionItem {
  label: React.ReactNode; // The header text or element
  content: React.ReactNode; // The collapsible content
  value: string; // Unique identifier for the item
  icon?: React.ReactNode; // Optional icon to display
  showIcon?: boolean; // Whether to show the icon (defaults to true if icon provided)
  bold?: boolean; // Whether to make the label bold
}
```

## Variants

### Basic List Accordion

The default list-style accordion with standard behavior.

```tsx
import { Accordion } from "gends";
import { IcFavorite } from "gends";

<Accordion
  items={[
    {
      label: "First Accordion Item",
      content: "Content of the first accordion item",
      value: "item-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
    {
      label: "Second Accordion Item",
      content: "Content of the second accordion item",
      value: "item-2",
      icon: <IcFavorite className="h-full w-full" />,
    },
  ]}
  bottomDivider={true}
/>;
```

### Multiple Selection Accordion

Allows multiple accordion items to be expanded simultaneously.

```tsx
<Accordion
  type="multiple"
  items={[
    {
      label: "First Item",
      content: "Content of the first item",
      value: "item-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
    {
      label: "Second Item",
      content: "Content of the second item",
      value: "item-2",
      icon: <IcInfo className="h-full w-full" />,
    },
    {
      label: "Third Item",
      content: "Content of the third item",
      value: "item-3",
      icon: <IcFavorite className="h-full w-full" />,
    },
  ]}
  defaultValue={["item-1", "item-3"]}
  bottomDivider={true}
/>
```

### Header Style Accordion

A header-style accordion for top-level navigation or section grouping.

```tsx
<Accordion
  header={true}
  items={[
    {
      label: "Header Accordion",
      content: "Content of the header accordion",
      value: "header-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
  ]}
/>
```

### Custom Icons and Mixed Configurations

Accordion with different icon types, including avatars and custom elements.

```tsx
import { Avatar } from "gends";
import { IcFavorite, IcInfo } from "gends";

<Accordion
  items={[
    {
      label: "Item with Icon",
      content: "This item has an icon",
      value: "item-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
    {
      label: "Item without Icon",
      content: "This item has no icon",
      value: "item-2",
      showIcon: false,
    },
    {
      label: "Item with Different Icon",
      content: "This item has a different icon",
      value: "item-3",
      icon: <IcInfo className="h-full w-full" />,
    },
    {
      label: "Item with Avatar Prefix",
      content: "This item has an avatar prefix",
      value: "item-4",
      icon: <Avatar initials="WW" size="xs" />,
    },
  ]}
  bottomDivider={true}
/>;
```

### Bold and Regular Label Mix

Accordion with mixed label styling for emphasis.

```tsx
<Accordion
  items={[
    {
      label: "Regular Label",
      content: "Content with regular label",
      value: "item-1",
      bold: false,
      icon: <IcFavorite className="h-full w-full" />,
    },
    {
      label: "Bold Label",
      content: "Content with bold label",
      value: "item-2",
      bold: true,
      icon: <IcFavorite className="h-full w-full" />,
    },
  ]}
  bottomDivider={true}
/>
```

### Custom Content

Accordion with rich content including components and styled elements.

```tsx
import { Slot } from "gends";
import { Badge } from "gends";

<Accordion
  items={[
    {
      label: "Item with Slot",
      content: <Slot />,
      value: "item-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
    {
      label: <span className="text-color-primary-40">Item with Coloured Text</span>,
      content: <span className="text-color-feedback-success-50">This item has green colour</span>,
      value: "item-2",
      showIcon: false,
    },
    {
      label: "Item with Badge",
      content: <Badge />,
      value: "item-3",
      icon: <IcInfo className="h-full w-full" />,
    },
  ]}
  bottomDivider={true}
/>;
```

### Divider Configurations

#### Top Divider Only

```tsx
<Accordion
  topDivider={true}
  items={[
    {
      label: "First Item with Top Divider",
      content: "Content of the first item",
      value: "item-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
  ]}
/>
```

#### Both Dividers (Header Style)

```tsx
<Accordion
  header={true}
  topDivider={true}
  bottomDivider={true}
  items={[
    {
      label: "Header with Both Dividers",
      content: "Content with both dividers",
      value: "item-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
  ]}
/>
```

#### No Dividers

```tsx
<Accordion
  bottomDivider={false}
  items={[
    {
      label: "Item Without Bottom Divider",
      content: "Content without bottom divider",
      value: "item-1",
      icon: <IcFavorite className="h-full w-full" />,
    },
  ]}
/>
```

### Size Variants

The accordion supports four size variants:

```tsx
// Extra Small
<Accordion size="xs" items={accordionItems} />

// Small
<Accordion size="sm" items={accordionItems} />

// Medium (Default)
<Accordion size="md" items={accordionItems} />

// Large
<Accordion size="lg" items={accordionItems} />
```

### Custom Width

Control the accordion container width:

```tsx
<Accordion width="600px" items={accordionItems} bottomDivider={true} />
```

### Header Without Icon

Header-style accordion without icon display:

```tsx
<Accordion
  header={true}
  items={[
    {
      label: "Header Without Icon",
      content: "Content of the header without icon",
      value: "header-1",
      showIcon: false,
    },
  ]}
/>
```

## Accessibility Features

- **Keyboard Navigation**: Full keyboard support with Arrow keys, Enter, and Space
- **ARIA Attributes**: Proper ARIA labeling for screen readers
- **Focus Management**: Clear focus indicators and logical tab order
- **Screen Reader Support**: Announces expanded/collapsed states

## Best Practices

### Content Organization

- Use descriptive labels that clearly indicate the content within
- Keep content sections focused and related
- Consider the logical hierarchy when nesting accordions

### Performance

- For large content sections, consider lazy loading heavy components
- Use the `multiple` type sparingly to avoid overwhelming users
- Keep the number of accordion items reasonable (typically < 10)

### UX Guidelines

- Use `header={true}` for main section headers
- Use `header={false}` for detailed item lists
- Include dividers when visual separation is needed
- Use icons consistently across related accordion items
- Consider using bold labels for emphasis on important items

### Default States

- Set appropriate `defaultValue` for improved UX
- For single-type accordions, consider having one item open by default
- For multiple-type accordions, be selective about which items open by default

## Integration Examples

### Form Sections

```tsx
<Accordion
  header={true}
  items={[
    {
      label: "Personal Information",
      content: <PersonalInfoForm />,
      value: "personal",
    },
    {
      label: "Contact Details",
      content: <ContactForm />,
      value: "contact",
    },
  ]}
  defaultValue="personal"
/>
```

### FAQ Section

```tsx
<Accordion
  type="single"
  items={faqs.map(faq => ({
    label: faq.question,
    content: faq.answer,
    value: faq.id,
    showIcon: false,
  }))}
  bottomDivider={true}
/>
```

### Navigation Menu

```tsx
<Accordion
  header={true}
  type="single"
  items={[
    {
      label: "Products",
      content: <ProductSubmenu />,
      value: "products",
      icon: <IcProducts className="h-full w-full" />,
    },
    {
      label: "Services",
      content: <ServicesSubmenu />,
      value: "services",
      icon: <IcServices className="h-full w-full" />,
    },
  ]}
/>
```

## Technical Notes

- The component uses controlled state management for expansion/collapse
- Icons are rendered with `h-full w-full` classes for proper sizing
- Content can be any React node, including complex components
- The `value` prop must be unique for each accordion item
- Dividers are styled consistently with the Genesis design system
- The component is fully responsive and works across all device sizes
