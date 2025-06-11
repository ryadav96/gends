# Slot Component

## Overview

The Slot component is a flexible placeholder container designed for dynamic content management in interface builders, drag-and-drop systems, and layout constructors. Built with Genesis Design System tokens, it automatically displays customizable placeholder text when empty and seamlessly renders children when content is provided. The component features fixed dimensions optimized for grid layouts and provides visual feedback for interactive states.

## Component API

### Slot Props

| Prop            | Type                                   | Default     | Description                                 |
| --------------- | -------------------------------------- | ----------- | ------------------------------------------- |
| children        | `React.ReactNode`                      | `undefined` | Content to render when slot is filled       |
| showPlaceholder | `boolean`                              | `true`      | Whether to show placeholder text when empty |
| placeholder     | `string`                               | `"Replace"` | Text displayed when slot is empty           |
| isActive        | `boolean`                              | `false`     | Visual state for interactions/hover         |
| className       | `string`                               | `undefined` | Additional CSS classes for customization    |
| ...props        | `React.HTMLAttributes<HTMLDivElement>` | `{}`        | All standard div HTML attributes            |

### Import Statement

```typescript
import { Slot } from "gends";
```

## Basic Usage

### Default Slot

```tsx
import { Slot } from "gends";

function MyComponent() {
  return <Slot placeholder="Replace" showPlaceholder={true} />;
}
```

## Variants

### Default Slot (Empty State)

```tsx
<Slot showPlaceholder={true} placeholder="Replace" isActive={false} />
```

### Slot Without Placeholder

```tsx
<Slot showPlaceholder={false} placeholder="Replace" isActive={false} />
```

### Active Slot

```tsx
<Slot showPlaceholder={true} placeholder="Drop here" isActive={true} />
```

### Slot with Content

```tsx
<Slot placeholder="Replace">
  <div className="flex items-center gap-2">
    <img src="/icon.png" alt="Icon" className="w-4 h-4" />
    <span>Content</span>
  </div>
</Slot>
```

## Dimensions & Specifications

### Default Dimensions

- **Width**: 76px (fixed)
- **Height**: 36px (fixed)
- **Padding**: 8px (using Genesis tokens)
- **Gap**: 10px (internal spacing)
- **Border**: 1px dashed border
- **Border Radius**: 6px (rounded-md)

### Design Tokens

**Colors:**

- Border: `border-color-primary-50` (dashed)
- Background: `bg-color-primary-20`
- Text: `text-color-neutral-black`

**Spacing:**

- Padding Top/Bottom: `pt-gd-8 pb-gd-8`
- Internal Gap: `gap-[10px]`

## Real-World Usage Examples

### File Upload Drop Zone

```tsx
function FileUploadSlot() {
  const [file, setFile] = useState(null);
  const [isDragOver, setIsDragOver] = useState(false);

  const handleDrop = e => {
    e.preventDefault();
    setIsDragOver(false);
    const droppedFile = e.dataTransfer.files[0];
    setFile(droppedFile);
  };

  return (
    <Slot
      isActive={isDragOver}
      placeholder="Drop file here"
      className="w-48 h-32 cursor-pointer"
      onDragOver={e => {
        e.preventDefault();
        setIsDragOver(true);
      }}
      onDragLeave={() => setIsDragOver(false)}
      onDrop={handleDrop}
    >
      {file && (
        <div className="text-center">
          <p className="font-medium">{file.name}</p>
          <p className="text-sm text-gray-500">{(file.size / 1024).toFixed(1)}KB</p>
        </div>
      )}
    </Slot>
  );
}
```

### Content Builder Widget Slot

```tsx
function WidgetSlot({ widget, onAddWidget, onRemoveWidget }) {
  return (
    <Slot
      placeholder="+ Add widget"
      className="w-full h-24 group"
      onClick={!widget ? onAddWidget : undefined}
    >
      {widget && (
        <div className="relative w-full h-full">
          <WidgetPreview data={widget} />
          <button
            onClick={onRemoveWidget}
            className="absolute top-1 right-1 opacity-0 group-hover:opacity-100 
                       bg-red-500 text-white rounded-full w-5 h-5 flex items-center justify-center text-xs"
          >
            ×
          </button>
        </div>
      )}
    </Slot>
  );
}
```

### Image Gallery Placeholder

```tsx
function ImageSlot({ image, onImageSelect, onImageRemove }) {
  return (
    <Slot
      placeholder="Add image"
      className="w-24 h-24 cursor-pointer border-2 hover:border-primary-60 group"
      onClick={!image ? onImageSelect : undefined}
    >
      {image && (
        <div className="relative w-full h-full">
          <img src={image.url} alt={image.alt} className="w-full h-full object-cover rounded" />
          <button
            onClick={e => {
              e.stopPropagation();
              onImageRemove();
            }}
            className="absolute -top-2 -right-2 opacity-0 group-hover:opacity-100 
                       bg-red-500 text-white rounded-full w-6 h-6 flex items-center justify-center text-sm"
          >
            ×
          </button>
        </div>
      )}
    </Slot>
  );
}
```

