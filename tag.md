# Tag Component

## Overview

The Tag component is a versatile and interactive labeling element designed for categorization, filtering, and content organization. Built with Genesis Design System tokens and accessibility patterns, it supports multiple behavioral types (removable, addable, feature, actionable), four size variants, and comprehensive visual feedback states. Perfect for filter systems, content labels, feature highlights, and interactive categorization across all device types with keyboard navigation support.

## Component API

### Tag Props

| Prop        | Type                                                    | Default      | Description                                       |
| ----------- | ------------------------------------------------------- | ------------ | ------------------------------------------------- |
| `text`      | `string`                                                | **Required** | Text content displayed in the tag                 |
| `type`      | `'removable' \| 'addable' \| 'feature' \| 'actionable'` | `'feature'`  | Determines tag behavior and visual appearance     |
| `size`      | `'xs' \| 's' \| 'm' \| 'l'`                             | `'m'`        | Size variant affecting height and padding         |
| `disabled`  | `boolean`                                               | `false`      | Disables interaction and applies disabled state   |
| `leftIcon`  | `boolean`                                               | `false`      | Shows heart icon on the left side of text         |
| `subBranch` | `boolean`                                               | `false`      | Shows additional heart icon for actionable tags   |
| `icon`      | `ReactNode`                                             | -            | Custom icon element (overrides default icons)     |
| `onRemove`  | `() => void`                                            | -            | Callback when remove icon is clicked              |
| `onAdd`     | `() => void`                                            | -            | Callback when add icon is clicked                 |
| `onAction`  | `() => void`                                            | -            | Callback when tag is clicked (actionable/feature) |
| `className` | `string`                                                | -            | Additional CSS classes for customization          |

## Size Variants

The Tag component offers four size variants optimized for different contexts:

| Size | Height | Font Size | Padding (Standard) | Icon Size | Recommended Use Case         |
| ---- | ------ | --------- | ------------------ | --------- | ---------------------------- |
| `xs` | 20px   | 12px      | 8px / 4px          | 16×16     | Dense lists, compact spaces  |
| `s`  | 24px   | 12px      | 12px / 8px         | 16×16     | Standard filters, tags       |
| `m`  | 28px   | 12px      | 12px / 8px         | 16×16     | Primary navigation, emphasis |
| `l`  | 32px   | 16px      | 12px / 8px         | 20×20     | Touch interfaces, headers    |

```tsx
// Size examples
<div className="flex items-center gap-2">
  <Tag text="Extra Small" size="xs" type="removable" />
  <Tag text="Small" size="s" type="removable" />
  <Tag text="Medium" size="m" type="removable" />
  <Tag text="Large" size="l" type="removable" />
</div>
```

## Type Variants

### Removable Tags

Interactive tags with close icon for deletion functionality.

- **Visual**: White background with gray border, close (×) icon
- **Behavior**: Click close icon to trigger removal
- **Use Cases**: Active filters, selected items, temporary labels

```tsx
<Tag
  text="Active Filter"
  type="removable"
  size="m"
  onRemove={() => handleRemoveFilter("category")}
/>
```

### Addable Tags

Interactive tags with plus icon for adding new items.

- **Visual**: White background with gray border, plus (+) icon
- **Behavior**: Click plus icon to trigger addition
- **Use Cases**: Add new filters, create tags, expand categories

```tsx
<Tag text="Add New Tag" type="addable" size="m" onAdd={() => showAddTagDialog()} />
```

### Feature Tags

Static or clickable tags for highlighting features or status.

- **Visual**: Gray background with rounded corners, optional heart icon
- **Behavior**: Optional click handler for feature interactions
- **Use Cases**: Premium features, status indicators, highlights

```tsx
// Feature tag with left icon
<Tag
  text="Premium Feature"
  type="feature"
  leftIcon
  size="m"
  onAction={() => showFeatureDetails()}
/>

// Simple feature tag
<Tag
  text="New"
  type="feature"
  size="s"
/>
```

### Actionable Tags

Interactive tags with edit icon for triggering actions.

