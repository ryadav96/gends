# Title Bar Component

## Overview

The Title Bar component is a flexible header layout component designed to provide consistent structure for application headers, modal headers, and navigation bars. Built with Genesis Design System tokens, it offers three distinct content areas (start, center, end) with customizable background variants and responsive spacing. Perfect for dashboards, modal dialogs, page headers, and any interface requiring structured header content with accessibility support.

## Component API

### TitleBar Props

| Prop            | Type                                   | Default     | Description                            |
| --------------- | -------------------------------------- | ----------- | -------------------------------------- |
| `variant`       | `'default' \| 'withBackground'`        | `'default'` | Background styling variant             |
| `startContent`  | `React.ReactNode`                      | -           | Left-aligned content area              |
| `centerContent` | `React.ReactNode`                      | -           | Center-aligned content area (optional) |
| `endContent`    | `React.ReactNode`                      | -           | Right-aligned content area             |
| `disabled`      | `boolean`                              | `false`     | Disables interactive elements          |
| `className`     | `string`                               | -           | Additional CSS classes                 |
| `...props`      | `React.HTMLAttributes<HTMLDivElement>` | -           | Standard HTML div element props        |

### Variant Options

The Title Bar offers two styling variants for different use cases:

| Variant          | Background    | Border | Use Cases                    |
| ---------------- | ------------- | ------ | ---------------------------- |
| `default`        | Transparent   | None   | In-page headers, dashboards  |
| `withBackground` | Surface color | Bottom | Modal headers, panel headers |

## Content Areas

The Title Bar provides three flexible content sections with built-in spacing and alignment:

### Start Content (Left-aligned)

- **Primary content area** for titles, logos, and navigation
- **Typical elements**: Headings, back buttons, avatars, breadcrumbs
- **Built-in spacing**: 12px gap between child elements

### Center Content (Center-aligned)

- **Optional centered content** for navigation or status indicators
- **Typical elements**: Tab navigation, status badges, search bars
- **Responsive behavior**: Maintains center alignment across screen sizes

### End Content (Right-aligned)

- **Action area** for buttons, menus, and controls
- **Typical elements**: Action buttons, dropdown menus, settings
- **Built-in spacing**: 16px gap between child elements

## Basic Usage

### Simple Title Bar

```tsx
import { TitleBar, Button, IconButton } from "gends";
import { IcArrowBack, IcMoreHorizontal } from "gends";

const BasicExample = () => {
  return (
    <TitleBar
      startContent={<h2 className="text-en-desktop-heading-2xl">Page Title</h2>}
      endContent={
        <div className="flex items-center gap-4">
          <Button kind="secondary" size="s">
            Cancel
          </Button>
          <Button kind="primary" size="s">
            Save
          </Button>
        </div>
      }
    />
  );
};
```

### Title Bar with Back Navigation

```tsx
const NavigationExample = () => {
  const handleBack = () => {
    console.log("Navigate back");
  };

  return (
    <TitleBar
      startContent={
        <div className="flex items-center gap-6">
          <IconButton
            icon={<IcArrowBack size="20px" />}
            onClick={handleBack}
            size="lg"
            type="tertiary"
          />
          <h2 className="text-en-desktop-heading-2xl">Settings</h2>
        </div>
      }
      endContent={<IconButton icon={<IcMoreHorizontal size="20px" />} size="lg" type="tertiary" />}
    />
  );
};
```

## Variant Examples

### Default Variant

Transparent background for in-page headers and dashboards.

```tsx
const DefaultVariantExample = () => (
  <TitleBar
    variant="default"
    startContent={
      <div className="flex items-center gap-3">
        <h1 className="text-en-desktop-heading-2xl">Dashboard</h1>
      </div>
    }
    endContent={
      <div className="flex items-center gap-4">
        <Button kind="tertiary" size="s">
          Export
        </Button>
        <Button kind="primary" size="s">
          New Item
        </Button>
      </div>
    }
  />
);
```

### With Background Variant

Surface background with bottom border for modal headers and elevated content.

