# Search Bar

A flexible search component that combines an input field with an optional dropdown for filtered searches.

## Features

- Input field with search icon
- Optional dropdown for category/filter selection
- Multiple size variants
- Left/right dropdown positioning
- Customizable dropdown width
- Disabled state support
- Flexible styling options

## Installation

```tsx
import { SearchBar } from 'gends';
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | `"s" \| "m" \| "l"` | `"m"` | Controls the size of the search bar |
| dropdownPlaceholder | string | `"Select"` | Placeholder text for the dropdown |
| inputPlaceholder | string | `"Search"` | Placeholder text for the search input |
| dropdownWidth | string | `"120px"` | Width of the dropdown section |
| options | `DropdownOption[]` | `[]` | Options for the dropdown menu |
| disabled | boolean | `false` | Disables both input and dropdown |
| hideDropdown | boolean | `false` | Hides the dropdown section |
| dropdownPosition | `"left" \| "right"` | `"right"` | Position of the dropdown relative to the input |
| onInputChange | `(value: string) => void` | - | Callback when input value changes |
| onDropdownChange | `(option: DropdownOption) => void` | - | Callback when dropdown selection changes |
| inputProps | InputHTMLAttributes | - | Additional props for the input element |

## DropdownOption Type

```tsx
type DropdownOption = {
  id: number;
  label: string;
  value: string;
};
```

## Examples

### Basic Search Bar

```tsx
<SearchBar 
  inputPlaceholder="Search items..."
  onInputChange={(value) => console.log('Search:', value)}
/>
```

### With Category Dropdown

```tsx
const options = [
  { id: 1, label: "Products", value: "products" },
  { id: 2, label: "Services", value: "services" },
  { id: 3, label: "Articles", value: "articles" }
];

<SearchBar 
  dropdownPlaceholder="Category"
  inputPlaceholder="Search..."
  options={options}
  onInputChange={(value) => console.log('Search:', value)}
  onDropdownChange={(option) => console.log('Category:', option)}
/>
```

### Left-Positioned Dropdown

```tsx
<SearchBar 
  dropdownPosition="left"
  dropdownWidth="150px"
  options={options}
  inputPlaceholder="Search in category..."
/>
```

### Different Sizes

```tsx
// Small
<SearchBar size="s" inputPlaceholder="Small search..." />

// Medium (default)
<SearchBar size="m" inputPlaceholder="Medium search..." />

// Large
<SearchBar size="l" inputPlaceholder="Large search..." />
```

### Disabled State

```tsx
<SearchBar 
  disabled={true}
  inputPlaceholder="Disabled search"
  options={options}
/>
```

## Styling

The SearchBar component can be customized using the following CSS classes:

- Container: Border, background, and layout styling
- Dropdown section: Width and position customization
- Input section: Text and placeholder styling
- Divider: Color and size of the separator between dropdown and input
- Icons: Size and color of search and dropdown icons

## Best Practices

1. Provide clear placeholder text that indicates the search purpose
2. Use appropriate dropdown options that make sense for the search context
3. Consider mobile responsiveness when setting dropdown width
4. Maintain consistent sizing with other form elements in your interface
5. Use left-positioned dropdown when the categories are more important than the search
6. Include helper text or tooltips for complex search interfaces