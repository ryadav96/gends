# Icon Component

## Overview

The Icon component is a foundational element in the Genesis Design System (Gends) that provides access to a comprehensive library of over 500 SVG icons. Designed for consistency, accessibility, and flexibility, the Icon component supports customizable sizing, colors, and styling while maintaining optimal performance and visual quality across all themes and devices.

The component includes both general-purpose icons and specialized document icons for file type representation, making it suitable for everything from UI elements to file management interfaces.

## Component API

### Icon Props

| Prop        | Type                            | Default  | Description                                        |
| ----------- | ------------------------------- | -------- | -------------------------------------------------- |
| `size`      | `string`                        | `"24px"` | Sets the width and height of the icon              |
| `color`     | `string`                        | `"#000"` | Changes the fill/stroke color of the icon          |
| `className` | `string`                        | `""`     | Additional Tailwind CSS classes for styling        |
| `style`     | `React.CSSProperties`           | `{}`     | Inline styles for further customization            |
| `...props`  | `React.SVGProps<SVGSVGElement>` | `{}`     | All standard SVG element properties and attributes |

### Document Icon Props

Document icons have the same props structure but with a default size of `"28px"`:

| Prop        | Type                            | Default  | Description                                        |
| ----------- | ------------------------------- | -------- | -------------------------------------------------- |
| `size`      | `string`                        | `"28px"` | Sets the width and height of the document icon     |
| `className` | `string`                        | `""`     | Additional Tailwind CSS classes for styling        |
| `...props`  | `React.SVGProps<SVGSVGElement>` | `{}`     | All standard SVG element properties and attributes |

## Basic Usage

```tsx
import { IcAdd, IcSearch, IcUser } from "gends";

// Basic icon with default props
<IcAdd />

// Icon with custom size and color
<IcSearch size="32px" color="#3B82F6" />

// Icon with Tailwind classes
<IcUser className="w-6 h-6 text-blue-500" />

// Icon with inline styles
<IcAdd style={{ width: "20px", height: "20px", color: "red" }} />
```

## Size Variants

Icons are designed to work optimally at specific sizes. While you can use any size, these are the recommended standard sizes:

| Size   | Use Case                          | Example Usage                |
| ------ | --------------------------------- | ---------------------------- |
| `16px` | Small inline icons, form inputs   | `<IcAdd size="16px" />`      |
| `20px` | Button icons, navigation items    | `<IcSearch size="20px" />`   |
| `24px` | Default size, toolbar icons       | `<IcUser />` (default)       |
| `32px` | Larger interactive elements       | `<IcMenu size="32px" />`     |
| `48px` | Feature highlights, empty states  | `<IcDocument size="48px" />` |
| `64px` | Hero sections, prominent displays | `<IcCloud size="64px" />`    |

```tsx
// Size examples
<IcAdd size="16px" />  {/* Small */}
<IcAdd size="20px" />  {/* Medium */}
<IcAdd />              {/* Default: 24px */}
<IcAdd size="32px" />  {/* Large */}
<IcAdd size="48px" />  {/* XL */}
<IcAdd size="64px" />  {/* XXL */}
```

## Color Customization

Icons support multiple ways to customize colors:

### Using the color prop

```tsx
<IcAdd color="#3B82F6" />        {/* Blue */}
<IcAdd color="#EF4444" />        {/* Red */}
<IcAdd color="#10B981" />        {/* Green */}
<IcAdd color="currentColor" />   {/* Inherits text color */}
```

### Using Tailwind CSS classes

```tsx
<IcAdd className="text-blue-500" />
<IcAdd className="text-red-600" />
<IcAdd className="text-green-500" />
<IcAdd className="text-gray-700 dark:text-gray-300" />
```

### Using CSS custom properties

```tsx
<IcAdd style={{ color: "var(--primary-color)" }} />
<IcAdd className="text-[var(--accent-color)]" />
```

## Available Icon Categories

The Genesis Design System includes over 500 icons organized into the following categories:

### User Interface Icons

- **Navigation**: `IcArrowLeft`, `IcArrowRight`, `IcArrowUp`, `IcArrowDown`, `IcChevronLeft`, `IcChevronRight`
- **Actions**: `IcAdd`, `IcEdit`, `IcDelete`, `IcSave`, `IcCancel`, `IcConfirm`, `IcCopy`, `IcPaste`
- **Toggles**: `IcVisible`, `IcVisibleOff`, `IcExpand`, `IcCollapse`, `IcMenu`, `IcClose`

### Content Icons

- **Media**: `IcPlay`, `IcPause`, `IcStop`, `IcVideo`, `IcImage`, `IcAudio`, `IcCamera`
- **Files**: `IcFolder`, `IcFile`, `IcDownload`, `IcUpload`, `IcAttachment`, `IcLink`
- **Text**: `IcText`, `IcTextAlign`, `IcBold`, `IcItalic`, `IcUnderline`

### Communication Icons