```tsx
const BackgroundVariantExample = () => (
  <TitleBar
    variant="withBackground"
    startContent={<h2 className="text-en-desktop-heading-2xl">Edit Profile</h2>}
    endContent={
      <div className="flex items-center gap-3">
        <Button kind="tertiary" size="s">
          Cancel
        </Button>
        <Button kind="primary" size="s">
          Save Changes
        </Button>
      </div>
    }
  />
);
```

## Advanced Features

### Three-Section Layout

```tsx
const ThreeSectionExample = () => {
  const [activeTab, setActiveTab] = useState("overview");

  return (
    <TitleBar
      variant="withBackground"
      startContent={
        <div className="flex items-center gap-4">
          <IconButton icon={<IcArrowBack size="20px" />} size="lg" type="tertiary" />
          <h2 className="text-en-desktop-heading-2xl">Project Details</h2>
        </div>
      }
      centerContent={
        <nav className="flex gap-6">
          {["overview", "tasks", "team", "settings"].map(tab => (
            <button
              key={tab}
              onClick={() => setActiveTab(tab)}
              className={`px-3 py-2 text-sm font-medium rounded-md transition-colors ${
                activeTab === tab
                  ? "bg-color-primary-10 text-color-primary-60"
                  : "text-color-neutral-grey-80 hover:text-color-primary-50"
              }`}
            >
              {tab.charAt(0).toUpperCase() + tab.slice(1)}
            </button>
          ))}
        </nav>
      }
      endContent={
        <div className="flex items-center gap-3">
          <Button kind="tertiary" size="s">
            Share
          </Button>
          <Button kind="secondary" size="s">
            Edit
          </Button>
        </div>
      }
    />
  );
};
```

### Complex Header with Multiple Elements

```tsx
const ComplexHeaderExample = () => {
  const [isToggleOn, setIsToggleOn] = useState(false);

  return (
    <TitleBar
      variant="withBackground"
      startContent={
        <div className="flex items-center gap-3">
          <IconButton icon={<IcArrowBack size="20px" />} size="lg" type="tertiary" />
          <Avatar color="navi" initials="JD" size="sm" />
          <div className="flex items-center gap-2">
            <h2 className="text-en-desktop-heading-2xl">John Doe's Profile</h2>
            <IconButton icon={<IcEditPen size="16px" />} size="sm" type="tertiary" />
          </div>
          <Badge appearance="Neutral" text="Admin" size="m" />
        </div>
      }
      endContent={
        <div className="flex items-center gap-4">
          <Toggle
            id="notifications"
            label="Notifications"
            labelPosition="left"
            checked={isToggleOn}
            onChange={() => setIsToggleOn(!isToggleOn)}
            size="lg"
          />
          <IconButton icon={<IcMoreHorizontal size="20px" />} size="lg" type="tertiary" />
          <Button kind="secondary" size="s">
            Export
          </Button>
          <Button kind="primary" size="s">
            Save
          </Button>
        </div>
      }
    />
  );
};
```

### Disabled State

```tsx
const DisabledExample = () => (
  <TitleBar
    disabled
    startContent={
      <div className="flex items-center gap-3">
        <Button
          kind="tertiary"
          prefixIcon={<IcExport className="-rotate-90" />}
          disabled
          className="text-color-neutral-grey-80"
        >
          Back
        </Button>
        <span className="w-px h-10 bg-color-neutral-grey-40" />
        <h2 className="text-en-desktop-heading-2xl text-color-neutral-grey-60">Disabled Page</h2>
      </div>
    }
    endContent={
      <div className="flex items-center gap-3">
        <Button kind="secondary" size="s" disabled>
          Secondary
        </Button>
        <Button kind="primary" size="s" disabled>
          Primary
        </Button>
      </div>
    }
  />
);
```

## Real-World Examples

### 1. Application Dashboard Header

