# Tabs Component

## Overview

The Tabs component is a comprehensive and flexible tabbed interface built on top of Radix UI primitives, designed for organizing content into accessible, interactive sections. It offers extensive customization options including multiple sizes, visual variants, icons, counter badges, and advanced interactive features like renaming, duplicating, and deleting tabs. Perfect for complex applications requiring dynamic tab management with full accessibility support and Genesis Design System integration.

## Component API

### Tabs Props

| Prop                   | Type                                        | Default      | Description                                 |
| ---------------------- | ------------------------------------------- | ------------ | ------------------------------------------- |
| `items`                | `TabItem[]`                                 | **Required** | Array of tab configuration objects          |
| `value`                | `string`                                    | -            | Currently selected tab value (controlled)   |
| `defaultValue`         | `string`                                    | -            | Default selected tab value (uncontrolled)   |
| `onValueChange`        | `(value: string) => void`                   | -            | Callback when tab selection changes         |
| `kind`                 | `'default' \| 'subtab'`                     | `'default'`  | Visual variant of the tabs                  |
| `size`                 | `'s' \| 'm' \| 'l'`                         | `'s'`        | Size variant affecting height and spacing   |
| `enableTabContextMenu` | `boolean`                                   | `false`      | Enable global context menu for all tabs     |
| `onTabRename`          | `(value: string, newLabel: string) => void` | -            | Callback when tab is renamed                |
| `onTabDuplicate`       | `(value: string) => void`                   | -            | Callback when tab is duplicated             |
| `onTabDelete`          | `(value: string) => void`                   | -            | Callback when tab is deleted                |
| `className`            | `string`                                    | -            | Additional CSS class for the tabs container |

### TabItem Interface

| Property       | Type        | Required | Description                           |
| -------------- | ----------- | -------- | ------------------------------------- |
| `value`        | `string`    | Yes      | Unique identifier for the tab         |
| `label`        | `string`    | Yes      | Display text for the tab              |
| `content`      | `ReactNode` | Yes      | Content to display when tab is active |
| `icon`         | `ReactNode` | No       | Icon to display before the tab label  |
| `tabCount`     | `number`    | No       | Number to display in counter badge    |
| `canRename`    | `boolean`   | No       | Enable rename option for this tab     |
| `canDuplicate` | `boolean`   | No       | Enable duplicate option for this tab  |
| `canDelete`    | `boolean`   | No       | Enable delete option for this tab     |

## Size Variants

The Tabs component offers three size variants optimized for different use cases:

| Size | Height | Padding | Font Size | Recommended Use Case                     |
| ---- | ------ | ------- | --------- | ---------------------------------------- |
| `s`  | 36px   | 12px    | 14px      | Compact interfaces, secondary navigation |
| `m`  | 36px   | 12px    | 14px      | Standard layouts, most common use case   |
| `l`  | 48px   | 16px    | 16px      | Touch interfaces, primary navigation     |

```tsx
// Small tabs for compact spaces
<Tabs
  items={tabItems}
  size="s"
  kind="default"
/>

// Large tabs for touch interfaces
<Tabs
  items={tabItems}
  size="l"
  kind="default"
/>
```

## Visual Variants

### Default Tabs

Traditional tab style with underline indicator, ideal for primary navigation.

```tsx
<Tabs
  items={[
    { value: "overview", label: "Overview", content: "Overview content" },
    { value: "details", label: "Details", content: "Details content" },
  ]}
  kind="default"
  defaultValue="overview"
/>
```

### Subtab Variant

Pill-style tabs with rounded background, perfect for secondary navigation and filters.

```tsx
<Tabs
  items={[
    { value: "all", label: "All Items", content: "All items content" },
    { value: "active", label: "Active", content: "Active items content" },
    { value: "archived", label: "Archived", content: "Archived items content" },
  ]}
  kind="subtab"
  defaultValue="all"
/>
```

