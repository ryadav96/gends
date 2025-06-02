# Tag

A versatile tag component that supports multiple types (removable, addable, feature, actionable), sizes, and interactive states—perfect for categorization, filtering, and interactive content labeling.

---

## 1. Quick start

```tsx
import { Tag } from "gends";

function Example() {
  return (
    <Tag text="Example Tag" type="removable" size="m" onRemove={() => console.log("Tag removed")} />
  );
}
```

Wrap **nothing else**—`Tag` is self-contained and handles all interactions internally.

---

## 2. Sizes

| Size | Height | Font Scale | Use Case                   |
| ---- | ------ | ---------- | -------------------------- |
| `xs` | 20px   | body-s     | Compact lists, dense UIs   |
| `s`  | 24px   | body-s     | Default size for most uses |
| `m`  | 28px   | body-s     | Standard visibility        |
| `l`  | 32px   | body-l     | Enhanced visibility        |

```tsx
<Tag size="xs" text="Extra Small" />
<Tag size="s" text="Small" />
<Tag size="m" text="Medium" />
<Tag size="l" text="Large" />
```

---

## 3. Types

| Type         | Description       | Visual Style                  | Interactions     |
| ------------ | ----------------- | ----------------------------- | ---------------- |
| `removable`  | Deletable tag     | Grey background, close icon   | Click to remove  |
| `addable`    | New tag creation  | Blue accent, plus icon        | Click to add     |
| `feature`    | Feature indicator | Yellow accent, optional heart | Static/clickable |
| `actionable` | Interactive tag   | Green accent, edit icon       | Click for action |

```tsx
// Removable tag
<Tag
  type="removable"
  text="Click to remove"
  onRemove={() => handleRemove()}
/>

// Addable tag
<Tag
  type="addable"
  text="Add new"
  onAdd={() => handleAdd()}
/>

// Feature tag
<Tag
  type="feature"
  text="Premium"
  leftIcon
/>

// Actionable tag
<Tag
  type="actionable"
  text="Edit"
  onAction={() => handleAction()}
/>
```

---

## 4. Icons and Layout

Tags support various icon configurations:

```tsx
// Left icon (feature tag)
<Tag
  type="feature"
  text="Featured"
  leftIcon
/>

// Right icon (default for removable/addable)
<Tag
  type="removable"
  text="Remove"
/>

// Both icons (actionable with subBranch)
<Tag
  type="actionable"
  text="Edit"
  subBranch
/>

// Custom icon
<Tag
  text="Custom"
  icon={<CustomIcon className="h-4 w-4" />}
/>
```

---

## 5. States

| State    | Visual Feedback    | Trigger         |
| -------- | ------------------ | --------------- |
| Default  | Normal opacity     | Initial state   |
| Hover    | Background lighten | Mouse over      |
| Focused  | Blue ring + shadow | Keyboard focus  |
| Disabled | 50% opacity        | `disabled` prop |

```tsx
// Default state
<Tag text="Normal" />

// Disabled state
<Tag text="Inactive" disabled />

// Interactive state
<Tag
  text="Clickable"
  type="actionable"
  onAction={() => {}}
/>
```

---

## 6. Full prop reference

### Basic

| Prop       | Type      | Default     | Description           |
| ---------- | --------- | ----------- | --------------------- |
| `text`     | `string`  | Required    | Tag content text      |
| `type`     | `TagType` | `"default"` | Tag behavior variant  |
| `size`     | `TagSize` | `"m"`       | Tag size variant      |
| `disabled` | `boolean` | `false`     | Disables interactions |

### Icons & Layout

| Prop        | Type        | Default       | Description                       |
| ----------- | ----------- | ------------- | --------------------------------- |
| `icon`      | `ReactNode` | Based on type | Custom icon override              |
| `leftIcon`  | `boolean`   | `false`       | Show icon on left (feature)       |
| `subBranch` | `boolean`   | `false`       | Show additional icon (actionable) |

### Event Handlers