```tsx
const DashboardHeader = () => {
  const [user, setUser] = useState({ name: "Alice Johnson", role: "Admin" });
  const [notifications, setNotifications] = useState(3);

  return (
    <TitleBar
      variant="default"
      startContent={
        <div className="flex items-center gap-4">
          <h1 className="text-en-desktop-heading-2xl">Dashboard</h1>
          <Badge appearance="Primary" text={`${notifications} new`} size="s" />
        </div>
      }
      endContent={
        <div className="flex items-center gap-4">
          <Button kind="tertiary" size="s" prefixIcon={<IcExport />}>
            Export Data
          </Button>
          <Button kind="secondary" size="s">
            Settings
          </Button>
          <div className="flex items-center gap-2">
            <Avatar initials="AJ" size="sm" />
            <div className="text-sm">
              <div className="font-medium">{user.name}</div>
              <div className="text-color-neutral-grey-70">{user.role}</div>
            </div>
          </div>
        </div>
      }
    />
  );
};
```

### 2. Modal Dialog Header

```tsx
const ModalHeader = ({ onClose, onSave, title, hasChanges }) => {
  return (
    <TitleBar
      variant="withBackground"
      startContent={
        <div className="flex items-center gap-2">
          <h2 className="text-en-desktop-heading-2xl">{title}</h2>
          {hasChanges && <Badge appearance="Warning" text="Unsaved" size="s" />}
        </div>
      }
      endContent={
        <div className="flex items-center gap-3">
          <Button kind="tertiary" size="s" onClick={onClose}>
            Cancel
          </Button>
          <Button kind="primary" size="s" onClick={onSave} disabled={!hasChanges}>
            Save Changes
          </Button>
          <IconButton icon={<IcClose size="20px" />} onClick={onClose} size="sm" type="tertiary" />
        </div>
      }
    />
  );
};
```

### 3. E-commerce Product Page Header

```tsx
const ProductPageHeader = ({ product, onBack, onShare, onAddToCart }) => {
  const [isFavorite, setIsFavorite] = useState(product.isFavorite);

  return (
    <TitleBar
      variant="default"
      startContent={
        <div className="flex items-center gap-4">
          <IconButton
            icon={<IcArrowBack size="20px" />}
            onClick={onBack}
            size="lg"
            type="tertiary"
          />
          <div>
            <h1 className="text-en-desktop-heading-2xl">{product.name}</h1>
            <div className="flex items-center gap-2 mt-1">
              <Badge appearance="Success" text={product.category} size="s" />
              <span className="text-sm text-color-neutral-grey-70">SKU: {product.sku}</span>
            </div>
          </div>
        </div>
      }
      endContent={
        <div className="flex items-center gap-3">
          <div className="text-right">
            <div className="text-2xl font-bold text-color-primary-60">${product.price}</div>
            <div className="text-sm text-color-neutral-grey-70">{product.stock} in stock</div>
          </div>
          <IconButton
            icon={<IcHeart size="20px" />}
            onClick={() => setIsFavorite(!isFavorite)}
            size="lg"
            type="tertiary"
            className={isFavorite ? "text-color-error-50" : ""}
          />
          <Button kind="tertiary" size="s" onClick={onShare}>
            Share
          </Button>
          <Button kind="primary" size="s" onClick={onAddToCart} disabled={product.stock === 0}>
            Add to Cart
          </Button>
        </div>
      }
    />
  );
};
```

### 4. Content Management System Header