## Basic Usage

### Simple Tabs

```tsx
import { Tabs } from "gends";

const BasicExample = () => {
  const items = [
    {
      value: "account",
      label: "Account",
      content: <div>Make changes to your account here.</div>,
    },
    {
      value: "password",
      label: "Password",
      content: <div>Change your password here.</div>,
    },
    {
      value: "settings",
      label: "Settings",
      content: <div>Edit your preferences here.</div>,
    },
  ];

  return <Tabs items={items} defaultValue="account" kind="default" size="s" />;
};
```

### Controlled Tabs

```tsx
import { useState } from "react";
import { Tabs } from "gends";

const ControlledExample = () => {
  const [activeTab, setActiveTab] = useState("account");

  const handleTabChange = (value: string) => {
    setActiveTab(value);
    console.log(`Tab changed to: ${value}`);
  };

  return (
    <div>
      <Tabs
        items={tabItems}
        value={activeTab}
        onValueChange={handleTabChange}
        kind="default"
        size="s"
      />

      {/* Programmatic control */}
      <div className="mt-4 space-x-2">
        <button onClick={() => setActiveTab("account")}>Select Account</button>
        <button onClick={() => setActiveTab("password")}>Select Password</button>
      </div>
    </div>
  );
};
```

## Enhanced Features

### Tabs with Icons and Counters

```tsx
import { IcProfile, IcSettings, IcFavorite } from "gends";

const TabsWithFeatures = () => {
  const items = [
    {
      value: "account",
      label: "Account",
      content: "Account management content",
      icon: <IcProfile className="h-4 w-4" />,
      tabCount: 5,
    },
    {
      value: "favorites",
      label: "Favorites",
      content: "Your favorite items",
      icon: <IcFavorite className="h-4 w-4" />,
      tabCount: 12,
    },
    {
      value: "settings",
      label: "Settings",
      content: "Application settings",
      icon: <IcSettings className="h-4 w-4" />,
      tabCount: 3,
    },
  ];

  return <Tabs items={items} defaultValue="account" kind="default" size="l" />;
};
```

### Interactive Tabs with Context Menu

```tsx
import { useState } from "react";
import { Tabs } from "gends";

const InteractiveTabsExample = () => {
  const [items, setItems] = useState([
    {
      value: "doc1",
      label: "Document 1",
      content: "First document content",
      icon: <IcDocument className="h-4 w-4" />,
    },
    {
      value: "doc2",
      label: "Document 2",
      content: "Second document content",
      icon: <IcDocument className="h-4 w-4" />,
    },
  ]);

  const [activeTab, setActiveTab] = useState("doc1");

  const handleTabRename = (value: string, newLabel: string) => {
    if (newLabel.trim() === "") return;

    setItems(prevItems =>
      prevItems.map(item => (item.value === value ? { ...item, label: newLabel } : item))
    );
  };

  const handleTabDuplicate = (value: string) => {
    const tabToDuplicate = items.find(item => item.value === value);
    if (tabToDuplicate) {
      const newValue = `${value}_copy_${Date.now()}`;
      const newTab = {
        ...tabToDuplicate,
        value: newValue,
        label: `${tabToDuplicate.label} (Copy)`,
      };
      setItems(prevItems => [...prevItems, newTab]);
    }
  };

  const handleTabDelete = (value: string) => {
    if (items.length <= 1) return; // Prevent deleting last tab

    setItems(prevItems => prevItems.filter(item => item.value !== value));

    if (value === activeTab) {
      const remainingItems = items.filter(item => item.value !== value);
      if (remainingItems.length > 0) {
        setActiveTab(remainingItems[0].value);
      }
    }
  };

  return (
    <Tabs
      items={items}
      value={activeTab}
      onValueChange={setActiveTab}
      kind="default"
      size="s"
      enableTabContextMenu
      onTabRename={handleTabRename}
      onTabDuplicate={handleTabDuplicate}
      onTabDelete={handleTabDelete}
    />
  );
};
```