- **Visual**: Gray background, edit pen icon, optional additional heart icon
- **Behavior**: Click to trigger custom action
- **Use Cases**: Edit mode toggles, quick actions, interactive controls

```tsx
// Actionable tag with sub-branch indicator
<Tag
  text="Edit Content"
  type="actionable"
  subBranch
  size="m"
  onAction={() => enableEditMode()}
/>

// Simple actionable tag
<Tag
  text="Quick Edit"
  type="actionable"
  size="m"
  onAction={() => handleQuickEdit()}
/>
```

## Basic Usage

### Simple Tags

```tsx
import { Tag } from "gends";

const BasicExample = () => {
  return (
    <div className="flex flex-wrap gap-2">
      <Tag text="Featured" type="feature" size="m" />
      <Tag text="New Release" type="feature" leftIcon size="m" />
      <Tag text="In Stock" type="feature" size="s" />
    </div>
  );
};
```

### Interactive Tags with State Management

```tsx
import { useState } from "react";
import { Tag } from "gends";

const InteractiveExample = () => {
  const [tags, setTags] = useState([
    { id: 1, text: "React", active: true },
    { id: 2, text: "TypeScript", active: true },
    { id: 3, text: "JavaScript", active: false },
  ]);

  const handleRemoveTag = (id: number) => {
    setTags(prevTags => prevTags.filter(tag => tag.id !== id));
  };

  const handleAddTag = () => {
    const newTag = {
      id: Date.now(),
      text: "New Tag",
      active: true,
    };
    setTags(prevTags => [...prevTags, newTag]);
  };

  return (
    <div className="flex flex-wrap gap-2">
      {tags.map(tag => (
        <Tag
          key={tag.id}
          text={tag.text}
          type="removable"
          size="m"
          onRemove={() => handleRemoveTag(tag.id)}
        />
      ))}
      <Tag text="Add Tag" type="addable" size="m" onAdd={handleAddTag} />
    </div>
  );
};
```

## Advanced Features

### Tags with Custom Icons and Sub-Branch Indicators

```tsx
import { Tag } from "gends";
import { IcStar, IcHeart } from "gends";

const AdvancedExample = () => {
  return (
    <div className="space-y-4">
      {/* Feature tag with left icon */}
      <div className="flex gap-2">
        <Tag text="Favorite" type="feature" leftIcon size="m" />
        <Tag text="Premium" type="feature" leftIcon size="l" />
      </div>

      {/* Actionable tags with sub-branch */}
      <div className="flex gap-2">
        <Tag
          text="Edit with Sub"
          type="actionable"
          subBranch
          size="m"
          onAction={() => console.log("Action with sub-branch")}
        />
        <Tag
          text="Simple Edit"
          type="actionable"
          size="m"
          onAction={() => console.log("Simple action")}
        />
      </div>

      {/* Custom icon usage */}
      <Tag text="Custom Icon" type="feature" icon={<IcStar className="h-4 w-4" />} size="m" />
    </div>
  );
};
```

### Disabled States

```tsx
const DisabledExample = () => {
  return (
    <div className="flex gap-2">
      <Tag text="Disabled Removable" type="removable" disabled size="m" />
      <Tag text="Disabled Addable" type="addable" disabled size="m" />
      <Tag text="Disabled Feature" type="feature" disabled size="m" />
      <Tag text="Disabled Actionable" type="actionable" disabled size="m" />
    </div>
  );
};
```

## Real-World Examples

### 1. Filter System

