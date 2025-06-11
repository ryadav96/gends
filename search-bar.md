# Search Bar Component

## Overview

The Search Bar component is a versatile and accessible search interface that combines a text input field with an optional dropdown selector. Built with Genesis Design System tokens, it provides a unified search experience with multiple size variants, dropdown positioning options, and extensive customization capabilities. The component is designed to work seamlessly within the MCP context while maintaining full accessibility support.

## Component API

### SearchBar Props

| Prop                | Type                                    | Default    | Description                                |
| ------------------- | --------------------------------------- | ---------- | ------------------------------------------ |
| size                | `"s" \| "m" \| "l"`                     | `"m"`      | Size variant of the search bar             |
| dropdownPlaceholder | `string`                                | `"Select"` | Placeholder text for the dropdown          |
| inputPlaceholder    | `string`                                | `"Search"` | Placeholder text for the input field       |
| dropdownWidth       | `string`                                | `"120px"`  | Width of the dropdown component            |
| options             | `DropdownOption[]`                      | `[]`       | Array of options for the dropdown          |
| disabled            | `boolean`                               | `false`    | Whether the search bar is disabled         |
| hideDropdown        | `boolean`                               | `false`    | Whether to hide the dropdown component     |
| dropdownPosition    | `"left" \| "right"`                     | `"left"`   | Position of the dropdown relative to input |
| onInputChange       | `(value: string) => void`               | `() => {}` | Callback when input value changes          |
| onDropdownChange    | `(option: DropdownOption) => void`      | `() => {}` | Callback when dropdown selection changes   |
| inputProps          | `InputHTMLAttributes<HTMLInputElement>` | `{}`       | Additional props for the input element     |

### DropdownOption Interface

```typescript
interface DropdownOption {
  id: number;
  label: string;
  value: string;
}
```

### Import Statement

```typescript
import { SearchBar } from "gends";
```

## Basic Usage

### Default Search Bar

```tsx
import { SearchBar } from "gends";

function MyComponent() {
  return (
    <SearchBar
      options={[
        { id: 1, label: "Option 1", value: "opt1" },
        { id: 2, label: "Option 2", value: "opt2" },
      ]}
      onInputChange={value => console.log("Search:", value)}
      onDropdownChange={option => console.log("Selected:", option)}
    />
  );
}
```

## Variants

### Size Variants

#### Small (s)

```tsx
<SearchBar
  size="s"
  dropdownPlaceholder="Select"
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

#### Medium (m) - Default

```tsx
<SearchBar
  size="m"
  dropdownPlaceholder="Choose..."
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

#### Large (l)

```tsx
<SearchBar
  size="l"
  dropdownPlaceholder="Select"
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

### Dropdown Position Variants

#### Left (default)

```tsx
<SearchBar
  dropdownPosition="left"
  dropdownPlaceholder="Select"
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

#### Right

```tsx
<SearchBar
  dropdownPosition="right"
  dropdownPlaceholder="Select"
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

## Advanced Features

### Custom Dropdown Width

```tsx
<SearchBar
  dropdownWidth="200px"
  dropdownPlaceholder="Wide Dropdown"
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

### Custom Input Props

```tsx
<SearchBar
  inputProps={{
    maxLength: 50,
    minLength: 3,
    pattern: "[A-Za-z0-9]+",
    required: true,
    autoComplete: "off",
    id: "search-input",
    name: "search",
    spellCheck: false,
  }}
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

### With Autofocus

```tsx
<SearchBar
  inputProps={{
    autoFocus: true,
  }}
  options={[
    { id: 1, label: "Option 1", value: "opt1" },
    { id: 2, label: "Option 2", value: "opt2" },
  ]}
/>
```

## Real-World Usage Examples

### Search with Filter

```tsx
function SearchWithFilter() {
  const [searchTerm, setSearchTerm] = useState("");
  const [selectedFilter, setSelectedFilter] = useState(null);

  const filterOptions = [
    { id: 1, label: "All", value: "all" },
    { id: 2, label: "Documents", value: "doc" },
    { id: 3, label: "Images", value: "img" },
  ];

  return (
    <SearchBar
      dropdownPlaceholder="Filter"
      options={filterOptions}
      onInputChange={setSearchTerm}
      onDropdownChange={setSelectedFilter}
    />
  );
}
```

### Search Without Dropdown

```tsx
function SimpleSearch() {
  return (
    <SearchBar
      hideDropdown
      inputPlaceholder="Search anything..."
      onInputChange={value => console.log("Searching:", value)}
    />
  );
}
```

### Disabled State

```tsx
function DisabledSearch() {
  return (
    <SearchBar
      disabled
      dropdownPlaceholder="Disabled"
      options={[
        { id: 1, label: "Option 1", value: "opt1" },
        { id: 2, label: "Option 2", value: "opt2" },
      ]}
    />
  );
}
```

## Accessibility Features

### Keyboard Navigation

- **Focus Management**: Proper focus handling between input and dropdown
- **ARIA Attributes**: Appropriate roles and labels
- **Keyboard Shortcuts**: Arrow keys for dropdown navigation
- **Focus Indicators**: Clear visual feedback

### Screen Reader Support

- **ARIA Labels**: Clear identification of search and filter areas
- **Live Regions**: Dynamic content updates announced
- **Role Descriptions**: Proper semantic structure

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Focus Indicators**: Clear visual feedback
- **Motion**: Respects reduced motion preferences

## Design System Integration

### Genesis Design Tokens

**Sizing:**

- Small: `h-gd-32`
- Medium: `h-gd-40`
- Large: `h-gd-48`

**Border Radius:**

- Small: `rounded-gd-6`
- Medium: `rounded-gd-8`
- Large: `rounded-gd-12`

**Typography:**

- Small/Medium: `text-en-desktop-body-m`
- Large: `text-en-desktop-body-l`

**Colors:**

- Border: `border-color-neutral-grey-40`
- Background: `bg-color-neutral-white`
- Disabled: `bg-color-background-surface-20`
- Icon: `text-color-neutral-grey-60`

**Spacing:**

- Small Padding: `py-[6px] px-gd-8`
- Medium Padding: `p-gd-8`
- Large Padding: `p-gd-12`

## Best Practices

### Performance

- Use controlled components when needed
- Optimize re-renders
- Handle cleanup properly

### User Experience

- Keep search terms focused and relevant
- Provide clear feedback on search results
- Consider mobile interactions
- Handle edge cases gracefully

### Integration

- Follow design system guidelines
- Maintain consistent spacing
- Consider loading states
- Handle errors appropriately

## Troubleshooting

### Common Issues

**Search:**

- Check input validation
- Verify search functionality
- Review event handlers

**Dropdown:**

- Check option formatting
- Verify selection handling
- Review positioning

**Styling:**

- Check custom styles
- Verify design tokens
- Review responsive behavior

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test all variants
- Verify accessibility

Remember: The Search Bar component provides a flexible and accessible way to handle search functionality with optional filtering. Choose the appropriate configuration based on your specific use case and requirements.