### Individual Tab Context Controls

```tsx
const IndividualControlExample = () => {
  const [items, setItems] = useState([
    {
      value: "protected",
      label: "Protected Tab",
      content: "This tab cannot be deleted",
      canRename: true,
      canDuplicate: true,
      canDelete: false, // Protected from deletion
    },
    {
      value: "limited",
      label: "Limited Tab",
      content: "This tab has limited options",
      canRename: true,
      canDuplicate: false, // Cannot duplicate
      canDelete: true,
    },
    {
      value: "readonly",
      label: "Read-only Tab",
      content: "This tab cannot be renamed",
      canRename: false, // Cannot rename
      canDuplicate: true,
      canDelete: true,
    },
    {
      value: "standard",
      label: "Standard Tab",
      content: "This tab has no context menu",
      // No context menu properties defined
    },
  ]);

  // ... handle functions ...

  return (
    <Tabs
      items={items}
      value={activeTab}
      onValueChange={setActiveTab}
      kind="default"
      size="s"
      onTabRename={handleTabRename}
      onTabDuplicate={handleTabDuplicate}
      onTabDelete={handleTabDelete}
    />
  );
};
```

## Real-World Examples

### 1. Document Editor Interface

```tsx
const DocumentEditor = () => {
  const [documents, setDocuments] = useState([
    {
      value: "welcome.md",
      label: "welcome.md",
      content: <MarkdownEditor content="# Welcome" />,
      icon: <IcMarkdown className="h-4 w-4" />,
      canRename: true,
      canDuplicate: true,
      canDelete: true,
    },
    {
      value: "readme.md",
      label: "README.md",
      content: <MarkdownEditor content="# Project README" />,
      icon: <IcMarkdown className="h-4 w-4" />,
      canRename: false, // System file
      canDuplicate: true,
      canDelete: false,
    },
  ]);

  const [activeDocument, setActiveDocument] = useState("welcome.md");

  const createNewDocument = () => {
    const newDoc = {
      value: `untitled-${Date.now()}.md`,
      label: "Untitled Document",
      content: <MarkdownEditor content="" />,
      icon: <IcMarkdown className="h-4 w-4" />,
      canRename: true,
      canDuplicate: true,
      canDelete: true,
    };
    setDocuments(prev => [...prev, newDoc]);
    setActiveDocument(newDoc.value);
  };

  return (
    <div className="h-screen flex flex-col">
      <div className="border-b bg-gray-50 p-2 flex items-center justify-between">
        <Tabs
          items={documents}
          value={activeDocument}
          onValueChange={setActiveDocument}
          kind="default"
          size="s"
          onTabRename={handleDocumentRename}
          onTabDuplicate={handleDocumentDuplicate}
          onTabDelete={handleDocumentDelete}
        />
        <button
          onClick={createNewDocument}
          className="px-3 py-1 bg-primary text-white rounded text-sm"
        >
          New Document
        </button>
      </div>
      <div className="flex-1 p-4">
        {documents.find(doc => doc.value === activeDocument)?.content}
      </div>
    </div>
  );
};
```

### 2. Dashboard Analytics

```tsx
const AnalyticsDashboard = () => {
  const analyticsItems = [
    {
      value: "overview",
      label: "Overview",
      content: <OverviewChart />,
      icon: <IcChart className="h-4 w-4" />,
      tabCount: 24, // Number of metrics
    },
    {
      value: "users",
      label: "Users",
      content: <UserAnalytics />,
      icon: <IcUsers className="h-4 w-4" />,
      tabCount: 1247, // Active users
    },
    {
      value: "revenue",
      label: "Revenue",
      content: <RevenueChart />,
      icon: <IcDollar className="h-4 w-4" />,
      tabCount: 5, // Revenue streams
    },
    {
      value: "reports",
      label: "Reports",
      content: <ReportsTable />,
      icon: <IcReport className="h-4 w-4" />,
      tabCount: 12, // Available reports
    },
  ];

  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold mb-6">Analytics Dashboard</h1>
      <Tabs items={analyticsItems} defaultValue="overview" kind="default" size="l" />
    </div>
  );
};
```