### Dashboard Layout Grid

```tsx
function DashboardGrid() {
  const [widgets, setWidgets] = useState({});

  const addWidget = position => {
    setWidgets(prev => ({
      ...prev,
      [position]: {
        type: "chart",
        title: `Chart ${position}`,
        data: generateMockData(),
      },
    }));
  };

  const removeWidget = position => {
    setWidgets(prev => {
      const updated = { ...prev };
      delete updated[position];
      return updated;
    });
  };

  return (
    <div className="grid grid-cols-3 grid-rows-2 gap-4 w-full h-96">
      {Array.from({ length: 6 }, (_, i) => (
        <Slot
          key={i}
          placeholder={`Add chart ${i + 1}`}
          className="w-full h-full border-dashed border-2"
          onClick={!widgets[i] ? () => addWidget(i) : undefined}
        >
          {widgets[i] && (
            <div className="w-full h-full p-2 group">
              <div className="relative w-full h-full bg-white rounded border">
                <h3 className="p-2 font-medium">{widgets[i].title}</h3>
                <div className="px-2 pb-2">
                  <div className="w-full h-20 bg-blue-100 rounded flex items-center justify-center">
                    Chart Data
                  </div>
                </div>
                <button
                  onClick={() => removeWidget(i)}
                  className="absolute top-1 right-1 opacity-0 group-hover:opacity-100 
                             bg-red-500 text-white rounded-full w-5 h-5 flex items-center justify-center text-xs"
                >
                  ×
                </button>
              </div>
            </div>
          )}
        </Slot>
      ))}
    </div>
  );
}
```

### Form Builder Field Slots

```tsx
function FormBuilderRow({ fields, onAddField, onRemoveField }) {
  const maxFields = 3;

  return (
    <div className="flex gap-4 w-full">
      {Array.from({ length: maxFields }, (_, i) => (
        <Slot
          key={i}
          placeholder="+ Add field"
          className="flex-1 min-h-12 p-4"
          onClick={!fields[i] ? () => onAddField(i) : undefined}
        >
          {fields[i] ? (
            <div className="w-full group">
              <FormFieldPreview field={fields[i]} />
              <button
                onClick={() => onRemoveField(i)}
                className="mt-2 text-red-500 text-sm opacity-0 group-hover:opacity-100"
              >
                Remove field
              </button>
            </div>
          ) : null}
        </Slot>
      ))}
    </div>
  );
}
```

### Media Placeholder with Type Detection

```tsx
function MediaSlot({ media, onSelectMedia, type = "any", size = "medium" }) {
  const sizeClasses = {
    small: "w-16 h-12",
    medium: "w-32 h-24",
    large: "w-48 h-36",
  };

  const getPlaceholderText = () => {
    switch (type) {
      case "image":
        return "Add image";
      case "video":
        return "Add video";
      case "audio":
        return "Add audio";
      default:
        return "Add media";
    }
  };

  const renderMediaPreview = () => {
    if (!media) return null;

    switch (media.type) {
      case "image":
        return (
          <img
            src={media.url}
            alt={media.alt || ""}
            className="max-w-full max-h-full object-cover rounded"
          />
        );
      case "video":
        return (
          <video src={media.url} className="max-w-full max-h-full rounded" controls={false} muted />
        );
      case "audio":
        return (
          <div className="text-center">
            <div className="text-2xl mb-1">🎵</div>
            <p className="text-xs truncate">{media.name}</p>
          </div>
        );
      default:
        return (
          <div className="text-center">
            <div className="text-2xl mb-1">📄</div>
            <p className="text-xs truncate">{media.name}</p>
          </div>
        );
    }
  };

  return (
    <Slot
      placeholder={getPlaceholderText()}
      className={`${sizeClasses[size]} cursor-pointer hover:bg-primary-30 group`}
      onClick={!media ? onSelectMedia : undefined}
    >
      {media && (
        <div className="relative w-full h-full flex items-center justify-center">
          {renderMediaPreview()}
          <button
            onClick={e => {
              e.stopPropagation();
              onSelectMedia(null);
            }}
            className="absolute -top-2 -right-2 opacity-0 group-hover:opacity-100 
                       bg-red-500 text-white rounded-full w-5 h-5 flex items-center justify-center text-xs"
          >
            ×
          </button>
        </div>
      )}
    </Slot>
  );
}
```

## Interactive States & Events

### Drag and Drop Integration

```tsx
function DragDropSlot({ onDrop, acceptedTypes = [] }) {
  const [isDragOver, setIsDragOver] = useState(false);
  const [content, setContent] = useState(null);

  const handleDragEnter = e => {
    e.preventDefault();
    setIsDragOver(true);
  };

  const handleDragLeave = e => {
    e.preventDefault();
    if (!e.currentTarget.contains(e.relatedTarget)) {
      setIsDragOver(false);
    }
  };

  const handleDrop = e => {
    e.preventDefault();
    setIsDragOver(false);

    const data = e.dataTransfer.getData("text/plain");
    if (data) {
      setContent(JSON.parse(data));
      onDrop?.(JSON.parse(data));
    }
  };

  return (
    <Slot
      isActive={isDragOver}
      placeholder="Drop content here"
      className={`w-32 h-24 transition-all ${isDragOver ? "border-primary-60 bg-primary-30" : ""}`}
      onDragEnter={handleDragEnter}
      onDragOver={e => e.preventDefault()}
      onDragLeave={handleDragLeave}
      onDrop={handleDrop}
    >
      {content && (
        <div className="text-center">
          <p className="font-medium">{content.title}</p>
          <p className="text-xs text-gray-500">{content.type}</p>
        </div>
      )}
    </Slot>
  );
}
```