```tsx
const CMSHeader = ({ document, onSave, onPublish, onPreview }) => {
  const [status, setStatus] = useState(document.status);
  const [lastSaved, setLastSaved] = useState(document.lastSaved);

  const handleSave = async () => {
    await onSave();
    setLastSaved(new Date());
  };

  const getStatusBadge = () => {
    const appearances = {
      draft: "Neutral",
      review: "Warning",
      published: "Success",
    };

    return (
      <Badge
        appearance={appearances[status]}
        text={status.charAt(0).toUpperCase() + status.slice(1)}
        size="m"
      />
    );
  };

  return (
    <TitleBar
      variant="withBackground"
      startContent={
        <div className="flex items-center gap-4">
          <div>
            <h1 className="text-en-desktop-heading-2xl">{document.title}</h1>
            <div className="flex items-center gap-3 mt-1">
              {getStatusBadge()}
              <span className="text-sm text-color-neutral-grey-70">
                Last saved: {lastSaved.toLocaleTimeString()}
              </span>
            </div>
          </div>
        </div>
      }
      centerContent={
        <nav className="flex gap-4">
          <button className="px-3 py-2 text-sm font-medium text-color-primary-60 border-b-2 border-color-primary-60">
            Content
          </button>
          <button className="px-3 py-2 text-sm font-medium text-color-neutral-grey-70 hover:text-color-primary-50">
            SEO
          </button>
          <button className="px-3 py-2 text-sm font-medium text-color-neutral-grey-70 hover:text-color-primary-50">
            Settings
          </button>
        </nav>
      }
      endContent={
        <div className="flex items-center gap-3">
          <Button kind="tertiary" size="s" onClick={onPreview}>
            Preview
          </Button>
          <Button kind="secondary" size="s" onClick={handleSave}>
            Save Draft
          </Button>
          <Button kind="primary" size="s" onClick={onPublish} disabled={status === "published"}>
            {status === "published" ? "Published" : "Publish"}
          </Button>
        </div>
      }
    />
  );
};
```

### 5. Data Analysis Tool Header

```tsx
const AnalyticsHeader = ({ dataset, onRefresh, onExport, onFilter }) => {
  const [isAutoRefresh, setIsAutoRefresh] = useState(false);
  const [refreshInterval, setRefreshInterval] = useState(30);

  return (
    <TitleBar
      variant="default"
      startContent={
        <div className="flex items-center gap-4">
          <h1 className="text-en-desktop-heading-2xl">Analytics Dashboard</h1>
          <div className="flex items-center gap-2">
            <Badge appearance="Primary" text={dataset.name} size="m" />
            <span className="text-sm text-color-neutral-grey-70">
              {dataset.recordCount.toLocaleString()} records
            </span>
          </div>
        </div>
      }
      centerContent={
        <div className="flex items-center gap-4">
          <Toggle
            id="auto-refresh"
            label={`Auto-refresh (${refreshInterval}s)`}
            labelPosition="left"
            checked={isAutoRefresh}
            onChange={setIsAutoRefresh}
            size="md"
          />
          <select
            value={refreshInterval}
            onChange={e => setRefreshInterval(Number(e.target.value))}
            className="px-2 py-1 border rounded text-sm"
            disabled={!isAutoRefresh}
          >
            <option value={15}>15s</option>
            <option value={30}>30s</option>
            <option value={60}>1m</option>
            <option value={300}>5m</option>
          </select>
        </div>
      }
      endContent={
        <div className="flex items-center gap-3">
          <Button kind="tertiary" size="s" onClick={onFilter}>
            Filters
          </Button>
          <Button kind="tertiary" size="s" onClick={onRefresh} prefixIcon={<IcRefresh />}>
            Refresh
          </Button>
          <Button kind="secondary" size="s" onClick={onExport} prefixIcon={<IcExport />}>
            Export
          </Button>
        </div>
      }
    />
  );
};
```

## Accessibility Features

The Title Bar component includes comprehensive accessibility support:

### Keyboard Navigation

- **Tab**: Navigate through interactive elements in logical order
- **Enter/Space**: Activate buttons and interactive elements
- **Escape**: Close dropdown menus or modal dialogs (when applicable)

### Screen Reader Support

- Proper heading hierarchy with semantic HTML elements
- ARIA labels for icon-only buttons
- Descriptive text for status indicators and badges
- Landmark roles for navigation areas

### Visual Accessibility

- High contrast ratios for all text and interactive elements
- Clear focus indicators using Genesis design tokens
- Consistent spacing for touch targets (minimum 44px)
- Color-blind friendly status indicators