### 3. Settings Panel

```tsx
const SettingsPanel = () => {
  const settingsItems = [
    {
      value: "general",
      label: "General",
      content: <GeneralSettings />,
      icon: <IcSettings className="h-4 w-4" />,
    },
    {
      value: "account",
      label: "Account",
      content: <AccountSettings />,
      icon: <IcProfile className="h-4 w-4" />,
      tabCount: 3, // Pending actions
    },
    {
      value: "security",
      label: "Security",
      content: <SecuritySettings />,
      icon: <IcShield className="h-4 w-4" />,
      tabCount: 1, // Security alert
    },
    {
      value: "notifications",
      label: "Notifications",
      content: <NotificationSettings />,
      icon: <IcBell className="h-4 w-4" />,
    },
  ];

  return (
    <div className="max-w-4xl mx-auto p-6">
      <h1 className="text-2xl font-bold mb-6">Settings</h1>
      <Tabs items={settingsItems} defaultValue="general" kind="default" size="m" />
    </div>
  );
};
```

### 4. E-commerce Product Details

```tsx
const ProductDetailsPage = () => {
  const productTabs = [
    {
      value: "description",
      label: "Description",
      content: <ProductDescription product={product} />,
    },
    {
      value: "specifications",
      label: "Specifications",
      content: <ProductSpecs product={product} />,
    },
    {
      value: "reviews",
      label: "Reviews",
      content: <ProductReviews productId={product.id} />,
      tabCount: product.reviewCount,
    },
    {
      value: "shipping",
      label: "Shipping & Returns",
      content: <ShippingInfo />,
    },
  ];

  return (
    <div className="max-w-6xl mx-auto p-6">
      <div className="grid grid-cols-1 md:grid-cols-2 gap-8 mb-8">
        <ProductGallery images={product.images} />
        <ProductInfo product={product} />
      </div>

      <Tabs items={productTabs} defaultValue="description" kind="subtab" size="m" />
    </div>
  );
};
```

### 5. Project Management Interface

```tsx
const ProjectManager = () => {
  const [projects, setProjects] = useState([
    {
      value: "website-redesign",
      label: "Website Redesign",
      content: <ProjectBoard projectId="website-redesign" />,
      icon: <IcGlobe className="h-4 w-4" />,
      tabCount: 15, // Active tasks
      canRename: true,
      canDuplicate: true,
      canDelete: true,
    },
    {
      value: "mobile-app",
      label: "Mobile App",
      content: <ProjectBoard projectId="mobile-app" />,
      icon: <IcPhone className="h-4 w-4" />,
      tabCount: 8,
      canRename: true,
      canDuplicate: true,
      canDelete: true,
    },
  ]);

  const [activeProject, setActiveProject] = useState("website-redesign");

  const createNewProject = () => {
    const newProject = {
      value: `project-${Date.now()}`,
      label: "New Project",
      content: <ProjectBoard projectId={`project-${Date.now()}`} />,
      icon: <IcFolder className="h-4 w-4" />,
      tabCount: 0,
      canRename: true,
      canDuplicate: true,
      canDelete: true,
    };
    setProjects(prev => [...prev, newProject]);
    setActiveProject(newProject.value);
  };

  return (
    <div className="h-screen flex flex-col">
      <header className="border-b bg-white px-6 py-4">
        <div className="flex items-center justify-between">
          <h1 className="text-xl font-semibold">Project Manager</h1>
          <button
            onClick={createNewProject}
            className="px-4 py-2 bg-primary text-white rounded hover:bg-primary-dark"
          >
            New Project
          </button>
        </div>
      </header>

      <div className="flex-1 bg-gray-50">
        <div className="border-b bg-white px-6">
          <Tabs
            items={projects}
            value={activeProject}
            onValueChange={setActiveProject}
            kind="default"
            size="m"
            onTabRename={handleProjectRename}
            onTabDuplicate={handleProjectDuplicate}
            onTabDelete={handleProjectDelete}
          />
        </div>
        <div className="p-6">{projects.find(p => p.value === activeProject)?.content}</div>
      </div>
    </div>
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab**: Navigate between tab triggers
- **Enter/Space**: Activate focused tab
- **Arrow Keys**: Navigate between tab triggers
- **Home**: Focus first tab
- **End**: Focus last tab

### Screen Reader Support

- Automatic ARIA labeling with `role="tablist"`, `role="tab"`, and `role="tabpanel"`
- Proper `aria-selected` states for active tabs
- `aria-controls` linking tabs to their content panels
- `aria-label` and `aria-describedby` for context menu actions

### Visual Accessibility

- High contrast focus indicators
- Color-blind friendly state indicators
- Sufficient color contrast ratios (WCAG AA compliant)
- Clear visual hierarchy and spacing

```tsx
// Accessibility-enhanced tabs
<Tabs
  items={items}
  defaultValue="account"
  aria-label="Account settings navigation"
  className="focus-within:ring-2 focus-within:ring-offset-2 focus-within:ring-primary"
