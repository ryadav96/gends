# FilterPills

A flexible filter component that displays selected filters as pills with options to add more filters, clear selections, and save filter configurations.

---

## 1. Quick start

```tsx
import { FilterPills } from "gends";

function Example() {
  const options = [
    {
      id: "status",
      label: "Status",
      selectedValues: ["active", "pending"],
      options: [
        { id: "active", label: "Active", value: "active" },
        { id: "pending", label: "Pending", value: "pending" },
      ],
    },
  ];

  return (
    <FilterPills
      options={options}
      onChange={(data, option, index) => {
        console.log("Filter changed:", data, option, index);
      }}
      onClearAll={() => {
        console.log("Cleared all filters");
      }}
    />
  );
}
```

---

## 2. Basic Usage

Display selected filters with clear and save options:

```tsx
<FilterPills
  options={filterOptions}
  onChange={handleFilterChange}
  onClearAll={handleClearAll}
  hideClearAll={false}
  hideSaveButton={false}
/>
```

---

## 3. Additional Filters

Add a "More" button for additional filter options:

```tsx
<FilterPills
  options={mainFilters}
  moreFilterOptions={additionalFilters}
  onMoreOptionChange={handleMoreFilterChange}
  onChange={handleFilterChange}
/>
```

---

## 4. Custom Styling

Customize the appearance of filter pills and buttons:

```tsx
<FilterPills
  options={filterOptions}
  buttonProps={{
    clearAll: {
      className: "custom-clear-button",
      appearance: "default",
      kind: "tertiary",
    },
    save: {
      className: "custom-save-button",
      appearance: "default",
      kind: "secondary",
    },
  }}
  filterPillsContainerProps={{
    className: "custom-container",
  }}
/>
```

---

## 5. Full Prop Reference

### Basic Props

| Prop             | Type                 | Default | Description                      |
| ---------------- | -------------------- | ------- | -------------------------------- |
| `options`        | `FilterPillsProps[]` | -       | Array of filter options          |
| `selectedValues` | `any`                | -       | Currently selected filter values |
| `hideClearAll`   | `boolean`            | `false` | Hide the clear all button        |
| `hideSaveButton` | `boolean`            | `false` | Hide the save button             |

### Event Handlers

| Prop                 | Type                                          | Default    | Description                 |
| -------------------- | --------------------------------------------- | ---------- | --------------------------- |
| `onChange`           | `(data: any, option: any, i: number) => void` | -          | Filter change handler       |
| `onClearAll`         | `() => void`                                  | -          | Clear all filters handler   |
| `onMoreOptionChange` | `(data: any, option: any, i: number) => void` | `() => {}` | More filters change handler |
| `onSaveHandler`      | `(e: any, options: any) => void`              | `() => {}` | Save filters handler        |

### Customization Props

| Prop                        | Type                                   | Default | Description                      |
| --------------------------- | -------------------------------------- | ------- | -------------------------------- |
| `moreFilterOptions`         | `FilterPillsProps[]`                   | `[]`    | Additional filter options        |
| `buttonProps`               | `object`                               | `{}`    | Props for clear and save buttons |
| `moreFilterProps`           | `FilterPillsProps`                     | `{}`    | Props for more filters button    |
| `filterPillsContainerProps` | `React.HTMLAttributes<HTMLDivElement>` | `{}`    | Container props                  |

---

## 6. Recipes

### Basic Filter Pills

```tsx
const filterOptions = [
  {
    id: "category",
    label: "Category",
    selectedValues: ["electronics"],
    options: [
      { id: "electronics", label: "Electronics", value: "electronics" },
      { id: "clothing", label: "Clothing", value: "clothing" },
    ],
  },
];

<FilterPills options={filterOptions} onChange={handleFilterChange} onClearAll={handleClearAll} />;
```

### With Additional Filters

```tsx
<FilterPills
  options={mainFilters}
  moreFilterOptions={additionalFilters}
  onMoreOptionChange={handleMoreFilterChange}
  onChange={handleFilterChange}
  onClearAll={handleClearAll}
  onSaveHandler={handleSaveFilters}
/>
```

### Custom Styled Filter Pills

```tsx
<FilterPills
  options={filterOptions}
  buttonProps={{
    clearAll: {
      className: "text-red-500",
      appearance: "default",
      kind: "tertiary",
    },
    save: {
      className: "bg-green-500",
      appearance: "default",
      kind: "secondary",
    },
  }}
  filterPillsContainerProps={{
    className: "bg-gray-100 p-4",
  }}
/>
```

---

## 7. Accessibility

The FilterPills component includes several accessibility features:

- Proper ARIA attributes for interactive elements
- Keyboard navigation support
- Focus management
- Screen reader announcements
- Clear visual hierarchy

```tsx
<FilterPills
  options={filterOptions}
  filterPillsContainerProps={{
    role: "region",
    "aria-label": "Filter options",
  }}
/>
```

---

## 8. Design Tokens

The FilterPills component uses the following design system tokens:

**Layout:**

- Container: `flex justify-between px-[16px] py-2 h-[44px]`
- Filter container: `flex items-center gap-[8px] flex-wrap`
- Button container: `flex items-center gap-[4px]`

**Typography:**

- Button text: `text-en-desktop-body-s`
- Filter label: `text-en-desktop-body-m`

**Spacing:**

- Container padding: `px-[16px] py-2`
- Gap between items: `gap-[8px]`
- Button padding: `pr-[8px]`

**Icons:**

- Add icon: `w-[16px] h-[16px]`
- Save icon: `w-full h-full`

---

Consider using FilterPills with:

- **Button** — For clear and save actions
- **FilterPill** — For individual filter items
- **Icon** — For action icons
- **Typography** — For labels and text
- **Form** — For filter configuration
- **Modal** — For additional filter options