```tsx
// Accessibility-focused implementation
<TitleBar
  variant="withBackground"
  startContent={
    <h1 className="text-en-desktop-heading-2xl" id="page-title">
      Dashboard Overview
    </h1>
  }
  endContent={
    <div className="flex items-center gap-3">
      <Button kind="tertiary" size="s" aria-label="Export dashboard data">
        Export
      </Button>
      <Button kind="primary" size="s">
        New Report
      </Button>
    </div>
  }
  role="banner"
  aria-labelledby="page-title"
/>
```

## Genesis Design System Integration

### Design Tokens

The Title Bar leverages Genesis design tokens for consistent theming:

```tsx
// CSS custom properties used internally
const titleBarTokens = {
  // Background colors
  backgroundDefault: "transparent",
  backgroundWithBackground: "var(--gd-background-surface-0)",

  // Border colors
  border: "var(--gd-border-default)",

  // Spacing
  paddingHorizontal: "var(--gd-spacing-16)",
  paddingVertical: "var(--gd-spacing-12)",
  gapStart: "var(--gd-spacing-12)",
  gapEnd: "var(--gd-spacing-16)",

  // Typography
  headingColor: "var(--gd-text-default)",
  subtitleColor: "var(--gd-text-subdued-1)",
};
```

### Component Integration

```tsx
// Seamless integration with other Genesis components
const IntegratedExample = () => (
  <TitleBar
    variant="withBackground"
    startContent={
      <div className="flex items-center gap-3">
        <Avatar color="primary" initials="GD" size="sm" />
        <h2 className="text-en-desktop-heading-2xl">Genesis Dashboard</h2>
      </div>
    }
    endContent={
      <div className="flex items-center gap-3">
        <Dropdown trigger={<Button kind="tertiary">Options</Button>}>
          <DropdownItem>Settings</DropdownItem>
          <DropdownItem>Help</DropdownItem>
        </Dropdown>
        <Button kind="primary" size="s">
          Create New
        </Button>
      </div>
    }
  />
);
```

## Best Practices

### Content Organization

```tsx
// ✅ Good: Logical content hierarchy
<TitleBar
  startContent={
    <div className="flex items-center gap-3">
      <IconButton icon={<IcBack />} />  {/* Navigation first */}
      <h1>Page Title</h1>              {/* Title second */}
      <Badge text="Status" />          {/* Status indicator */}
    </div>
  }
  endContent={
    <div className="flex items-center gap-3">
      <Button kind="tertiary">Secondary</Button>  {/* Less important actions */}
      <Button kind="primary">Primary</Button>     {/* Primary action last */}
    </div>
  }
/>

// ❌ Avoid: Inconsistent spacing and hierarchy
<TitleBar
  startContent={
    <div style={{ display: 'flex', gap: '8px' }}>  {/* Inconsistent spacing */}
      <h1>Title</h1>
      <IconButton icon={<IcBack />} />              {/* Wrong order */}
    </div>
  }
/>
```

### Performance Optimization

```tsx
// ✅ Good: Memoized components for better performance
const OptimizedTitleBar = memo(() => {
  const startContent = useMemo(
    () => (
      <div className="flex items-center gap-3">
        <h1 className="text-en-desktop-heading-2xl">Dashboard</h1>
      </div>
    ),
    []
  );

  const endContent = useMemo(
    () => (
      <div className="flex items-center gap-3">
        <Button kind="primary" size="s">
          Action
        </Button>
      </div>
    ),
    []
  );

  return <TitleBar startContent={startContent} endContent={endContent} />;
});
```

### Responsive Design

```tsx
// ✅ Good: Mobile-responsive title bar
const ResponsiveTitleBar = () => {
  const [isMobile, setIsMobile] = useState(false);

  useEffect(() => {
    const checkMobile = () => setIsMobile(window.innerWidth < 768);
    checkMobile();
    window.addEventListener("resize", checkMobile);
    return () => window.removeEventListener("resize", checkMobile);
  }, []);

  return (
    <TitleBar
      startContent={
        <div className="flex items-center gap-3">
          {isMobile && <IconButton icon={<IcMenu />} />}
          <h1 className={isMobile ? "text-lg" : "text-en-desktop-heading-2xl"}>
            {isMobile ? "Dashboard" : "Analytics Dashboard"}
          </h1>
        </div>
      }
      endContent={
        <div className="flex items-center gap-2">
          {!isMobile && (
            <Button kind="tertiary" size="s">
              Export
            </Button>
          )}
          <Button kind="primary" size={isMobile ? "s" : "m"}>
            {isMobile ? "New" : "Create New"}
          </Button>
        </div>
      }
    />
  );
};
```

