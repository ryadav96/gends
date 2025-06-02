# SelectorDropdown

A versatile dropdown selector component that supports multiple sizes, custom icons, searchable options, and comprehensive styling options.

---

## 1. Quick start

```tsx
import { SelectorDropdown } from "gends";

function Example() {
  return (
    <SelectorDropdown
      options={["Option 1", "Option 2", "Option 3"]}
      size="md"
      placeholder="Select an option"
      onChange={value => console.log(value)}
    />
  );
}
```

---

## 2. Sizes

| size | Height | Font size | Padding     | Use case            |
| ---- | ------ | --------- | ----------- | ------------------- |
| `sm` | 24px   | Body S    | 4px × 4px   | Compact layouts     |
| `md` | 32px   | Body M    | 6px × 8px   | Standard usage      |
| `lg` | 40px   | Body M    | 10px × 12px | Prominent selectors |

```tsx
<SelectorDropdown size="sm" options={options} />
<SelectorDropdown size="md" options={options} />
<SelectorDropdown size="lg" options={options} />
```

---

## 3. Icon configurations

| icon type | Description           | Use case               |
| --------- | --------------------- | ---------------------- |
| No icon   | Text-only options     | Simple selections      |
| With icon | Icon + text options   | Enhanced visual cues   |
| Custom    | Custom icon component | Specialized indicators |

```tsx
// Without icon
<SelectorDropdown
  options={["Option 1", "Option 2"]}
  showIcon={false}
/>

// With default icon
<SelectorDropdown
  options={["Option 1", "Option 2"]}
  showIcon={true}
  icon={<DefaultIcon />}
/>

// With custom icon
<SelectorDropdown
  options={["Option 1", "Option 2"]}
  showIcon={true}
  icon={<CustomIcon />}
/>
```

---

## 4. States

| state    | Description    | Visual treatment |
| -------- | -------------- | ---------------- |
| Default  | Normal state   | Standard styling |
| Disabled | Inactive state | Muted colors     |
| Focused  | Keyboard focus | Focus ring       |
| Active   | Dropdown open  | Active styling   |

```tsx
// Default state
<SelectorDropdown options={options} />

// Disabled state
<SelectorDropdown
  options={options}
  disabled={true}
/>

// With focus style
<SelectorDropdown
  options={options}
  showFocusStyle={true}
/>
```

---

## 5. Dropdown configuration

```tsx
// Custom dropdown height
<SelectorDropdown
  options={options}
  maxDropdownHeight="400px"
/>

// With scrollbar
<SelectorDropdown
  options={longOptionsList}
  maxDropdownHeight="300px"
/>

// Custom dropdown styling
<SelectorDropdown
  options={options}
  className="custom-dropdown"
/>
```

---

## 6. Custom content

```tsx
// Custom option rendering
<SelectorDropdown>
  <div className="custom-option">
    <Icon />
    <span>Option 1</span>
  </div>
  <div className="custom-option">
    <Icon />
    <span>Option 2</span>
  </div>
</SelectorDropdown>

// With complex content
<SelectorDropdown>
  <CustomOptionComponent data={optionData} />
</SelectorDropdown>
```

---

## 7. Full prop reference

### Basic Props

| Prop           | Type                      | Default | Description              |
| -------------- | ------------------------- | ------- | ------------------------ |
| `options`      | `React.ReactNode[]`       | `[]`    | Array of option elements |
| `defaultValue` | `string`                  | `""`    | Initial selected value   |
| `onChange`     | `(value: string) => void` | -       | Selection change handler |
| `placeholder`  | `string`                  | `""`    | Placeholder text         |
| `children`     | `React.ReactNode`         | -       | Custom dropdown content  |

### Display Props

| Prop             | Type                   | Default | Description           |
| ---------------- | ---------------------- | ------- | --------------------- |
| `size`           | `'sm' \| 'md' \| 'lg'` | `'md'`  | Dropdown size variant |
| `showIcon`       | `boolean`              | `true`  | Show option icons     |
| `icon`           | `ReactNode`            | -       | Custom icon component |
| `disabled`       | `boolean`              | `false` | Disable dropdown      |
| `showFocusStyle` | `boolean`              | `true`  | Show focus ring       |

### Dropdown Props

| Prop                | Type     | Default   | Description            |
| ------------------- | -------- | --------- | ---------------------- |
| `maxDropdownHeight` | `string` | `"300px"` | Max height of dropdown |
| `className`         | `string` | `""`      | Additional CSS classes |

### Event Handlers

| Prop       | Type                      | Description          |
| ---------- | ------------------------- | -------------------- |
| `onChange` | `(value: string) => void` | Value change handler |

---

## 8. Recipes

### Basic selector

```tsx
<SelectorDropdown
  options={["Option 1", "Option 2", "Option 3"]}
  placeholder="Select an option"
  onChange={value => handleSelection(value)}
/>
```

### Icon selector

```tsx
<SelectorDropdown
  options={[
    <div className="flex items-center gap-2">
      <Icon1 />
      <span>First Option</span>
    </div>,
    <div className="flex items-center gap-2">
      <Icon2 />
      <span>Second Option</span>
    </div>,
  ]}
  showIcon={true}
  size="md"
/>
```

### Custom styled selector

```tsx
<SelectorDropdown
  options={options}
  className="border-2 border-blue-500 rounded-full"
  size="lg"
  showIcon={true}
  icon={<CustomIcon />}
/>
```

### Disabled state

```tsx
<SelectorDropdown options={options} disabled={true} placeholder="Not available" />
```

### With custom content

```tsx
<SelectorDropdown size="md">
  <div className="p-2 hover:bg-gray-100">
    <h4>Custom Option 1</h4>
    <p className="text-sm text-gray-500">Description</p>
  </div>
  <div className="p-2 hover:bg-gray-100">
    <h4>Custom Option 2</h4>
    <p className="text-sm text-gray-500">Description</p>
  </div>
</SelectorDropdown>
```

---

## 9. Accessibility

The SelectorDropdown component includes accessibility features:

- Keyboard navigation support
- ARIA attributes for states
- Focus management
- Screen reader support

```tsx
<SelectorDropdown options={options} aria-label="Select option" aria-describedby="helper-text" />
```

---

## 10. Design Tokens

The SelectorDropdown component uses the following design system tokens:

**Sizing:**

- Small: `h-gd-24`
- Medium: `h-gd-32`
- Large: `h-gd-40`

**Typography:**

- Small: `text-en-desktop-body-s-prominent`
- Medium/Large: `text-en-desktop-body-m-prominent`

**Spacing:**

- Small padding: `px-gd-4 py-gd-4`
- Medium padding: `px-gd-8 py-gd-6`
- Large padding: `px-gd-12 py-gd-10`

**Colors:**

- Text: `text-color-text-subdued-1`
- Hover: `text-color-text-default`
- Active: `text-color-text-default`
- Disabled: `opacity-30`

**Icons:**

- Small/Medium: `16px`
- Large: `20px`

**Layout:**

- Border radius: `rounded-full`
- Dropdown padding: `p-gd-8`
- Option padding: `p-gd-8`

---

Consider using SelectorDropdown with:

- **Form** — For option selection
- **Filter** — For data filtering
- **Settings** — For preferences
- **Navigation** — For menu selection
- **Configuration** — For setup options