/>
```

## Design System Integration

### Genesis Design System Tokens

The Tabs component uses Genesis Design System tokens for consistent theming:

```css
/* Tab spacing using Genesis tokens */
.tab-trigger {
  padding: var(--gd-spacing-12) var(--gd-spacing-16);
  gap: var(--gd-spacing-8);
}

/* Typography using Genesis scales */
.tab-label {
  font-size: var(--gd-text-body-m);
  line-height: var(--gd-line-height-m);
}

/* Colors using Genesis color tokens */
.tab-active {
  color: var(--gd-color-primary-50);
  border-bottom-color: var(--gd-color-primary-50);
}

.tab-hover {
  background-color: var(--gd-color-neutral-10);
}
```

### Theme Support

```tsx
// Automatic theme adaptation
<div className="theme-light">
  <Tabs items={items} kind="default" />
</div>

<div className="theme-dark">
  <Tabs items={items} kind="default" />
</div>
```

## Best Practices

### Performance Optimization

```tsx
// Memoize tab items to prevent unnecessary re-renders
const tabItems = useMemo(
  () => [
    {
      value: "heavy-content",
      label: "Heavy Content",
      content: <ExpensiveComponent />,
    },
  ],
  [dependencies]
);

// Lazy load tab content
const LazyTabContent = lazy(() => import("./LazyTabContent"));

const optimizedItems = [
  {
    value: "lazy",
    label: "Lazy Tab",
    content: (
      <Suspense fallback={<Spinner />}>
        <LazyTabContent />
      </Suspense>
    ),
  },
];
```

### State Management

```tsx
// Use context for complex tab state
const TabsContext = createContext();

const TabsProvider = ({ children }) => {
  const [tabs, setTabs] = useState([]);
  const [activeTab, setActiveTab] = useState(null);

  const addTab = useCallback(tab => {
    setTabs(prev => [...prev, tab]);
  }, []);

  const removeTab = useCallback(tabValue => {
    setTabs(prev => prev.filter(tab => tab.value !== tabValue));
  }, []);

  return (
    <TabsContext.Provider value={{ tabs, activeTab, addTab, removeTab }}>
      {children}
    </TabsContext.Provider>
  );
};
```

### UX Guidelines

- Keep tab labels concise (ideally 1-2 words)
- Provide visual feedback for interactive actions
- Use loading states for asynchronous content
- Group related tabs logically
- Consider mobile responsiveness for many tabs
- Provide clear visual hierarchy with icons and counters

```tsx
// Good tab labeling
const wellLabeledTabs = [
  { value: "overview", label: "Overview" },
  { value: "analytics", label: "Analytics" },
  { value: "settings", label: "Settings" },
];