- **Messaging**: `IcMessage`, `IcChat`, `IcNotification`, `IcBell`, `IcMail`, `IcSend`
- **Social**: `IcShare`, `IcLike`, `IcComment`, `IcBookmark`, `IcFollow`
- **Calls**: `IcPhone`, `IcVideoCall`, `IcMicrophone`, `IcMicrophoneOff`

### System Icons

- **Status**: `IcSuccess`, `IcError`, `IcWarning`, `IcInfo`, `IcLoading`, `IcSync`
- **Settings**: `IcSettings`, `IcFilter`, `IcSort`, `IcSearch`, `IcRefresh`
- **Security**: `IcLock`, `IcUnlock`, `IcShield`, `IcKey`, `IcPrivacy`

### Business Icons

- **Finance**: `IcMoney`, `IcCard`, `IcWallet`, `IcChart`, `IcTrend`, `IcCalculator`
- **Shopping**: `IcCart`, `IcBag`, `IcProduct`, `IcStore`, `IcPayment`, `IcReceipt`
- **Analytics**: `IcGraph`, `IcReport`, `IcStatistics`, `IcDashboard`, `IcMetrics`

### Technology Icons

- **Devices**: `IcMobile`, `IcDesktop`, `IcTablet`, `IcWatch`, `IcTv`, `IcHeadphones`
- **Network**: `IcWifi`, `IcBluetooth`, `IcSignal`, `IcNetwork`, `IcCloud`, `IcDatabase`
- **Development**: `IcCode`, `IcTerminal`, `IcBug`, `IcGit`, `IcApi`, `IcWebhook`

## Document Icons

Specialized icons for file type representation with automatic file extension detection:

### Available Document Types

```tsx
import {
  DocIcon,          // .doc files
  DocxIcon,         // .docx files
  PdfIcon,          // .pdf files
  XlsIcon,          // .xls files
  XlsxIcon,         // .xlsx files
  CsvIcon,          // .csv files
  TxtIcon,          // .txt files
  DocumentIcon,     // Generic/unknown files
  getDocIconByExtension
} from "gends";

// Direct usage
<DocIcon size="32px" />
<PdfIcon size="32px" />
<XlsxIcon size="32px" />

// Dynamic icon selection
const FileIcon = getDocIconByExtension("pdf");
<FileIcon size="32px" />
```

### Document Icon Helper Function

```tsx
// Automatically select the correct icon based on file extension
const getIconForFile = (filename: string) => {
  const extension = filename.split(".").pop() || "";
  const IconComponent = getDocIconByExtension(extension);
  return <IconComponent size="24px" />;
};

// Usage
{
  getIconForFile("document.pdf");
} // Returns PdfIcon
{
  getIconForFile("spreadsheet.xlsx");
} // Returns XlsxIcon
{
  getIconForFile("unknown.xyz");
} // Returns DocumentIcon
```

## Interactive Examples

### Button with Icons

```tsx
import { Button, IcAdd, IcDownload } from "gends";

<Button prefixIcon={<IcAdd size="16px" />}>
  Add Item
</Button>

<Button suffixIcon={<IcDownload size="16px" />}>
  Download
</Button>
```

### Icon with Hover Effects

```tsx
<IcHeart
  className="w-6 h-6 text-gray-400 hover:text-red-500 transition-colors cursor-pointer"
  onClick={() => handleLike()}
/>
```

### Responsive Icon Sizing

```tsx
<IcMenu className="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6" />
```

### Icon in Form Fields

```tsx
<div className="relative">
  <input className="pl-10 pr-4 py-2 border rounded" />
  <IcSearch
    size="20px"
    className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400"
  />
</div>
```

## Advanced Usage Patterns

### Icon Library Showcase

```tsx
import * as Icons from "gends";

const IconShowcase = () => {
  const [search, setSearch] = useState("");

  const iconEntries = Object.entries(Icons).filter(
    ([name]) => name.startsWith("Ic") && name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div className="grid grid-cols-6 gap-4">
      {iconEntries.map(([name, Icon]) => (
        <div key={name} className="flex flex-col items-center p-2">
          <Icon className="w-8 h-8 text-gray-600" />
          <span className="text-xs mt-1">{name}</span>
        </div>
      ))}
    </div>
  );
};
```

### Dynamic Icon Loading

```tsx
const DynamicIcon = ({ iconName, ...props }) => {
  const IconComponent = Icons[iconName];

  if (!IconComponent) {
    return <IcQuestion {...props} />; // Fallback icon
  }

  return <IconComponent {...props} />;
};

// Usage
<DynamicIcon iconName="IcAdd" size="24px" />;
```

### Icon with Tooltip

```tsx
import { Tooltip } from "gends";

<Tooltip content="Add new item">
  <IcAdd size="20px" className="text-blue-500 cursor-pointer hover:text-blue-600" />
</Tooltip>;
```

## Best Practices

### Accessibility

- **Always provide meaningful context**: Use `aria-label` or `aria-labelledby` for interactive icons
- **Use semantic markup**: Wrap clickable icons in buttons with proper ARIA attributes
- **Consider screen readers**: Icons should complement, not replace, text labels
- **Maintain focus visibility**: Ensure interactive icons have clear focus states