| Prop       | Type         | Default | Description                 |
| ---------- | ------------ | ------- | --------------------------- |
| `onRemove` | `() => void` | -       | Removable tag callback      |
| `onAdd`    | `() => void` | -       | Addable tag callback        |
| `onAction` | `() => void` | -       | Actionable/feature callback |

### Styling

| Prop        | Type     | Default | Description            |
| ----------- | -------- | ------- | ---------------------- |
| `className` | `string` | -       | Additional CSS classes |

---

## 7. Recipes

### Filter tags

```tsx
function FilterTags({ filters, onRemove }) {
  return (
    <div className="flex flex-wrap gap-2">
      {filters.map(filter => (
        <Tag
          key={filter.id}
          text={filter.label}
          type="removable"
          size="s"
          onRemove={() => onRemove(filter.id)}
        />
      ))}
      <Tag type="addable" text="Add filter" onAdd={() => showFilterDialog()} />
    </div>
  );
}
```

### Feature badges

```tsx
function FeatureBadges({ features }) {
  return (
    <div className="flex gap-1">
      {features.map(feature => (
        <Tag
          key={feature.id}
          type="feature"
          text={feature.name}
          leftIcon={feature.isPremium}
          size="xs"
        />
      ))}
    </div>
  );
}
```

### Interactive category tags

```tsx
function CategoryTags({ categories, onEdit, onDelete }) {
  return (
    <div className="flex flex-wrap gap-2">
      {categories.map(category => (
        <Tag
          key={category.id}
          text={category.name}
          type="actionable"
          size="m"
          onAction={() => onEdit(category)}
          subBranch={category.hasSubcategories}
        />
      ))}
    </div>
  );
}
```

### Tag input with suggestions

```tsx
function TagInput({ selectedTags, suggestions, onAdd, onRemove }) {
  return (
    <div className="flex flex-wrap items-center gap-2 p-2 border rounded">
      {selectedTags.map(tag => (
        <Tag
          key={tag.id}
          text={tag.label}
          type="removable"
          size="s"
          onRemove={() => onRemove(tag)}
        />
      ))}
      <div className="flex gap-1">
        {suggestions.map(suggestion => (
          <Tag
            key={suggestion.id}
            text={suggestion.label}
            type="addable"
            size="s"
            onAdd={() => onAdd(suggestion)}
          />
        ))}
      </div>
    </div>
  );
}
```

### Status indicators

```tsx
function StatusTags({ items }) {
  return (
    <div className="space-y-1">
      {items.map(item => (
        <div key={item.id} className="flex items-center justify-between">
          <span>{item.name}</span>
          <Tag
            text={item.status}
            type="feature"
            size="xs"
            leftIcon={item.status === "active"}
            className={cn({
              "bg-green-100 text-green-800": item.status === "active",
              "bg-yellow-100 text-yellow-800": item.status === "pending",
              "bg-red-100 text-red-800": item.status === "inactive",
            })}
          />
        </div>
      ))}
    </div>
  );
}
```

---

## 8. Accessibility considerations

- Uses semantic HTML with appropriate ARIA attributes
- Supports keyboard navigation and focus management
- Provides visual feedback for interactive states
- Maintains sufficient color contrast ratios
- Includes clear action indicators

```tsx
<Tag
  text="Accessible Tag"
  type="actionable"
  role="button"
  aria-label="Edit item"
  tabIndex={0}
  onKeyDown={e => {
    if (e.key === "Enter" || e.key === " ") {
      handleAction();
    }
  }}
/>
```

---

## 9. Design patterns

### Layout patterns

- Use consistent spacing (4px margins)
- Align icons with text baseline
- Maintain fixed heights per size
- Support wrapping in flex containers

### Interaction patterns

- Clear hover/focus states
- Instant feedback on actions
- Support for keyboard navigation
- Consistent icon placement

### Visual hierarchy

- Size indicates importance
- Type determines interactivity
- Colors reflect purpose
- Icons enhance meaning

---
