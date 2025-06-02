# Carousel

A flexible and accessible carousel component built with Embla Carousel. It provides smooth sliding animations, navigation controls, and various customization options for displaying content in a slideshow format.

---

## 1. Quick start

```tsx
import { Carousel } from "gends";

function Example() {
  const slides = [
    <div key="1">Slide 1</div>,
    <div key="2">Slide 2</div>,
    <div key="3">Slide 3</div>,
  ];

  return <Carousel slides={slides} showDots={true} showLabels={true} label="Featured Items" />;
}
```

---

## 2. Sizes

The Carousel component supports five size variants:

| Size | Description                 | Use case                     |
| ---- | --------------------------- | ---------------------------- |
| `xs` | Extra small (32px controls) | Compact UI, mobile views     |
| `s`  | Small (32px controls)       | Dense layouts                |
| `m`  | Medium (32px controls)      | Standard usage               |
| `l`  | Large (48px controls)       | Prominent displays           |
| `xl` | Extra large (48px controls) | Hero sections, landing pages |

```tsx
// Small size
<Carousel size="s" slides={slides} />

// Large size
<Carousel size="l" slides={slides} />
```

---

## 3. Navigation Controls

Customize the navigation behavior and appearance:

```tsx
// Basic navigation
<Carousel
  slides={slides}
  showDots={true}
  hideNav={false}
/>

// Custom navigation buttons
<Carousel
  slides={slides}
  iconButtonProps={{
    prevButton: { className: "custom-prev" },
    nextButton: { className: "custom-next" }
  }}
/>

// Hide navigation
<Carousel
  slides={slides}
  hideNav={true}
  showDots={true}
/>
```

---

## 4. Auto Play

Configure automatic slide transitions:

```tsx
// Basic auto play
<Carousel
  slides={slides}
  autoPlay={true}
  interval={3000}
/>

// Auto play with loop
<Carousel
  slides={slides}
  autoPlay={true}
  loop={true}
  interval={5000}
/>

// Auto play with controls
<Carousel
  slides={slides}
  autoPlay={true}
  showLabels={true}
  label="Auto Playing Slides"
/>
```

---

## 5. Custom Styling

Apply custom styles to different parts of the carousel:

```tsx
<Carousel
  slides={slides}
  classes={{
    dot: "custom-dot",
    activeDot: "custom-active-dot",
    dotContainer: "custom-dot-container",
    footer: "custom-footer",
    label: "custom-label",
    nav: "custom-nav",
  }}
  styles={{
    dot: { backgroundColor: "#ccc" },
    activeDot: { backgroundColor: "#000" },
    dotContainer: { gap: "8px" },
    footer: { padding: "16px" },
    label: { fontSize: "16px" },
    nav: { gap: "8px" },
  }}
/>
```

---

## 6. Full Prop Reference

### Basic Props

| Prop         | Type                                | Default | Description                        |
| ------------ | ----------------------------------- | ------- | ---------------------------------- |
| `slides`     | `React.ReactNode[]`                 | -       | Array of slide content             |
| `size`       | `'xs' \| 's' \| 'm' \| 'l' \| 'xl'` | `'l'`   | Size variant of the carousel       |
| `autoPlay`   | `boolean`                           | `false` | Enable automatic slide transitions |
| `loop`       | `boolean`                           | `false` | Enable infinite loop               |
| `interval`   | `number`                            | `3000`  | Auto play interval in milliseconds |
| `hideNav`    | `boolean`                           | `false` | Hide navigation buttons            |
| `hideFooter` | `boolean`                           | `false` | Hide the footer section            |

### Display Props

| Prop         | Type      | Default | Description         |
| ------------ | --------- | ------- | ------------------- |
| `showDots`   | `boolean` | `false` | Show dot indicators |
| `showLabels` | `boolean` | `false` | Show slide labels   |
| `label`      | `string`  | `""`    | Custom label text   |

### Styling Props

| Prop      | Type     | Default | Description                            |
| --------- | -------- | ------- | -------------------------------------- |
| `classes` | `object` | `{}`    | Custom class names for different parts |
| `styles`  | `object` | `{}`    | Custom styles for different parts      |

### Navigation Props

| Prop              | Type     | Default | Description                  |
| ----------------- | -------- | ------- | ---------------------------- |
| `iconButtonProps` | `object` | `{}`    | Props for navigation buttons |
| `emblaOptions`    | `object` | `{}`    | Options for Embla Carousel   |

### Footer Props

| Prop           | Type       | Default | Description                   |
| -------------- | ---------- | ------- | ----------------------------- |
| `renderFooter` | `function` | -       | Custom footer render function |

---

## 7. Recipes

### Basic Image Carousel

```tsx
const slides = [
  <img key="1" src="/image1.jpg" alt="Image 1" />,
  <img key="2" src="/image2.jpg" alt="Image 2" />,
  <img key="3" src="/image3.jpg" alt="Image 3" />,
];

<Carousel slides={slides} showDots={true} showLabels={true} label="Image Gallery" size="l" />;
```

### Auto Playing Product Showcase

```tsx
<Carousel
  slides={productSlides}
  autoPlay={true}
  loop={true}
  interval={5000}
  showDots={true}
  showLabels={true}
  label="Featured Products"
  size="xl"
/>
```

### Compact Navigation

```tsx
<Carousel
  slides={slides}
  size="s"
  hideNav={false}
  showDots={true}
  classes={{
    nav: "gap-1",
    dot: "w-2 h-2",
    activeDot: "w-4 h-2",
  }}
/>
```

### Custom Footer

```tsx
<Carousel
  slides={slides}
  renderFooter={({ selectedIndex, slides }) => (
    <div className="custom-footer">
      <span>
        Slide {selectedIndex + 1} of {slides.length}
      </span>
      <CustomControls />
    </div>
  )}
/>
```

---

## 8. Accessibility

The Carousel component includes several accessibility features:

- Proper ARIA attributes for slides and controls
- Keyboard navigation support:
  - Arrow keys: Navigate between slides
  - Enter/Space: Activate controls
  - Tab: Move between interactive elements
- Screen reader announcements for slide changes
- Focus management
- Proper heading hierarchy

```tsx
<Carousel
  slides={slides}
  showLabels={true}
  label="Accessible Carousel"
  role="region"
  aria-label="Image carousel"
/>
```

---

## 9. Design Tokens

The Carousel component uses the following design system tokens:

**Spacing:**

- Container gap: `gap-4`
- Dot gap: `gap-[8px]` (compact) / `gap-[12px]` (relaxed)
- Footer padding: `pt-gd-8 pb-gd-8`

**Typography:**

- Label: `text-en-Desktop-Heading-m`
- Slide count: `text-en-Desktop-Heading-m`

**Colors:**

- Active dot: `bg-[#000093]`
- Inactive dot: `bg-[#000093] opacity-30`
- Hover states: `hover:bg-[#6464FF]`

**Layout:**

- Dot sizes:
  - Compact: `w-[8px] h-[8px]`
  - Relaxed: `w-[12px] h-[12px]`
- Active dot sizes:
  - Compact: `w-[24px] h-[8px]`
  - Relaxed: `w-[32px] h-[12px]`
- Icon button sizes:
  - Compact: `w-[32px] h-[32px]`
  - Relaxed: `w-[48px] h-[48px]`

**Transitions:**

- Slide transitions: Smooth sliding animation
- Dot transitions: `transition-all`

---

Consider using Carousel with:

- **Image** — For image galleries
- **Card** — For content slides
- **Button** — For custom controls
- **IconButton** — For navigation
- **Text** — For slide labels
- **Badge** — For slide indicators