## Common Pitfalls & Troubleshooting

### Content Overflow

```tsx
// ❌ Problem: Content overflow on small screens
<TitleBar
  startContent={
    <h1 className="text-en-desktop-heading-2xl whitespace-nowrap">
      Very Long Title That Might Overflow On Small Screens
    </h1>
  }
/>

// ✅ Solution: Responsive text truncation
<TitleBar
  startContent={
    <h1 className="text-en-desktop-heading-2xl truncate max-w-md">
      Very Long Title That Might Overflow On Small Screens
    </h1>
  }
/>
```

### Missing Accessibility Labels

```tsx
// ❌ Problem: Icon buttons without labels
<TitleBar
  endContent={
    <IconButton icon={<IcClose />} onClick={handleClose} />
  }
/>

// ✅ Solution: Proper accessibility labels
<TitleBar
  endContent={
    <IconButton
      icon={<IcClose />}
      onClick={handleClose}
      aria-label="Close dialog"
    />
  }
/>
```

### Inconsistent Button Grouping

```tsx
// ❌ Problem: Inconsistent spacing and grouping
<TitleBar
  endContent={
    <>
      <Button kind="tertiary">Cancel</Button>
      <span style={{ margin: '0 8px' }} />
      <Button kind="primary">Save</Button>
    </>
  }
/>

// ✅ Solution: Proper container with consistent spacing
<TitleBar
  endContent={
    <div className="flex items-center gap-3">
      <Button kind="tertiary">Cancel</Button>
      <Button kind="primary">Save</Button>
    </div>
  }
/>
```

## Migration Guide

### From Custom Headers

```tsx
// Legacy custom header
<div className="flex justify-between items-center p-4 border-b">
  <h1>Page Title</h1>
  <button>Action</button>
</div>

// Migrate to Genesis Title Bar
<TitleBar
  variant="withBackground"
  startContent={<h1 className="text-en-desktop-heading-2xl">Page Title</h1>}
  endContent={<Button kind="primary">Action</Button>}
/>
```

### From Other Header Libraries

```tsx
// React Header component example
<Header
  left={<BackButton />}
  center={<Title>Page</Title>}
  right={<ActionButton />}
/>

// Genesis Title Bar equivalent
<TitleBar
  startContent={<IconButton icon={<IcBack />} />}
  centerContent={<h2 className="text-en-desktop-heading-2xl">Page</h2>}
  endContent={<Button kind="primary">Action</Button>}
/>
```

### TypeScript Integration

```tsx
interface HeaderData {
  title: string;
  subtitle?: string;
  actions: Array<{
    label: string;
    onClick: () => void;
    kind: "primary" | "secondary" | "tertiary";
  }>;
}

const TypedTitleBar: React.FC<{ data: HeaderData }> = ({ data }) => {
  return (
    <TitleBar
      startContent={
        <div>
          <h1 className="text-en-desktop-heading-2xl">{data.title}</h1>
          {data.subtitle && <p className="text-sm text-color-neutral-grey-70">{data.subtitle}</p>}
        </div>
      }
      endContent={
        <div className="flex items-center gap-3">
          {data.actions.map((action, index) => (
            <Button key={index} kind={action.kind} size="s" onClick={action.onClick}>
              {action.label}
            </Button>
          ))}
        </div>
      }
    />
  );
};
```

## Conclusion

The Genesis Title Bar component provides a flexible, accessible foundation for application headers across various contexts. Its three-section layout, variant options, and seamless integration with other Genesis components make it suitable for everything from simple page headers to complex dashboard navigation. The component's adherence to design system tokens ensures consistent theming while its accessibility features guarantee inclusive user experiences across all platforms and user needs.