```tsx
// Good: Accessible icon button
<button aria-label="Add new item" className="p-2 rounded focus:ring-2">
  <IcAdd size="20px" />
</button>

// Good: Icon with text label
<div className="flex items-center gap-2">
  <IcUser size="16px" />
  <span>Profile</span>
</div>

// Avoid: Icon-only button without accessibility
<IcAdd onClick={handleAdd} />
```

### Performance

- **Use consistent sizing**: Stick to standard sizes to leverage browser caching
- **Minimize inline styles**: Prefer CSS classes over inline styles for better performance
- **Consider icon fonts for very large sets**: For applications with hundreds of icons, consider icon fonts

### Visual Design

- **Maintain visual hierarchy**: Use size and color to establish importance
- **Ensure sufficient contrast**: Icons should meet WCAG contrast requirements
- **Align with text baseline**: Icons in text should align properly with typography
- **Use consistent stroke weights**: Match icon stroke width with your design system

```tsx
// Good: Consistent sizing and alignment
<div className="flex items-center gap-2 text-gray-700">
  <IcCalendar size="16px" />
  <span className="text-sm">Select date</span>
</div>

// Good: Semantic color usage
<IcError size="20px" className="text-red-500" />
<IcSuccess size="20px" className="text-green-500" />
<IcWarning size="20px" className="text-yellow-500" />
```

### Common Patterns

- **Loading states**: Use `IcSpinner` or `IcLoading` for async operations
- **Empty states**: Use larger icons (48px+) for empty state illustrations
- **Navigation**: Use directional icons consistently across the application
- **Status indicators**: Use color-coded icons for status representation

## Theme Integration

Icons automatically inherit theme colors when using `currentColor` or Tailwind classes:

```tsx
// Automatically adapts to theme
<IcSun className="w-5 h-5 text-current" />

// Theme-aware with dark mode support
<IcMoon className="w-5 h-5 text-gray-600 dark:text-gray-300" />

// Custom theme integration
<IcBell
  className="w-5 h-5"
  style={{ color: "var(--theme-primary)" }}
/>
```

## Migration Guide

### From other icon libraries

```tsx
// From Heroicons
- import { PlusIcon } from '@heroicons/react/24/outline'
+ import { IcAdd } from 'gends'

// From React Icons
- import { FiPlus } from 'react-icons/fi'
+ import { IcAdd } from 'gends'

// Size prop changes
- <PlusIcon className="w-6 h-6" />
+ <IcAdd size="24px" />
```

### Updating existing implementations

```tsx
// Before: Mixed sizing approaches
<Icon name="add" width={24} height={24} />

// After: Consistent Genesis approach
<IcAdd size="24px" />
```

## Troubleshooting

### Common Issues

**Icon not displaying**

- Verify the icon name is correct and imported properly
- Check if the icon exists in the current version of Gends
- Ensure size is specified correctly (include units like "px")

**Icon too small/large**

- Use standard sizes: 16px, 20px, 24px, 32px, 48px, 64px
- For responsive sizing, use Tailwind classes: `w-4 h-4`, `w-6 h-6`, etc.

**Color not applying**

- Ensure the icon supports color changes (not all do)
- Use `currentColor` to inherit text color
- For Tailwind, use `text-*` classes instead of `fill-*` or `stroke-*`

**Performance issues**

- Avoid importing all icons: `import { IcAdd } from 'gends'` instead of `import * as Icons from 'gends'`
- Use consistent sizes to improve caching
- Consider code splitting for large icon sets

## Related Components

- **Button**: Uses icons for prefixes and suffixes
- **Input**: Often includes search, clear, and validation icons
- **Navigation**: Relies heavily on directional and menu icons
- **Tooltip**: Commonly used with info and help icons
- **Badge**: Uses status and notification icons
- **Modal**: Uses close and navigation icons

## Examples Gallery

### File Type Icons

```tsx
<div className="flex gap-4">
  <DocIcon size="32px" />
  <PdfIcon size="32px" />
  <XlsxIcon size="32px" />
  <CsvIcon size="32px" />
  <TxtIcon size="32px" />
</div>
```

### Status Icons

```tsx
<div className="flex gap-4">
  <IcSuccess size="24px" className="text-green-500" />
  <IcWarning size="24px" className="text-yellow-500" />
  <IcError size="24px" className="text-red-500" />
  <IcInfo size="24px" className="text-blue-500" />
</div>
```

### Interactive Icons

```tsx
<div className="flex gap-2">
  <IcHeart className="w-6 h-6 text-gray-400 hover:text-red-500 cursor-pointer" />
  <IcBookmark className="w-6 h-6 text-gray-400 hover:text-blue-500 cursor-pointer" />
  <IcShare className="w-6 h-6 text-gray-400 hover:text-green-500 cursor-pointer" />
</div>
```

---

For additional icon requests or custom icon needs, please refer to the Genesis Design System guidelines or contact the design team.