```tsx
const FilterSystem = () => {
  const [activeFilters, setActiveFilters] = useState([
    { id: "category", label: "Electronics", value: "electronics" },
    { id: "price", label: "$100-$500", value: "price-range" },
    { id: "brand", label: "Apple", value: "apple" },
  ]);

  const availableFilters = [
    { id: "rating", label: "4+ Stars", value: "rating-4plus" },
    { id: "shipping", label: "Free Shipping", value: "free-shipping" },
    { id: "discount", label: "On Sale", value: "on-sale" },
  ];

  const handleRemoveFilter = (filterId: string) => {
    setActiveFilters(prev => prev.filter(filter => filter.id !== filterId));
  };

  const handleAddFilter = (filter: any) => {
    if (!activeFilters.find(f => f.id === filter.id)) {
      setActiveFilters(prev => [...prev, filter]);
    }
  };

  const clearAllFilters = () => {
    setActiveFilters([]);
  };

  return (
    <div className="space-y-4">
      <div className="flex items-center justify-between">
        <h3 className="text-lg font-semibold">Active Filters</h3>
        {activeFilters.length > 0 && (
          <button onClick={clearAllFilters} className="text-sm text-blue-600 hover:text-blue-800">
            Clear All
          </button>
        )}
      </div>

      <div className="flex flex-wrap gap-2 min-h-[32px]">
        {activeFilters.length === 0 ? (
          <span className="text-gray-500 italic">No filters applied</span>
        ) : (
          activeFilters.map(filter => (
            <Tag
              key={filter.id}
              text={filter.label}
              type="removable"
              size="m"
              onRemove={() => handleRemoveFilter(filter.id)}
            />
          ))
        )}
      </div>

      {availableFilters.length > 0 && (
        <>
          <h4 className="text-md font-medium text-gray-700">Suggested Filters</h4>
          <div className="flex flex-wrap gap-2">
            {availableFilters
              .filter(filter => !activeFilters.find(f => f.id === filter.id))
              .map(filter => (
                <Tag
                  key={filter.id}
                  text={filter.label}
                  type="addable"
                  size="s"
                  onAdd={() => handleAddFilter(filter)}
                />
              ))}
          </div>
        </>
      )}
    </div>
  );
};
```

### 2. Content Management System

```tsx
const ContentTagger = () => {
  const [selectedTags, setSelectedTags] = useState(["featured", "tutorial", "react"]);

  const [availableTags] = useState([
    "javascript",
    "typescript",
    "nextjs",
    "tailwind",
    "ui-design",
    "backend",
    "database",
    "api",
  ]);

  const handleRemoveTag = (tag: string) => {
    setSelectedTags(prev => prev.filter(t => t !== tag));
  };

  const handleAddTag = (tag: string) => {
    if (!selectedTags.includes(tag)) {
      setSelectedTags(prev => [...prev, tag]);
    }
  };

  const handleCreateCustomTag = () => {
    const customTag = prompt("Enter new tag name:");
    if (customTag && !selectedTags.includes(customTag.toLowerCase())) {
      setSelectedTags(prev => [...prev, customTag.toLowerCase()]);
    }
  };

  return (
    <div className="max-w-2xl space-y-6">
      <div>
        <h3 className="text-lg font-semibold mb-3">Article Tags</h3>
        <div className="flex flex-wrap gap-2 p-4 border rounded-lg min-h-[80px] bg-gray-50">
          {selectedTags.map(tag => (
            <Tag
              key={tag}
              text={tag}
              type="removable"
              size="m"
              onRemove={() => handleRemoveTag(tag)}
            />
          ))}
          <Tag text="Add Custom Tag" type="addable" size="m" onAdd={handleCreateCustomTag} />
        </div>
      </div>

      <div>
        <h4 className="text-md font-medium mb-3">Popular Tags</h4>
        <div className="flex flex-wrap gap-2">
          {availableTags
            .filter(tag => !selectedTags.includes(tag))
            .map(tag => (
              <Tag key={tag} text={tag} type="addable" size="s" onAdd={() => handleAddTag(tag)} />
            ))}
        </div>
      </div>

      <div className="text-sm text-gray-600">
        Selected {selectedTags.length} tag{selectedTags.length !== 1 ? "s" : ""}
      </div>
    </div>
  );
};
```

### 3. User Skill Profile

