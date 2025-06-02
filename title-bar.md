# TitleBar

A flexible header component that provides consistent layout for start, center, and end content sections with customizable background variants and spacing.

---

## 1. Quick start

```tsx
import { TitleBar } from "gends";
import { Button, IconButton } from "gends";

function Example() {
  return (
    <TitleBar
      variant="default"
      startContent={<h1>Page Title</h1>}
      endContent={<Button>Action</Button>}
    />
  );
}
```

---

## 2. Variants

| variant          | Description            | Use case            |
| ---------------- | ---------------------- | ------------------- |
| `default`        | Transparent background | In-page headers     |
| `withBackground` | Background with border | Modal/panel headers |

```tsx
// Default transparent variant
<TitleBar variant="default" startContent={<h1>Title</h1>} />

// With background and border
<TitleBar
  variant="withBackground"
  startContent={<h1>Modal Title</h1>}
  endContent={<IconButton icon={<CloseIcon />} />}
/>
```

---

## 3. Content sections

The TitleBar provides three distinct content areas for flexible layout:

| section         | Position | Description               | Typical content             |
| --------------- | -------- | ------------------------- | --------------------------- |
| `startContent`  | Left     | Primary content area      | Titles, logos, back buttons |
| `centerContent` | Center   | Optional centered content | Navigation, tabs            |
| `endContent`    | Right    | Action area               | Buttons, menus, controls    |

```tsx
<TitleBar
  startContent={
    <div className="flex items-center gap-3">
      <IconButton icon={<BackIcon />} />
      <h1>Dashboard</h1>
    </div>
  }
  centerContent={
    <nav className="flex gap-4">
      <a href="/overview">Overview</a>
      <a href="/analytics">Analytics</a>
    </nav>
  }
  endContent={
    <div className="flex items-center gap-2">
      <IconButton icon={<SearchIcon />} />
      <IconButton icon={<SettingsIcon />} />
      <Button>Export</Button>
    </div>
  }
/>
```

---

## 4. States

```tsx
// Normal state
<TitleBar startContent={<h1>Active Title</h1>} />

// Disabled state
<TitleBar
  disabled={true}
  startContent={<h1>Disabled Title</h1>}
  endContent={<Button disabled>Action</Button>}
/>
```

---

## 5. Custom styling

```tsx
// Custom CSS classes
<TitleBar
  className="shadow-lg bg-gradient-to-r from-blue-500 to-purple-600"
  startContent={<h1 className="text-white">Custom Title</h1>}
/>

// With custom styling and content
<TitleBar
  variant="withBackground"
  className="border-blue-200 bg-blue-50"
  startContent={<h1 className="text-blue-900">Styled Header</h1>}
/>
```

---

## 6. Full prop reference

### Basic Props

| Prop            | Type                            | Default     | Description                 |
| --------------- | ------------------------------- | ----------- | --------------------------- |
| `variant`       | `'default' \| 'withBackground'` | `'default'` | Background and border style |
| `startContent`  | `ReactNode`                     | -           | Left-aligned content        |
| `centerContent` | `ReactNode`                     | -           | Center-aligned content      |
| `endContent`    | `ReactNode`                     | -           | Right-aligned content       |

### State Props

| Prop       | Type      | Default | Description                  |
| ---------- | --------- | ------- | ---------------------------- |
| `disabled` | `boolean` | `false` | Disable interactive elements |

### Styling Props

| Prop        | Type     | Description            |
| ----------- | -------- | ---------------------- |
| `className` | `string` | Additional CSS classes |

### HTML Props

The TitleBar component accepts all standard HTML div element props including:

| Prop    | Type     | Description   |
| ------- | -------- | ------------- |
| `id`    | `string` | Element ID    |
| `role`  | `string` | ARIA role     |
| `style` | `object` | Inline styles |

---

## 7. Recipes

### Simple page header

```tsx
<TitleBar
  startContent={<h1 className="text-2xl font-bold">Products</h1>}
  endContent={<Button kind="primary">Add Product</Button>}
/>
```

### Modal header with close button

```tsx
<TitleBar
  variant="withBackground"
  startContent={<h2 className="text-xl">Edit Profile</h2>}
  endContent={<IconButton type="tertiary" icon={<CloseIcon />} onClick={onClose} />}
/>
```

### Navigation header

```tsx
<TitleBar
  startContent={
    <div className="flex items-center gap-2">
      <IconButton icon={<BackIcon />} onClick={goBack} />
      <h1>Settings</h1>
    </div>
  }
  centerContent={
    <nav className="flex gap-6">
      <a href="/settings/general">General</a>
      <a href="/settings/security">Security</a>
      <a href="/settings/billing">Billing</a>
    </nav>
  }
  endContent={<Button>Save Changes</Button>}
/>
```

### Toolbar with multiple actions

```tsx
<TitleBar
  variant="withBackground"
  startContent={<h2>Document Editor</h2>}
  endContent={
    <div className="flex items-center gap-2">
      <IconButton icon={<UndoIcon />} />
      <IconButton icon={<RedoIcon />} />
      <IconButton icon={<ShareIcon />} />
      <Button kind="primary">Publish</Button>
    </div>
  }
/>
```

### Disabled state

```tsx
<TitleBar
  disabled={true}
  startContent={<h1 className="opacity-50">Loading...</h1>}
  endContent={
    <Button disabled kind="secondary">
      Please Wait
    </Button>
  }
/>
```

### Custom branded header

```tsx
<TitleBar
  className="bg-gradient-to-r from-purple-600 to-blue-600 text-white"
  startContent={
    <div className="flex items-center gap-3">
      <img src="/logo.svg" alt="Logo" className="h-8 w-8" />
      <h1 className="text-xl font-bold">Brand Dashboard</h1>
    </div>
  }
  endContent={
    <div className="flex items-center gap-2">
      <Button kind="secondary" appearance="contrast">
        Help
      </Button>
      <Button kind="primary" appearance="contrast">
        Account
      </Button>
    </div>
  }
/>
```

---

## 8. Accessibility

The TitleBar component includes accessibility considerations:

- Proper semantic HTML structure with div containers
- Focus management for interactive elements
- Keyboard navigation support for contained elements
- Disabled state propagation to child elements

```tsx
<TitleBar
  role="banner"
  aria-label="Main navigation header"
  startContent={<h1 id="page-title">Dashboard</h1>}
  endContent={<Button aria-describedby="page-title">Actions</Button>}
/>
```

---

## 9. Design Tokens

The TitleBar component uses the following design system tokens:

**Layout:**

- Width: `w-full` (100% container width)
- Padding: `px-4 py-3` (16px horizontal, 12px vertical)
- Flex layout: `flex items-center justify-between`

**Spacing:**

- Start content gap: `gap-3` (12px between items)
- End content gap: `gap-4` (16px between items)

**Background Variants:**

- Default: `bg-transparent` (no background)
- WithBackground: `bg-background border-b` (background with bottom border)

**Typography:**

- Inherits text styles from content elements
- No default typography constraints

**Borders:**

- WithBackground variant: Bottom border using design system border color

---

Consider using TitleBar with:

- **Modal** — For dialog headers
- **Page** — For main page headers
- **Panel** — For sidebar or panel headers
- **Card** — For card section headers
- **Navigation** — For top navigation bars
