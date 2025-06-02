# Tile

A flexible container component that provides a consistent, interactive surface for content—perfect for cards, sections, and interactive elements. Supports both direct content and slot-based composition.

---

## 1. Quick start

```tsx
import { Tile } from "gends";

function Example() {
  return (
    <Tile>
      <h2>Content Title</h2>
      <p>Content description goes here</p>
    </Tile>
  );
}
```

Wrap **any content**—`Tile` provides consistent styling and hover interactions while maintaining flexibility for its children.

---

## 2. Dimensions

| Property | Value                         | Description                          |
| -------- | ----------------------------- | ------------------------------------ |
| Width    | 1092px                        | Fixed width for consistent layouts   |
| Height   | 200px                         | Fixed height for uniform appearance  |
| Padding  | 32px horizontal, 6px vertical | Internal spacing using design tokens |
| Radius   | lg (8px)                      | Rounded corners for modern look      |

```tsx
<Tile className="w-full" /> {/* Override default width */}
<Tile className="h-[300px]" /> {/* Custom height */}
```

The component uses Figma-specified dimensions by default but can be customized via className.

---

## 3. Visual styles

| Property      | Value                | Description                 |
| ------------- | -------------------- | --------------------------- |
| Background    | background-surface-0 | Light surface color         |
| Border radius | lg (8px)             | Rounded corners             |
| Hover effect  | accent/50 opacity    | Subtle interaction feedback |
| Layout        | Flex, centered       | Centered content alignment  |

```tsx
<Tile className="bg-primary-100" /> {/* Custom background */}
<Tile className="rounded-xl" /> {/* Custom border radius */}
```

---

## 4. Composition modes

### Direct content

```tsx
<Tile>
  <div className="space-y-4">
    <h3>Regular content</h3>
    <p>Direct children are centered by default</p>
  </div>
</Tile>
```

### Slot mode

```tsx
<Tile asChild>
  <button onClick={() => console.log("Clicked")}>Interactive content</button>
</Tile>
```

---

## 5. Full prop reference

### Basic

| Prop        | Type        | Default | Description               |
| ----------- | ----------- | ------- | ------------------------- |
| `asChild`   | `boolean`   | `false` | Use Slot composition mode |
| `children`  | `ReactNode` | -       | Content to render         |
| `className` | `string`    | -       | Additional CSS classes    |

### HTML Attributes

Tile extends `React.HTMLAttributes<HTMLDivElement>`, so all standard div props work:

```tsx
<Tile onClick={() => {}} role="button" aria-label="Interactive tile" data-testid="feature-tile" />
```

---

## 6. Recipes

### Interactive card

```tsx
function FeatureCard({ title, description, onClick }) {
  return (
    <Tile asChild className="cursor-pointer hover:shadow-lg transition-shadow">
      <button onClick={onClick}>
        <div className="space-y-4 text-left">
          <h3 className="text-xl font-semibold">{title}</h3>
          <p className="text-gray-600">{description}</p>
        </div>
      </button>
    </Tile>
  );
}
```

### Content section

```tsx
function ContentSection({ children }) {
  return (
    <Tile className="p-6">
      <div className="w-full max-w-3xl mx-auto">{children}</div>
    </Tile>
  );
}
```

### Media tile

```tsx
function MediaTile({ image, title, subtitle }) {
  return (
    <Tile className="relative overflow-hidden group">
      <img
        src={image}
        alt={title}
        className="absolute inset-0 w-full h-full object-cover transition-transform group-hover:scale-105"
      />
      <div className="absolute inset-0 bg-black/50">
        <div className="relative z-10 text-white p-6">
          <h3 className="text-2xl font-bold">{title}</h3>
          <p className="mt-2">{subtitle}</p>
        </div>
      </div>
    </Tile>
  );
}
```

### Grid layout

```tsx
function TileGrid({ items }) {
  return (
    <div className="grid grid-cols-2 gap-6">
      {items.map(item => (
        <Tile key={item.id} className="h-[150px] w-full">
          <div className="text-center">
            <item.icon className="h-8 w-8 mx-auto" />
            <h3 className="mt-2 font-medium">{item.title}</h3>
          </div>
        </Tile>
      ))}
    </div>
  );
}
```

### Dashboard widget

```tsx
function DashboardWidget({ title, data, loading }) {
  return (
    <Tile className="relative">
      {loading ? (
        <div className="absolute inset-0 bg-white/80 flex items-center justify-center">
          <Spinner />
        </div>
      ) : (
        <div className="w-full p-4">
          <h4 className="text-sm font-medium text-gray-500">{title}</h4>
          <div className="mt-4">
            {/* Widget content */}
            {data}
          </div>
        </div>
      )}
    </Tile>
  );
}
```

---

## 7. Accessibility considerations

- Use semantic HTML within tiles
- Provide appropriate ARIA attributes for interactive tiles
- Ensure sufficient color contrast
- Maintain keyboard navigation support
- Consider focus management for interactive content

```tsx
<Tile asChild role="region" aria-label="Feature description">
  <section>
    <h2 id="section-title">Feature</h2>
    <div aria-labelledby="section-title">{/* Content */}</div>
  </section>
</Tile>
```

---

## 8. Design patterns

### Layout patterns

- Center content by default
- Support flexible widths
- Maintain consistent padding
- Allow content overflow handling

### Interaction patterns

- Subtle hover effects
- Optional click/tap handling
- Support for interactive children
- Keyboard navigation support

### Composition patterns

- Direct content nesting
- Slot-based composition
- Grid/flex container compatibility
- Responsive adaptability

---

## 9. Related components

Consider using Tile with:

- **Card** — For more structured content layouts
- **Section** — For page organization
- **Grid** — For tile-based layouts
- **Button** — For interactive tiles
- **Slot** — For component composition

---

## 10. Storybook playground

Run `pnpm storybook` and open **Atoms / Tile** to experiment with all configurations.

The underlying file is

```
src/components/genesis/atoms/tile/tile.stories.tsx
```

which you can use as reference for advanced patterns and implementation examples.