```tsx
const SkillProfile = () => {
  const [skills, setSkills] = useState([
    { name: "React", level: "expert", featured: true },
    { name: "TypeScript", level: "advanced", featured: true },
    { name: "Node.js", level: "intermediate", featured: false },
    { name: "Python", level: "beginner", featured: false },
  ]);

  const handleToggleFeatured = (skillName: string) => {
    setSkills(prev =>
      prev.map(skill =>
        skill.name === skillName ? { ...skill, featured: !skill.featured } : skill
      )
    );
  };

  const handleEditSkill = (skillName: string) => {
    console.log(`Editing skill: ${skillName}`);
    // Open edit modal/form
  };

  const handleRemoveSkill = (skillName: string) => {
    setSkills(prev => prev.filter(skill => skill.name !== skillName));
  };

  const getLevelColor = (level: string) => {
    switch (level) {
      case "expert":
        return "bg-green-100 text-green-800";
      case "advanced":
        return "bg-blue-100 text-blue-800";
      case "intermediate":
        return "bg-yellow-100 text-yellow-800";
      case "beginner":
        return "bg-gray-100 text-gray-800";
      default:
        return "bg-gray-100 text-gray-800";
    }
  };

  return (
    <div className="max-w-3xl space-y-6">
      <div>
        <h3 className="text-xl font-semibold mb-4">Featured Skills</h3>
        <div className="flex flex-wrap gap-2">
          {skills
            .filter(skill => skill.featured)
            .map(skill => (
              <Tag
                key={skill.name}
                text={`${skill.name} (${skill.level})`}
                type="feature"
                leftIcon
                size="l"
                onAction={() => handleEditSkill(skill.name)}
              />
            ))}
        </div>
      </div>

      <div>
        <h4 className="text-lg font-medium mb-3">All Skills</h4>
        <div className="space-y-3">
          {skills.map(skill => (
            <div key={skill.name} className="flex items-center gap-2">
              <Tag
                text={skill.name}
                type="removable"
                size="m"
                onRemove={() => handleRemoveSkill(skill.name)}
              />
              <span className={`px-2 py-1 rounded-full text-xs ${getLevelColor(skill.level)}`}>
                {skill.level}
              </span>
              <Tag
                text={skill.featured ? "Featured" : "Feature"}
                type={skill.featured ? "feature" : "actionable"}
                size="s"
                leftIcon={skill.featured}
                onAction={() => handleToggleFeatured(skill.name)}
              />
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};
```

### 4. E-commerce Product Categories

```tsx
const ProductCategories = () => {
  const [selectedCategories, setSelectedCategories] = useState(["electronics"]);
  const [categoryHierarchy] = useState({
    electronics: ["smartphones", "laptops", "accessories"],
    clothing: ["shirts", "pants", "shoes"],
    home: ["furniture", "decor", "kitchen"],
  });

  const handleCategoryToggle = (category: string) => {
    setSelectedCategories(prev =>
      prev.includes(category) ? prev.filter(c => c !== category) : [...prev, category]
    );
  };

  const handleSubcategoryAdd = (subcategory: string) => {
    if (!selectedCategories.includes(subcategory)) {
      setSelectedCategories(prev => [...prev, subcategory]);
    }
  };

  const getAvailableSubcategories = () => {
    return Object.entries(categoryHierarchy)
      .filter(([category]) => selectedCategories.includes(category))
      .flatMap(([, subcategories]) => subcategories)
      .filter(sub => !selectedCategories.includes(sub));
  };

  return (
    <div className="max-w-4xl space-y-6">
      <div>
        <h3 className="text-lg font-semibold mb-3">Product Categories</h3>
        <div className="flex flex-wrap gap-2">
          {Object.keys(categoryHierarchy).map(category => (
            <Tag
              key={category}
              text={category.charAt(0).toUpperCase() + category.slice(1)}
              type={selectedCategories.includes(category) ? "removable" : "addable"}
              size="m"
              onRemove={
                selectedCategories.includes(category)
                  ? () => handleCategoryToggle(category)
                  : undefined
              }
              onAdd={
                !selectedCategories.includes(category)
                  ? () => handleCategoryToggle(category)
                  : undefined
              }
            />
          ))}
        </div>
      </div>

      {getAvailableSubcategories().length > 0 && (
        <div>
          <h4 className="text-md font-medium mb-3 text-gray-700">Available Subcategories</h4>
          <div className="flex flex-wrap gap-2">
            {getAvailableSubcategories().map(subcategory => (
              <Tag
                key={subcategory}
                text={subcategory.charAt(0).toUpperCase() + subcategory.slice(1)}
                type="addable"
                size="s"
                onAdd={() => handleSubcategoryAdd(subcategory)}
              />
            ))}
          </div>
        </div>
      )}

      <div>
        <h4 className="text-md font-medium mb-3">Selected Categories & Subcategories</h4>
        <div className="flex flex-wrap gap-2 p-4 border rounded-lg min-h-[60px] bg-blue-50">
          {selectedCategories.length === 0 ? (
            <span className="text-gray-500 italic">No categories selected</span>
          ) : (
            selectedCategories.map(category => (
              <Tag
                key={category}
                text={category.charAt(0).toUpperCase() + category.slice(1)}
                type="removable"
                size="m"
                onRemove={() => handleCategoryToggle(category)}
              />
            ))
          )}
        </div>
      </div>
    </div>
  );
};
```