### Keyboard Navigation Support

```tsx
function KeyboardAccessibleSlot({ onActivate, content, placeholder }) {
  const handleKeyDown = e => {
    if (e.key === "Enter" || e.key === " ") {
      e.preventDefault();
      onActivate?.();
    }
  };

  return (
    <Slot
      placeholder={placeholder}
      className="focus:outline-none focus:ring-2 focus:ring-primary-50 focus:ring-offset-2"
      tabIndex={0}
      role="button"
      aria-label={content ? "Content slot with content" : `Empty slot: ${placeholder}`}
      onKeyDown={handleKeyDown}
      onClick={onActivate}
    >
      {content}
    </Slot>
  );
}
```

## Customization & Styling

### Size Variants

```tsx
// Small slot
<Slot
  placeholder="Small"
  className="w-16 h-8 text-xs"
/>

// Large slot
<Slot
  placeholder="Large"
  className="w-48 h-32 text-lg"
/>

// Full width slot
<Slot
  placeholder="Full width"
  className="w-full h-12"
/>
```

### Color Variants

```tsx
// Success variant
<Slot
  placeholder="Success"
  className="border-green-300 bg-green-50 text-green-700"
/>

// Warning variant
<Slot
  placeholder="Warning"
  className="border-yellow-300 bg-yellow-50 text-yellow-700"
/>

// Error variant
<Slot
  placeholder="Error"
  className="border-red-300 bg-red-50 text-red-700"
/>
```

### Border Styles

```tsx
// Solid border
<Slot
  placeholder="Solid border"
  className="border-solid border-2"
/>

// No border
<Slot
  placeholder="No border"
  className="border-none bg-gray-100"
/>

// Rounded corners
<Slot
  placeholder="Rounded"
  className="rounded-lg"
/>
```

## Accessibility Features

### Screen Reader Support

- **Semantic HTML**: Uses `div` with appropriate ARIA attributes
- **Content Detection**: Automatically announces empty vs filled state
- **Interactive Labels**: Clear identification when used as buttons

### Keyboard Navigation

- **Focus Management**: Proper focus indicators and tabIndex support
- **Key Handlers**: Enter and Space key activation
- **Focus Visible**: Ring indicators for keyboard users

### Visual Accessibility

- **Color Contrast**: Meets WCAG 2.1 contrast requirements
- **Focus Indicators**: Clear visual feedback
- **State Communication**: Visual and textual state indicators

```tsx
<Slot
  placeholder="Accessible slot"
  role="button"
  tabIndex={0}
  aria-label="Upload area for images"
  aria-describedby="upload-instructions"
  onKeyDown={e => {
    if (e.key === "Enter" || e.key === " ") {
      handleActivation();
    }
  }}
/>
```

## Design System Integration

### Genesis Design Tokens

**Fixed Dimensions:**

- Width: `w-[76px]` (76px)
- Height: `h-[36px]` (36px)

**Spacing:**

- Padding: `pt-gd-8 pb-gd-8` (8px top/bottom)
- Gap: `gap-[10px]` (10px internal spacing)

**Colors:**

- Border: `border-color-primary-50`
- Background: `bg-color-primary-20`
- Text: `text-color-neutral-black`

**Border:**

- Style: `border-[1px] border-dashed`
- Radius: `rounded-md`

**Interactive States:**

- Transition: `transition-all`
- Hover: Enhanced via className customization
- Focus: Ring styles for accessibility

## Best Practices

### Performance

- Use controlled components sparingly
- Optimize re-renders with React.memo if needed
- Handle cleanup in useEffect hooks

### User Experience

- Provide clear placeholder text
- Use isActive for visual feedback
- Handle loading and error states
- Consider mobile touch targets

### Integration

- Follow design system spacing
- Maintain consistent slot sizes in grids
- Handle edge cases gracefully
- Provide meaningful ARIA labels

## Troubleshooting

### Common Issues

**Content Not Rendering:**

- Check children prop structure
- Verify React.Children.count logic
- Review conditional rendering

**Styling Issues:**

- Check className conflicts
- Verify design token usage
- Review CSS specificity

**Accessibility Problems:**

- Add proper ARIA attributes
- Test keyboard navigation
- Verify screen reader announcements

### Migration Notes

**From Previous Versions:**

- Update import paths
- Review prop changes
- Test placeholder behavior
- Verify accessibility compliance

Remember: The Slot component is designed for flexible content management. Use appropriate dimensions, clear placeholders, and proper accessibility attributes for the best user experience in your interface builders and layout systems.
