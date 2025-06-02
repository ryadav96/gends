# Tabs

A versatile tabs component built on Radix UI that supports multiple sizes, variants, icons, counters, and interactive features like renaming, duplicating, and deleting tabs—perfect for organizing content into accessible, interactive sections.

---

## 1. Quick start

```tsx
import { Tabs, TabsList, TabsTrigger, TabsContent } from "gends";

function Example() {
  return (
    <Tabs defaultValue="tab1">
      <TabsList>
        <TabsTrigger value="tab1">First Tab</TabsTrigger>
        <TabsTrigger value="tab2">Second Tab</TabsTrigger>
      </TabsList>
      <TabsContent value="tab1">First tab content</TabsContent>
      <TabsContent value="tab2">Second tab content</TabsContent>
    </Tabs>
  );
}
```

Compose tab elements to create an organized, accessible interface. The component handles keyboard navigation and ARIA attributes automatically.

---

## 2. Sizes

| size | Height | Recommended use case |
| ---- | ------ | -------------------- |
| `s`  | 36 px  | Dense layouts        |
| `m`  | 36 px  | Standard layouts     |
| `l`  | 48 px  | Touch interfaces     |

```tsx
<Tabs size="s">
  <TabsList>
    <TabsTrigger>Small</TabsTrigger>
  </TabsList>
</Tabs>

<Tabs size="l">
  <TabsList>
    <TabsTrigger>Large</TabsTrigger>
  </TabsList>
</Tabs>
```

---

## 3. Variants

| kind      | Description     | Use Case             |
| --------- | --------------- | -------------------- |
| `default` | Standard tabs   | Primary navigation   |
| `subtab`  | Pill-style tabs | Secondary navigation |

```tsx
// Default tabs
<Tabs kind="default">
  <TabsList>
    <TabsTrigger>Standard Tab</TabsTrigger>
  </TabsList>
</Tabs>

// Subtab variant
<Tabs kind="subtab">
  <TabsList>
    <TabsTrigger>Pill Tab</TabsTrigger>
  </TabsList>
</Tabs>
```

---

## 4. Features

### Icons & Counters

```tsx
<TabsTrigger icon={<IcMail size="24px" />} tabCount={5}>
  Messages
</TabsTrigger>
```

### Interactive Features

```tsx
<Tabs
  onTabRename={(value, newLabel) => console.log("Renamed:", value, "to", newLabel)}
  onTabDuplicate={value => console.log("Duplicated:", value)}
  onTabDelete={value => console.log("Deleted:", value)}
>
  <TabsList>
    <TabsTrigger showRename showDuplicate showDelete>
      Interactive Tab
    </TabsTrigger>
  </TabsList>
</Tabs>
```

---

## 5. Full prop reference

### Tabs Component

| Prop             | Type                                        | Default     | Description           |
| ---------------- | ------------------------------------------- | ----------- | --------------------- |
| `size`           | `'s' \| 'm' \| 'l'`                         | `'s'`       | Component size        |
| `kind`           | `'default' \| 'subtab'`                     | `'default'` | Visual variant        |
| `defaultValue`   | `string`                                    | -           | Initial active tab    |
| `value`          | `string`                                    | -           | Controlled active tab |
| `onTabRename`    | `(value: string, newLabel: string) => void` | -           | Rename handler        |
| `onTabDuplicate` | `(value: string) => void`                   | -           | Duplication handler   |
| `onTabDelete`    | `(value: string) => void`                   | -           | Deletion handler      |

### TabsList

| Prop         | Type      | Default | Description              |
| ------------ | --------- | ------- | ------------------------ |
| `fullWidth`  | `boolean` | `false` | Stretch to container     |
| `scrollable` | `boolean` | `false` | Enable horizontal scroll |

### TabsTrigger

| Prop            | Type        | Default | Description           |
| --------------- | ----------- | ------- | --------------------- |
| `icon`          | `ReactNode` | -       | Leading icon          |
| `tabCount`      | `number`    | -       | Badge counter         |
| `showRename`    | `boolean`   | `false` | Show rename option    |
| `showDuplicate` | `boolean`   | `false` | Show duplicate option |
| `showDelete`    | `boolean`   | `false` | Show delete option    |

### TabsContent

| Prop         | Type      | Default | Description           |
| ------------ | --------- | ------- | --------------------- |
| `value`      | `string`  | -       | Matching tab value    |
| `forceMount` | `boolean` | `false` | Always render content |

---

## 6. Recipes

### Basic navigation tabs

```tsx
function NavigationTabs() {
  return (
    <Tabs defaultValue="overview">
      <TabsList>
        <TabsTrigger value="overview" icon={<IcHome />}>
          Overview
        </TabsTrigger>
        <TabsTrigger value="analytics" icon={<IcChart />}>
          Analytics
        </TabsTrigger>
        <TabsTrigger value="settings" icon={<IcSettings />}>
          Settings
        </TabsTrigger>
      </TabsList>
      <TabsContent value="overview">Overview content</TabsContent>
      <TabsContent value="analytics">Analytics content</TabsContent>
      <TabsContent value="settings">Settings content</TabsContent>
    </Tabs>
  );
}
```

### Editable document tabs

```tsx
function DocumentTabs() {
  const handleRename = (value: string, newLabel: string) => {
    // Update document title
  };

  const handleDuplicate = (value: string) => {
    // Clone document
  };

  const handleDelete = (value: string) => {
    // Delete document
  };

  return (
    <Tabs onTabRename={handleRename} onTabDuplicate={handleDuplicate} onTabDelete={handleDelete}>
      <TabsList>
        <TabsTrigger value="doc1" showRename showDuplicate showDelete>
          Document.txt
        </TabsTrigger>
      </TabsList>
    </Tabs>
  );
}
```

### Scrollable tabs with counter

```tsx
function MessageTabs() {
  return (
    <Tabs defaultValue="inbox">
      <TabsList scrollable>
        <TabsTrigger value="inbox" tabCount={5}>
          Inbox
        </TabsTrigger>
        <TabsTrigger value="sent" tabCount={2}>
          Sent
        </TabsTrigger>
        <TabsTrigger value="drafts" tabCount={3}>
          Drafts
        </TabsTrigger>
      </TabsList>
    </Tabs>
  );
}
```

---

## 7. Accessibility considerations

- Built on Radix UI primitives for robust accessibility
- Full keyboard navigation support (Arrow keys, Home, End)
- Proper ARIA attributes and roles
- Focus management
- Screen reader announcements

```tsx
// Keyboard navigation
// - Arrow Right/Left: Move between tabs
// - Home: Jump to first tab
// - End: Jump to last tab
// - Enter/Space: Activate tab
```

---

## 8. Design patterns

### Layout patterns

- Consistent spacing and alignment
- Clear visual hierarchy
- Responsive behavior
- Proper tab organization

### Interaction patterns

- Clear active state indication
- Smooth transitions
- Intuitive editing interface
- Proper loading states

### Content patterns

- Clear, concise tab labels
- Meaningful icons
- Appropriate use of counters
- Consistent content organization

---