### 5. Task Management with Priority Tags

```tsx
const TaskPriorityTags = () => {
  const [tasks, setTasks] = useState([
    { id: 1, title: "Fix critical bug", priority: "high", featured: true },
    { id: 2, title: "Update documentation", priority: "medium", featured: false },
    { id: 3, title: "Refactor components", priority: "low", featured: false },
    { id: 4, title: "Design review", priority: "medium", featured: true },
  ]);

  const priorityConfig = {
    high: { color: "bg-red-100 text-red-800", icon: true },
    medium: { color: "bg-yellow-100 text-yellow-800", icon: false },
    low: { color: "bg-green-100 text-green-800", icon: false },
  };

  const handleChangePriority = (taskId: number) => {
    const priorities = ["low", "medium", "high"];
    setTasks(prev =>
      prev.map(task => {
        if (task.id === taskId) {
          const currentIndex = priorities.indexOf(task.priority);
          const nextIndex = (currentIndex + 1) % priorities.length;
          return { ...task, priority: priorities[nextIndex] };
        }
        return task;
      })
    );
  };

  const handleToggleFeatured = (taskId: number) => {
    setTasks(prev =>
      prev.map(task => (task.id === taskId ? { ...task, featured: !task.featured } : task))
    );
  };

  const handleRemoveTask = (taskId: number) => {
    setTasks(prev => prev.filter(task => task.id !== taskId));
  };

  return (
    <div className="max-w-4xl space-y-6">
      <div>
        <h3 className="text-xl font-semibold mb-4">Featured Tasks</h3>
        <div className="grid gap-3">
          {tasks
            .filter(task => task.featured)
            .map(task => (
              <div
                key={task.id}
                className="flex items-center gap-3 p-3 border rounded-lg bg-blue-50"
              >
                <span className="font-medium flex-1">{task.title}</span>
                <Tag
                  text={task.priority.toUpperCase()}
                  type="feature"
                  leftIcon={priorityConfig[task.priority].icon}
                  size="m"
                />
                <Tag
                  text="Unfeature"
                  type="actionable"
                  size="s"
                  onAction={() => handleToggleFeatured(task.id)}
                />
              </div>
            ))}
        </div>
      </div>

      <div>
        <h3 className="text-xl font-semibold mb-4">All Tasks</h3>
        <div className="grid gap-2">
          {tasks.map(task => (
            <div key={task.id} className="flex items-center gap-2 p-2 border rounded">
              <span className="flex-1">{task.title}</span>

              <Tag
                text={task.priority}
                type="actionable"
                size="s"
                onAction={() => handleChangePriority(task.id)}
              />

              <Tag
                text={task.featured ? "Featured" : "Feature"}
                type={task.featured ? "feature" : "addable"}
                size="s"
                leftIcon={task.featured}
                onAdd={!task.featured ? () => handleToggleFeatured(task.id) : undefined}
                onAction={task.featured ? () => handleToggleFeatured(task.id) : undefined}
              />

              <Tag
                text="Remove"
                type="removable"
                size="s"
                onRemove={() => handleRemoveTask(task.id)}
              />
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};
```

