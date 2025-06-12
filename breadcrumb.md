# Breadcrumb Component Documentation

## Overview

The Breadcrumb component provides navigation that shows the current page's location within a navigational hierarchy. It supports automatic collapsing for long paths, custom icons, and various styling options.

## Import

```typescript
import { Breadcrumb } from "gends";
```

## Basic Usage

```typescript
<Breadcrumb
  items={[
    { label: "Home", href: "#" },
    { label: "Documents", href: "#" },
    { label: "Document.pdf" },
  ]}
/>
```

## Props

### BreadcrumbProps

| Prop                 | Type                                                                        | Default              | Description                                                |
| -------------------- | --------------------------------------------------------------------------- | -------------------- | ---------------------------------------------------------- |
| `items`              | `BreadcrumbItem[]`                                                          | **Required**         | Array of breadcrumb items                                  |
| `maxItems`           | `number`                                                                    | `4`                  | Maximum number of items to show before collapsing          |
| `separator`          | `React.ReactNode`                                                           | `<IcChevronRight />` | Custom separator between items                             |
| `ellipsisComponent`  | `React.ReactNode`                                                           | -                    | Custom ellipsis component for collapsed items              |
| `renderItem`         | `(item: BreadcrumbItem, index: number, isLast: boolean) => React.ReactNode` | -                    | Custom item renderer                                       |
| `linkComponent`      | `React.ElementType`                                                         | -                    | Custom link component (e.g., Next.js Link)                 |
| `itemClassName`      | `string`                                                                    | `""`                 | Additional CSS classes for items                           |
| `separatorClassName` | `string`                                                                    | `""`                 | Additional CSS classes for separators                      |
| `ellipsisClassName`  | `string`                                                                    | `""`                 | Additional CSS classes for ellipsis                        |
| `testIdPrefix`       | `string`                                                                    | `"breadcrumb"`       | Prefix for test IDs                                        |
| `collapseAfter`      | `number`                                                                    | -                    | Number of items to show after first item before collapsing |
| `className`          | `string`                                                                    | `""`                 | Additional CSS classes for container                       |

### BreadcrumbItem

| Property          | Type                                                   | Description                           |
| ----------------- | ------------------------------------------------------ | ------------------------------------- |
| `label`           | `React.ReactNode`                                      | Display text or content               |
| `href`            | `string`                                               | Link URL (optional)                   |
| `isCurrent`       | `boolean`                                              | Whether this is the current page      |
| `isHome`          | `boolean`                                              | Whether this is the home item         |
| `icon`            | `React.ReactNode`                                      | Custom icon                           |
| `showDefaultIcon` | `boolean`                                              | Show default home icon for first item |
| `onClick`         | `(event: React.MouseEvent<HTMLAnchorElement>) => void` | Click handler                         |
| `className`       | `string`                                               | Additional CSS classes                |
| `testId`          | `string`                                               | Custom test ID                        |

## Variants and Examples

### 1. Basic Breadcrumb

Simple breadcrumb with text labels:

```typescript
<Breadcrumb
  items={[
    { label: "Home", href: "#" },
    { label: "Documents", href: "#" },
    { label: "Document.pdf" },
  ]}
/>
```

### 2. Long Path with Auto-Collapse

Breadcrumb that automatically collapses when items exceed `maxItems`:

```typescript
const sampleItems = [
  { label: "Home", href: "#", icon: <IcHome className="h-4 w-4 mr-1" /> },
  { label: "Category", href: "#" },
  { label: "Subcategory", href: "#" },
  { label: "Type", href: "#" },
  { label: "Brand", href: "#" },
  { label: "Model", href: "#" },
  { label: "Current Page" },
];

<Breadcrumb
  items={sampleItems}
  ellipsisComponent={
    <SelectorDropdown
      options={sampleItems.slice(1, -2).map((item, idx) => (
        <div key={idx}>{item.label}</div>
      ))}
      placeholder="More"
      showIcon
      size="md"
      className="!bg-transparent !p-0 !shadow-none"
      onChange={value => {
        console.log("Selected breadcrumb", value);
      }}
    >
      <div>
        <IconButton
          appearance="default"
          icon={<IcMoreHorizontal />}
          inverse
          size="sm"
          type="tertiary"
          style={{ color: "#000" }}
          classNames={{
            button: "hover:bg-transparent focus:bg-transparent active:bg-transparent shadow-none text-color-neutral-black",
            icon: "text-color-neutral-black",
          }}
        />
      </div>
    </SelectorDropdown>
  }
/>
```

### 3. Breadcrumb with Icons

Breadcrumb items with custom icons:

```typescript
const longPathItems = [
  {
    label: "Home",
    href: "#",
    icon: <IcHome className="h-4 w-4 mr-1" />,
    isHome: true,
  },
  {
    label: "Products",
    href: "#",
    icon: <IcFolder className="h-4 w-4 mr-1" />,
  },
  {
    label: "Electronics",
    href: "#",
    icon: <IcFolder className="h-4 w-4 mr-1" />,
  },
  {
    label: "Computers",
    href: "#",
    icon: <IcFolder className="h-4 w-4 mr-1" />,
  },
  {
    label: "Laptops",
    href: "#",
    icon: <IcFolder className="h-4 w-4 mr-1" />,
  },
  {
    label: "MacBook Pro",
    icon: <IcDocument className="h-4 w-4 mr-1" />,
  },
];

<Breadcrumb
  items={longPathItems}
  ellipsisComponent={
    <SelectorDropdown
      options={longPathItems.slice(1, -2).map((item, idx) => (
        <div key={idx} className="flex items-center">
          {item.icon}
          {item.label}
        </div>
      ))}
      placeholder="More"
      showIcon
      size="md"
      className="!bg-transparent !p-0 !shadow-none"
    >
      <IconButton
        appearance="default"
        icon={<IcMoreHorizontal />}
        size="sm"
        type="tertiary"
        classNames={{
          button: "hover:bg-transparent text-color-neutral-black",
          icon: "text-color-neutral-black",
        }}
      />
    </SelectorDropdown>
  }
/>
```

### 4. Manual Composition

For complete custom control, you can manually compose the breadcrumb:

```typescript
<Breadcrumb>
  <ol className="flex flex-wrap items-center gap-1.5 break-words text-sm text-muted-foreground">
    <li className="inline-flex items-center gap-1.5">
      <a
        href="#"
        className="flex items-center gap-1.5 text-sm font-medium text-color-text-default hover:text-color-primary-50 active:text-color-primary-60 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-color-primary-60 rounded-[4px]"
      >
        <div className="flex items-center gap-1.5 text-color-neutral-grey-80 hover:text-color-primary-50 active:text-color-primary-60 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-color-primary-60">
          <IcHome className="h-4 w-4 mr-1" />
          <span className="text-gray-900 text-color-text-default hover:text-color-primary-50 active:text-color-primary-60 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-color-primary-60">
            Home
          </span>
        </div>
      </a>
    </li>
    <span aria-hidden="true" className="text-gray-400">
      <IcChevronRight className="h-4 w-4" />
    </span>
    <li className="inline-flex items-center gap-1.5">
      <a
        href="#"
        className="flex items-center gap-1.5 text-sm font-medium text-color-text-default hover:text-color-primary-50 active:text-color-primary-60 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-color-primary-60 rounded-[4px]"
      >
        Products
      </a>
    </li>
    <span aria-hidden="true" className="text-gray-400">
      <IcChevronRight className="h-4 w-4" />
    </span>
    <li className="inline-flex items-center gap-1.5">
      <span
        aria-current="page"
        className="flex items-center gap-1.5 text-sm font-medium text-gray-900 text-color-text-default hover:text-color-primary-50 active:text-color-primary-60 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-color-primary-60"
      >
        Current Product
      </span>
    </li>
  </ol>
</Breadcrumb>
```

### 5. Ellipsis Between Items

Control exactly where the ellipsis appears:

```typescript
<Breadcrumb
  items={sampleItems}
  maxItems={4}
  ellipsisComponent={
    <SelectorDropdown
      options={sampleItems.slice(1, -2).map((item, idx) => (
        <div key={idx}>{item.label}</div>
      ))}
      placeholder="More"
      showIcon
      size="md"
      className="!bg-transparent !p-0 !shadow-none"
      onChange={value => {
        console.log("Selected breadcrumb", value);
      }}
    >
      <div>
        <IconButton
          appearance="default"
          icon={<IcMoreHorizontal />}
          inverse
          size="sm"
          type="tertiary"
          style={{ color: "#000" }}
          classNames={{
            button: "hover:bg-transparent focus:bg-transparent active:bg-transparent shadow-none text-color-neutral-black",
            icon: "text-color-neutral-black",
          }}
        />
      </div>
    </SelectorDropdown>
  }
/>
```

### 6. Advanced Breadcrumb with Collapse After

Use `collapseAfter` prop to control collapse behavior:

```typescript
const breadcrumbItems = [
  {
    label: "B01",
    href: "#",
    icon: <IcHome className="h-4 w-4 mr-1" />,
    isHome: true,
  },
  { label: "B02", href: "#" },
  { label: "B03", href: "#" },
  { label: "B04", href: "#" },
  { label: "B05", href: "#" },
  { label: "B06", href: "#" },
];

<Breadcrumb
  items={breadcrumbItems}
  collapseAfter={2}
  ellipsisComponent={
    <SelectorDropdown
      options={breadcrumbItems.slice(1, -2).map((item, idx) => (
        <div key={idx}>{item.label}</div>
      ))}
      placeholder="More"
      showIcon
      size="md"
      className="!bg-transparent !p-0 !shadow-none"
      onChange={value => {
        console.log("Selected breadcrumb", value);
      }}
    >
      <div>
        <IconButton
          appearance="default"
          icon={<IcMoreHorizontal />}
          inverse
          size="sm"
          type="tertiary"
          style={{ color: "#000" }}
          classNames={{
            button: "hover:bg-transparent focus:bg-transparent active:bg-transparent shadow-none text-color-neutral-black",
            icon: "text-color-neutral-black",
          }}
        />
      </div>
    </SelectorDropdown>
  }
/>
```

## Responsive Behavior

The breadcrumb automatically adjusts based on container width:

- **< 200px**: Shows only 1 item
- **< 300px**: Shows only 2 items
- **< 400px**: Shows only 3 items
- **≥ 400px**: Shows `maxItems` items

## Accessibility Features

- **ARIA Labels**: Uses `aria-label="Breadcrumb"` for navigation
- **Current Page**: Uses `aria-current="page"` for the current item
- **Keyboard Navigation**: Supports focus management with `focus-visible` styles
- **Screen Reader Support**: Separators are hidden from screen readers with `aria-hidden="true"`

## Styling

### CSS Classes

The component uses Tailwind CSS classes and custom color tokens:

- **Text Colors**: `text-color-text-default`, `text-color-primary-50`, `text-color-primary-60`
- **Icon Colors**: `text-color-neutral-grey-80`, `text-color-neutral-grey-60`
- **Hover States**: `hover:text-color-primary-50`
- **Focus States**: `focus-visible:ring-2 focus-visible:ring-color-primary-60`

### Customization

You can customize the appearance using the provided className props:

```typescript
<Breadcrumb
  items={items}
  className="my-custom-breadcrumb"
  itemClassName="my-custom-item"
  separatorClassName="my-custom-separator"
  ellipsisClassName="my-custom-ellipsis"
/>
```

## Integration with Next.js

For Next.js applications, you can use a custom link component:

```typescript
import { Link } from "gends";

<Breadcrumb
  items={items}
  linkComponent={Link}
/>
```

## Testing

The component includes comprehensive test IDs:

- `breadcrumb`: Main container
- `breadcrumb-list`: Breadcrumb list
- `breadcrumb-item-{index}`: Individual items
- `breadcrumb-separator-{index}`: Separators
- `breadcrumb-ellipsis`: Ellipsis button
- `breadcrumb-ellipsis-item`: Ellipsis container

Use the `testIdPrefix` prop to customize test ID prefixes:

```typescript
<Breadcrumb
  items={items}
  testIdPrefix="custom-breadcrumb"
/>
```

## Best Practices

1. **Always provide a home link** as the first item
2. **Use meaningful labels** that clearly indicate the page hierarchy
3. **Keep labels concise** - they're automatically truncated at 150px width
4. **Provide custom ellipsis components** for better UX when collapsing
5. **Use icons sparingly** - typically only for the home item and key categories
6. **Test responsive behavior** at different screen sizes
7. **Ensure proper contrast** for accessibility compliance

## Common Patterns

### E-commerce Category Navigation

```typescript
const categoryItems = [
  { label: "Home", href: "/", icon: <IcHome className="h-4 w-4 mr-1" />, isHome: true },
  { label: "Electronics", href: "/electronics" },
  { label: "Computers", href: "/electronics/computers" },
  { label: "Laptops", href: "/electronics/computers/laptops" },
  { label: "MacBook Pro 16-inch" },
];
```

### Document Management System

```typescript
const documentItems = [
  { label: "Home", href: "/", icon: <IcHome className="h-4 w-4 mr-1" />, isHome: true },
  { label: "Shared Documents", href: "/shared", icon: <IcFolder className="h-4 w-4 mr-1" /> },
  { label: "Projects", href: "/shared/projects", icon: <IcFolder className="h-4 w-4 mr-1" /> },
  { label: "Q4 Reports", href: "/shared/projects/q4", icon: <IcFolder className="h-4 w-4 mr-1" /> },
  { label: "Financial_Report_2024.pdf", icon: <IcDocument className="h-4 w-4 mr-1" /> },
];
```

### Admin Dashboard

```typescript
const adminItems = [
  { label: "Dashboard", href: "/admin", icon: <IcHome className="h-4 w-4 mr-1" />, isHome: true },
  { label: "Users", href: "/admin/users" },
  { label: "User Management", href: "/admin/users/management" },
  { label: "Edit User Profile" },
];
```