// Avoid overly long labels
const poorLabels = [
  { value: "overview", label: "Comprehensive Overview Dashboard" },
  { value: "analytics", label: "Advanced Analytics and Reporting" },
];
```

## Common Pitfalls and Troubleshooting

### Content Not Updating

```tsx
// ❌ Incorrect: Mutating items array directly
const handleUpdate = () => {
  items[0].content = newContent; // Direct mutation
  setItems(items);
};

// ✅ Correct: Create new array/objects
const handleUpdate = () => {
  setItems(prev =>
    prev.map(item => (item.value === targetValue ? { ...item, content: newContent } : item))
  );
};
```

### Context Menu Not Appearing

```tsx
// ❌ Missing enableTabContextMenu or individual permissions
<Tabs
  items={items}
  onTabRename={handleRename}
  // Missing enableTabContextMenu={true}
/>

// ✅ Correct: Enable context menu and provide handlers
<Tabs
  items={items}
  enableTabContextMenu
  onTabRename={handleRename}
  onTabDuplicate={handleDuplicate}
  onTabDelete={handleDelete}
/>
```

### Performance Issues with Many Tabs

```tsx
// ❌ Rendering all tab content at once
const heavyTabs = Array.from({ length: 50 }, (_, i) => ({
  value: `tab-${i}`,
  label: `Tab ${i}`,
  content: <HeavyComponent data={data[i]} />, // All rendered
}));

// ✅ Lazy load content only when needed
const optimizedTabs = Array.from({ length: 50 }, (_, i) => ({
  value: `tab-${i}`,
  label: `Tab ${i}`,
  content: <LazyTabContent tabId={i} />,
}));
```

### Accessibility Issues

```tsx
// ❌ Missing proper labeling
<Tabs items={items} />

// ✅ Proper accessibility attributes
<Tabs
  items={items}
  aria-label="Main navigation tabs"
  className="focus-visible:ring-2 focus-visible:ring-primary"
/>
```

## Migration Guide

### From Legacy Tab Components

```tsx
// Legacy component
<TabsLegacy>
  <TabPanel label="Tab 1">Content 1</TabPanel>
  <TabPanel label="Tab 2">Content 2</TabPanel>
</TabsLegacy>

// New Tabs component
<Tabs
  items={[
    { value: 'tab1', label: 'Tab 1', content: 'Content 1' },
    { value: 'tab2', label: 'Tab 2', content: 'Content 2' }
  ]}
  defaultValue="tab1"
/>
```

### Adding Interactive Features

```tsx
// Basic tabs
<Tabs items={basicItems} />

// Enhanced with context menu
<Tabs
  items={enhancedItems.map(item => ({
    ...item,
    canRename: true,
    canDuplicate: true,
    canDelete: item.value !== 'protected'
  }))}
  enableTabContextMenu
  onTabRename={handleRename}
  onTabDuplicate={handleDuplicate}
  onTabDelete={handleDelete}
/>
```

### TypeScript Migration

```tsx
// Define proper types
interface CustomTabItem extends TabItem {
  metadata?: Record<string, any>;
  permissions?: {
    edit: boolean;
    delete: boolean;
  };
}

const typedTabs: CustomTabItem[] = [
  {
    value: "admin",
    label: "Admin Panel",
    content: <AdminPanel />,
    metadata: { role: "admin" },
    permissions: { edit: true, delete: false },
  },
];
```

The Tabs component provides a robust foundation for organizing content with extensive customization options, accessibility features, and interactive capabilities. Its integration with the Genesis Design System ensures consistent theming and behavior across your application while maintaining flexibility for complex use cases.