## Accessibility Features

### Keyboard Navigation

- **Tab**: Navigate to focusable tags (removable, addable, actionable)
- **Enter/Space**: Activate tag action (remove, add, or custom action)
- **Escape**: Remove focus from tag

### Screen Reader Support

- Proper `role="button"` for interactive tags
- `aria-disabled` for disabled state
- Descriptive action announcements
- Clear semantic structure

### Visual Accessibility

- High contrast focus indicators
- Color-blind friendly state differentiation
- Sufficient color contrast ratios (WCAG AA)
- Clear visual hierarchy with consistent sizing

```tsx
// Accessibility-enhanced tags
<div role="group" aria-label="Filter tags">
  <Tag
    text="Accessible Filter"
    type="removable"
    size="m"
    onRemove={() => handleRemove()}
    aria-label="Remove accessible filter"
  />
</div>
```

## Design System Integration

### Genesis Design System Tokens

The Tag component uses Genesis Design System tokens for consistent theming:

```css
/* Height using Genesis spacing tokens */
.tag-xs {
  height: var(--gd-spacing-20);
}
.tag-s {
  height: var(--gd-spacing-24);
}
.tag-m {
  height: var(--gd-spacing-28);
}
.tag-l {
  height: var(--gd-spacing-32);
}

/* Typography using Genesis text scales */
.tag-text {
  font-size: var(--gd-text-body-s);
  line-height: var(--gd-line-height-s);
}

/* Colors using Genesis color tokens */
.tag-removable {
  background-color: var(--gd-background-surface-0);
  border-color: var(--gd-neutral-grey-40);
  color: var(--gd-text-subdued-1);
}

.tag-feature {
  background-color: var(--gd-background-surface-30);
  color: var(--gd-text-subdued-1);
}
```

### Theme Support

```tsx
// Automatic theme adaptation
<div className="theme-light">
  <Tag text="Light Theme" type="feature" />
</div>

<div className="theme-dark">
  <Tag text="Dark Theme" type="feature" />
</div>
```

## Best Practices

### Performance Optimization

```tsx
// Memoize tag handlers to prevent unnecessary re-renders
const FilterTags = ({ filters }) => {
  const handleRemove = useCallback((filterId: string) => {
    setFilters(prev => prev.filter(f => f.id !== filterId));
  }, []);

  const handleAdd = useCallback((filter: Filter) => {
    setFilters(prev => [...prev, filter]);
  }, []);

  return (
    <div className="flex flex-wrap gap-2">
      {filters.map(filter => (
        <Tag
          key={filter.id}
          text={filter.label}
          type="removable"
          size="m"
          onRemove={() => handleRemove(filter.id)}
        />
      ))}
    </div>
  );
};

// Virtualize for large tag lists
const VirtualizedTagList = ({ tags }) => {
  if (tags.length > 100) {
    return <VirtualGrid items={tags} renderItem={TagItem} />;
  }

  return (
    <div className="flex flex-wrap gap-2">
      {tags.map(tag => (
        <Tag key={tag.id} {...tag} />
      ))}
    </div>
  );
};
```

### State Management Patterns

```tsx
// Use reducer for complex tag state
const tagReducer = (state, action) => {
  switch (action.type) {
    case "ADD_TAG":
      return { ...state, tags: [...state.tags, action.payload] };
    case "REMOVE_TAG":
      return { ...state, tags: state.tags.filter(t => t.id !== action.payload) };
    case "TOGGLE_FEATURED":
      return {
        ...state,
        tags: state.tags.map(t => (t.id === action.payload ? { ...t, featured: !t.featured } : t)),
      };
    default:
      return state;
  }
};

const TagManager = () => {
  const [state, dispatch] = useReducer(tagReducer, { tags: [] });

  return (
    <div className="flex flex-wrap gap-2">
      {state.tags.map(tag => (
        <Tag
          key={tag.id}
          text={tag.text}
          type={tag.featured ? "feature" : "removable"}
          leftIcon={tag.featured}
          onRemove={() => dispatch({ type: "REMOVE_TAG", payload: tag.id })}
          onAction={() => dispatch({ type: "TOGGLE_FEATURED", payload: tag.id })}
        />
      ))}
    </div>
  );
};
```

### UX Guidelines

- Keep tag text concise (ideally 1-3 words)
- Group related tags logically
- Provide clear visual feedback for interactions
- Use consistent sizing within the same context
- Consider mobile touch targets (minimum 44px)
- Implement proper loading states for async operations

```tsx
// Good tag labeling
const goodTags = [
  { text: "React", type: "feature" },
  { text: "New", type: "feature" },
  { text: "Sale", type: "feature" },
];

// Avoid overly long text
const avoidLongText = [
  { text: "This is a very long tag name that should be shortened", type: "feature" },
];

// Better approach for long content
const betterApproach = [
  { text: "Long Content", type: "actionable", onAction: () => showDetails() },
];
```

## Common Pitfalls and Troubleshooting

### Event Handlers Not Firing

```tsx
// ❌ Incorrect: Wrong event handler for tag type
<Tag
  text="Remove Me"
  type="removable"
  onAdd={() => handleRemove()} // Wrong handler
/>

// ✅ Correct: Matching handler to tag type
<Tag
  text="Remove Me"
  type="removable"
  onRemove={() => handleRemove()}
/>
```

### Missing Icons

```tsx
// ❌ Missing: No leftIcon prop for feature tags
<Tag text="Featured" type="feature" />

// ✅ Correct: Show heart icon for feature
<Tag text="Featured" type="feature" leftIcon />
```

### Disabled State Issues

```tsx
// ❌ Incorrect: Disabled tag still has handlers
<Tag
  text="Disabled"
  type="removable"
  disabled
  onRemove={() => handleRemove()} // Handler won't work
/>

// ✅ Correct: Conditional handler based on disabled state
<Tag
  text="Conditional"
  type="removable"
  disabled={isDisabled}
  onRemove={!isDisabled ? () => handleRemove() : undefined}
/>
```

### Performance Issues with Many Tags

```tsx
// ❌ Creating new functions on each render
const TagList = ({ tags }) => (
  <div>
    {tags.map(tag => (
      <Tag
        key={tag.id}
        text={tag.text}
        type="removable"
        onRemove={() => handleRemove(tag.id)} // New function each render
      />
    ))}
  </div>
);

// ✅ Memoized handlers
const TagList = ({ tags }) => {
  const handleRemove = useCallback((id: string) => {
    setTags(prev => prev.filter(t => t.id !== id));
  }, []);

  return (
    <div>
      {tags.map(tag => (
        <TagItem key={tag.id} tag={tag} onRemove={handleRemove} />
      ))}
    </div>
  );
};

const TagItem = memo(({ tag, onRemove }) => (
  <Tag text={tag.text} type="removable" onRemove={() => onRemove(tag.id)} />
));
```

## Migration Guide

### From Legacy Tag Components

```tsx
// Legacy component
<LegacyTag
  label="Old Tag"
  removable
  onDelete={() => handleDelete()}
/>

// New Tag component
<Tag
  text="New Tag"
  type="removable"
  onRemove={() => handleDelete()}
/>
```

### Adding Interactive Features

```tsx
// Basic static tag
<Tag text="Static" />

// Enhanced with interactions
<Tag
  text="Interactive"
  type="actionable"
  onAction={() => handleAction()}
/>
```

### TypeScript Migration

```tsx
// Define proper tag data types
interface TagData {
  id: string;
  text: string;
  type: "removable" | "addable" | "feature" | "actionable";
  featured?: boolean;
  metadata?: Record<string, any>;
}

const typedTags: TagData[] = [
  {
    id: "1",
    text: "TypeScript",
    type: "feature",
    featured: true,
    metadata: { level: "advanced" },
  },
];
```

The Tag component provides a versatile foundation for content labeling and categorization with comprehensive interactive capabilities, accessibility features, and seamless integration with the Genesis Design System. Its flexible API supports everything from simple static labels to complex interactive tag management systems.
