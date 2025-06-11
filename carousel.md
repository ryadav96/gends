# Carousel Component

## Overview

The Carousel component is a flexible and accessible slideshow interface built with Embla Carousel. It supports automatic playback, manual navigation, dot indicators, custom styling, and extensive accessibility features. The component provides smooth sliding animations with configurable controls for displaying content in a slideshow format across different size variants.

## Component API

### Carousel Props

| Prop              | Type                                                                     | Default  | Description                                       |
| ----------------- | ------------------------------------------------------------------------ | -------- | ------------------------------------------------- |
| `slides`          | `React.ReactNode[]`                                                      | Required | Array of React nodes to display as slides         |
| `size`            | `'xs' \| 's' \| 'm' \| 'l' \| 'xl'`                                      | `'l'`    | Size variant affecting control and dot dimensions |
| `autoPlay`        | `boolean`                                                                | `false`  | Enable automatic slide transitions                |
| `loop`            | `boolean`                                                                | `false`  | Enable infinite looping through slides            |
| `showDots`        | `boolean`                                                                | `false`  | Display dot indicators for slide navigation       |
| `showLabels`      | `boolean`                                                                | `false`  | Show slide counter labels in footer               |
| `label`           | `string`                                                                 | `""`     | Custom label text displayed in footer             |
| `interval`        | `number`                                                                 | `3000`   | Auto play interval in milliseconds                |
| `hideNav`         | `boolean`                                                                | `false`  | Hide previous/next navigation buttons             |
| `hideFooter`      | `boolean`                                                                | `false`  | Hide entire footer section                        |
| `emblaOptions`    | `Record<string, any>`                                                    | `{}`     | Additional options passed to Embla Carousel       |
| `iconButtonProps` | `{ prevButton?: object, nextButton?: object, playPauseButton?: object }` | `{}`     | Props for navigation icon buttons                 |
| `classes`         | `CarouselClasses`                                                        | `{}`     | Custom CSS classes for different parts            |
| `styles`          | `CarouselStyles`                                                         | `{}`     | Custom inline styles for different parts          |
| `renderFooter`    | `(context: CarouselContext) => React.ReactNode`                          | `null`   | Custom footer renderer function                   |

### CarouselClasses Interface

| Property       | Type     | Description                        |
| -------------- | -------- | ---------------------------------- |
| `dot`          | `string` | CSS class for inactive dots        |
| `activeDot`    | `string` | CSS class for active dot           |
| `dotContainer` | `string` | CSS class for dots container       |
| `footer`       | `string` | CSS class for footer section       |
| `label`        | `string` | CSS class for label text           |
| `nav`          | `string` | CSS class for navigation container |

### CarouselStyles Interface

| Property       | Type                  | Description                      |
| -------------- | --------------------- | -------------------------------- |
| `dot`          | `React.CSSProperties` | Inline styles for inactive dots  |
| `activeDot`    | `React.CSSProperties` | Inline styles for active dot     |
| `dotContainer` | `React.CSSProperties` | Inline styles for dots container |
| `footer`       | `React.CSSProperties` | Inline styles for footer section |
| `label`        | `React.CSSProperties` | Inline styles for label text     |
| `nav`          | `React.CSSProperties` | Inline styles for navigation     |

### CarouselHandle Interface (Ref)

| Method       | Type                      | Description                |
| ------------ | ------------------------- | -------------------------- |
| `scrollTo`   | `(index: number) => void` | Navigate to specific slide |
| `scrollNext` | `() => void`              | Navigate to next slide     |
| `scrollPrev` | `() => void`              | Navigate to previous slide |
| `togglePlay` | `() => void`              | Toggle auto play on/off    |

## Basic Usage

### Import

```tsx
import { Carousel } from "gends";
```

### Simple Carousel

```tsx
const BasicCarousel = () => {
  const slides = [
    <div key="1" className="bg-blue-100 p-8 text-center">
      Slide 1
    </div>,
    <div key="2" className="bg-green-100 p-8 text-center">
      Slide 2
    </div>,
    <div key="3" className="bg-red-100 p-8 text-center">
      Slide 3
    </div>,
  ];

  return <Carousel slides={slides} showDots={true} showLabels={true} label="Featured Content" />;
};
```

### With Auto Play

```tsx
const AutoPlayCarousel = () => {
  const slides = [...]; // Your slides array

  return (
    <Carousel
      slides={slides}
      autoPlay={true}
      loop={true}
      interval={4000}
      showDots={true}
      label="Auto Playing Slides"
    />
  );
};
```

## Size Variants

The Carousel component supports five size variants that affect control dimensions and spacing:

### Size Specifications

| Size | Control Size | Dot Size    | Active Dot Size | Icon Size | Use Case           |
| ---- | ------------ | ----------- | --------------- | --------- | ------------------ |
| `xs` | 32px         | 8px × 8px   | 24px × 8px      | 12px      | Compact interfaces |
| `s`  | 32px         | 8px × 8px   | 24px × 8px      | 12px      | Dense layouts      |
| `m`  | 32px         | 8px × 8px   | 24px × 8px      | 12px      | Standard usage     |
| `l`  | 48px         | 12px × 12px | 32px × 12px     | 16px      | Prominent displays |
| `xl` | 48px         | 12px × 12px | 32px × 12px     | 16px      | Hero sections      |

### Size Examples

```tsx
// Extra Small - Compact interface
<Carousel
  slides={slides}
  size="xs"
  showDots={true}
  hideNav={false}
/>

// Small - Dense layout
<Carousel
  slides={slides}
  size="s"
  showDots={true}
  label="Small Carousel"
/>

// Medium - Standard usage
<Carousel
  slides={slides}
  size="m"
  showDots={true}
  showLabels={true}
  label="Medium Carousel"
/>

// Large - Prominent display (default)
<Carousel
  slides={slides}
  size="l"
  autoPlay={true}
  showDots={true}
  label="Large Carousel"
/>

// Extra Large - Hero sections
<Carousel
  slides={slides}
  size="xl"
  autoPlay={true}
  loop={true}
  showDots={true}
  showLabels={true}
  label="Hero Carousel"
/>
```

## Navigation & Controls

### Basic Navigation

```tsx
const NavigationCarousel = () => (
  <Carousel
    slides={slides}
    showDots={true}
    hideNav={false}
    showLabels={true}
    label="Navigation Example"
  />
);
```

### Hidden Navigation

```tsx
const DotsOnlyCarousel = () => (
  <Carousel slides={slides} showDots={true} hideNav={true} label="Dots Only" />
);
```

### Custom Navigation Props

```tsx
const CustomNavCarousel = () => (
  <Carousel
    slides={slides}
    iconButtonProps={{
      prevButton: {
        "aria-label": "Go to previous slide",
        className: "custom-prev-button",
      },
      nextButton: {
        "aria-label": "Go to next slide",
        className: "custom-next-button",
      },
      playPauseButton: {
        "aria-label": "Toggle slideshow",
        className: "custom-play-button",
      },
    }}
    autoPlay={true}
    showDots={true}
  />
);
```

## Auto Play Functionality

### Auto Play with Loop

```tsx
const AutoPlayLoop = () => (
  <Carousel
    slides={slides}
    autoPlay={true}
    loop={true}
    interval={5000}
    showDots={true}
    showLabels={true}
    label="Auto Playing Loop"
  />
);
```

### Auto Play with Controls

```tsx
const AutoPlayWithControls = () => {
  const carouselRef = useRef(null);

  const handleTogglePlay = () => {
    carouselRef.current?.togglePlay();
  };

  return (
    <div>
      <Carousel
        ref={carouselRef}
        slides={slides}
        autoPlay={true}
        interval={3000}
        showDots={true}
        label="Controllable Auto Play"
      />
      <button onClick={handleTogglePlay}>Toggle Play/Pause</button>
    </div>
  );
};
```

### Manual Control Example

```tsx
const ManualControl = () => {
  const carouselRef = useRef(null);

  const goToSlide = index => {
    carouselRef.current?.scrollTo(index);
  };

  const nextSlide = () => {
    carouselRef.current?.scrollNext();
  };

  const prevSlide = () => {
    carouselRef.current?.scrollPrev();
  };

  return (
    <div>
      <Carousel ref={carouselRef} slides={slides} hideNav={true} showDots={true} />
      <div className="flex gap-2 mt-4">
        <button onClick={prevSlide}>Previous</button>
        <button onClick={() => goToSlide(0)}>Go to First</button>
        <button onClick={() => goToSlide(1)}>Go to Second</button>
        <button onClick={nextSlide}>Next</button>
      </div>
    </div>
  );
};
```

## Custom Styling

### Custom Dot Styling

```tsx
const CustomDotCarousel = () => (
  <Carousel
    slides={slides}
    showDots={true}
    classes={{
      dot: "bg-gray-300 hover:bg-gray-500",
      activeDot: "bg-blue-600",
      dotContainer: "gap-3 p-2",
    }}
    styles={{
      dot: {
        borderRadius: "4px",
        transition: "all 0.3s ease",
      },
      activeDot: {
        borderRadius: "4px",
        boxShadow: "0 2px 4px rgba(0,0,0,0.2)",
      },
    }}
  />
);
```

### Custom Footer Styling

```tsx
const CustomFooterCarousel = () => (
  <Carousel
    slides={slides}
    showDots={true}
    showLabels={true}
    label="Custom Footer"
    classes={{
      footer: "bg-gray-100 p-4 rounded-lg",
      label: "text-blue-600 font-bold",
      nav: "gap-4",
    }}
    styles={{
      footer: {
        border: "2px solid #e5e7eb",
        marginTop: "16px",
      },
    }}
  />
);
```

### Complete Custom Styling

```tsx
const FullyCustomCarousel = () => (
  <Carousel
    slides={slides}
    showDots={true}
    showLabels={true}
    label="Fully Customized"
    classes={{
      dot: "bg-purple-200 hover:bg-purple-400",
      activeDot: "bg-purple-600",
      dotContainer: "gap-2 bg-purple-50 p-2 rounded-full",
      footer: "bg-gradient-to-r from-purple-100 to-blue-100 p-4 rounded-lg",
      label: "text-purple-800 font-semibold",
      nav: "gap-2",
    }}
    styles={{
      dot: { width: "10px", height: "10px" },
      activeDot: { width: "30px", height: "10px" },
      footer: { boxShadow: "0 4px 6px rgba(0,0,0,0.1)" },
    }}
  />
);
```

## Advanced Usage

### Custom Footer Renderer

```tsx
const CustomFooterRenderer = () => {
  const renderCustomFooter = context => {
    const { selectedIndex, slides, isPlaying, togglePlay, canScrollNext, canScrollPrev, emblaApi } =
      context;

    return (
      <div className="flex items-center justify-between bg-gray-50 p-4 rounded-lg">
        <div className="flex items-center gap-4">
          <button onClick={togglePlay} className="px-4 py-2 bg-blue-500 text-white rounded">
            {isPlaying ? "Pause" : "Play"}
          </button>
          <span className="text-sm font-medium">
            Slide {selectedIndex + 1} of {slides.length}
          </span>
        </div>

        <div className="flex gap-2">
          <button
            onClick={() => emblaApi?.scrollPrev()}
            disabled={!canScrollPrev}
            className="px-3 py-1 bg-gray-300 rounded disabled:opacity-50"
          >
            ← Prev
          </button>
          <button
            onClick={() => emblaApi?.scrollNext()}
            disabled={!canScrollNext}
            className="px-3 py-1 bg-gray-300 rounded disabled:opacity-50"
          >
            Next →
          </button>
        </div>
      </div>
    );
  };

  return <Carousel slides={slides} autoPlay={true} renderFooter={renderCustomFooter} />;
};
```

### Image Gallery Carousel

```tsx
const ImageGallery = () => {
  const imageSlides = [
    <img
      key="1"
      src="/api/placeholder/800/400"
      alt="Gallery image 1"
      className="w-full h-64 object-cover rounded"
    />,
    <img
      key="2"
      src="/api/placeholder/800/400"
      alt="Gallery image 2"
      className="w-full h-64 object-cover rounded"
    />,
    <img
      key="3"
      src="/api/placeholder/800/400"
      alt="Gallery image 3"
      className="w-full h-64 object-cover rounded"
    />,
    <img
      key="4"
      src="/api/placeholder/800/400"
      alt="Gallery image 4"
      className="w-full h-64 object-cover rounded"
    />,
  ];

  return (
    <Carousel
      slides={imageSlides}
      size="xl"
      showDots={true}
      showLabels={true}
      label="Image Gallery"
      loop={true}
      autoPlay={true}
      interval={4000}
    />
  );
};
```

### Product Showcase

```tsx
const ProductShowcase = () => {
  const productSlides = [
    <div key="1" className="bg-white p-6 rounded-lg shadow-md">
      <img
        src="/api/placeholder/300/200"
        alt="Product 1"
        className="w-full h-48 object-cover rounded mb-4"
      />
      <h3 className="text-lg font-semibold">Product One</h3>
      <p className="text-gray-600">$29.99</p>
    </div>,
    <div key="2" className="bg-white p-6 rounded-lg shadow-md">
      <img
        src="/api/placeholder/300/200"
        alt="Product 2"
        className="w-full h-48 object-cover rounded mb-4"
      />
      <h3 className="text-lg font-semibold">Product Two</h3>
      <p className="text-gray-600">$39.99</p>
    </div>,
    <div key="3" className="bg-white p-6 rounded-lg shadow-md">
      <img
        src="/api/placeholder/300/200"
        alt="Product 3"
        className="w-full h-48 object-cover rounded mb-4"
      />
      <h3 className="text-lg font-semibold">Product Three</h3>
      <p className="text-gray-600">$49.99</p>
    </div>,
  ];

  return (
    <Carousel
      slides={productSlides}
      size="l"
      showDots={true}
      showLabels={true}
      label="Featured Products"
      autoPlay={true}
      loop={true}
      interval={5000}
    />
  );
};
```

## Embla Options Integration

```tsx
const AdvancedCarousel = () => (
  <Carousel
    slides={slides}
    emblaOptions={{
      align: "center",
      skipSnaps: false,
      dragFree: false,
      containScroll: "trimSnaps",
    }}
    showDots={true}
    label="Advanced Carousel"
  />
);
```

## useCarousel Hook

Access carousel context in child components:

import { useCarousel } from "gends";

const CarouselStatusDisplay = () => {
  const { selectedIndex, slides, isPlaying, canScrollNext, canScrollPrev } = useCarousel();

  return (
    <div className="text-sm text-gray-600">
      <p>
        Current slide: {selectedIndex + 1} of {slides.length}
      </p>
      <p>Status: {isPlaying ? "Playing" : "Paused"}</p>
      <p>Can go next: {canScrollNext ? "Yes" : "No"}</p>
      <p>Can go previous: {canScrollPrev ? "Yes" : "No"}</p>
    </div>
  );
};

// Use within a custom footer
const CarouselWithStatus = () => (
  <Carousel
    slides={slides}
    renderFooter={() => (
      <div className="flex justify-between items-center">
        <CarouselStatusDisplay />
        <div className="default-controls">{/* Default navigation will be rendered */}</div>
      </div>
    )}
  />
);
``
## Design Tokens & Styling

### Size-Based Styling

The component uses density-based styling with two density modes:

- **Compact**: `xs`, `s`, `m` sizes
- **Relaxed**: `l`, `xl` sizes

### Color Specifications

| Element       | Color                   | Hover                    | Active                   |
| ------------- | ----------------------- | ------------------------ | ------------------------ |
| Active Dot    | `#000093`               | `#00004C`                | `#00004C`                |
| Inactive Dot  | `#000093` (30% opacity) | `#6464FF` (100% opacity) | `#000093` (100% opacity) |
| Focus Outline | `#3535f3`               | -                        | -                        |

### Spacing Tokens

- Footer padding: `pt-gd-8 pb-gd-8` (8px top/bottom)
- Container spacing: `space-y-[16px]` (16px vertical gap)
- Dot gap (compact): `gap-[8px]`
- Dot gap (relaxed): `gap-[12px]`
- Navigation gap: `gap-2` (8px)

### Typography

- Label: `text-en-desktop-heading-m`
- Slide counter: `text-en-desktop-body-m-prominent` with `!text-color-neutral-grey-80`

## Accessibility Features

The Carousel component includes comprehensive accessibility support:

### ARIA Attributes

- `role="region"` on main container
- `role="group"` on individual slides
- `aria-roledescription="slide"` on slides
- `aria-label` describing slide position
- `aria-selected` for dot indicators

### Keyboard Navigation

- **Arrow Keys**: Navigate between slides
- **Tab**: Move between interactive elements
- **Enter/Space**: Activate controls
- **Escape**: Pause auto play (when focused)

### Screen Reader Support

```tsx
<Carousel
  slides={slides}
  showLabels={true}
  label="Accessible Image Carousel"
  aria-label="Featured images carousel"
  showDots={true}
  iconButtonProps={{
    prevButton: { "aria-label": "View previous image" },
    nextButton: { "aria-label": "View next image" },
    playPauseButton: { "aria-label": "Toggle slideshow playback" },
  }}
/>
```

## Best Practices

### Performance

```tsx
// Optimize slide content with React.memo for complex slides
const OptimizedSlide = React.memo(({ data }) => (
  <div className="slide-content">{/* Complex slide content */}</div>
));

const slides = useMemo(
  () => data.map((item, index) => <OptimizedSlide key={item.id || index} data={item} />),
  [data]
);
```

### Responsive Design

```tsx
const ResponsiveCarousel = () => {
  const [size, setSize] = useState("l");

  useEffect(() => {
    const handleResize = () => {
      setSize(window.innerWidth < 768 ? "s" : "l");
    };

    window.addEventListener("resize", handleResize);
    handleResize();

    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return (
    <Carousel
      slides={slides}
      size={size}
      showDots={true}
      hideNav={size === "s"}
      showLabels={size !== "s"}
    />
  );
};
```

### Error Handling

```tsx
const SafeCarousel = ({ slides = [] }) => {
  if (slides.length === 0) {
    return <div className="p-8 text-center text-gray-500">No slides to display</div>;
  }

  return (
    <Carousel
      slides={slides}
      showDots={slides.length > 1}
      hideNav={slides.length <= 1}
      label={`Gallery (${slides.length} ${slides.length === 1 ? "item" : "items"})`}
    />
  );
};
```

## Troubleshooting

### Common Issues

**Slides not displaying properly:**

- Ensure each slide has a unique `key` prop
- Verify slides array is not empty
- Check for CSS conflicts affecting slide dimensions

**Auto play not working:**

- Confirm `autoPlay={true}` is set
- Check `interval` value is reasonable (> 1000ms recommended)
- Ensure component is not re-rendering frequently

**Navigation not responsive:**

- Verify `hideNav={false}` (default)
- Check if `loop={false}` is preventing navigation at ends
- Ensure `iconButtonProps` are not breaking button functionality

**Dots not appearing:**

- Confirm `showDots={true}` is set
- Check for CSS conflicts affecting dot visibility
- Verify custom dot styling is not hiding elements

## Migration Guide

### From v1.x to v2.x

```tsx
// v1.x (deprecated)
<Carousel
  images={imageArray}
  controls={true}
  indicators={true}
/>

// v2.x (current)
<Carousel
  slides={imageArray.map(img => <img key={img.id} src={img.src} alt={img.alt} />)}
  hideNav={false}
  showDots={true}
/>
```

### Property Mapping

| v1.x Property | v2.x Property | Notes                         |
| ------------- | ------------- | ----------------------------- |
| `images`      | `slides`      | Now accepts any React content |
| `controls`    | `hideNav`     | Inverted boolean logic        |
| `indicators`  | `showDots`    | Direct mapping                |
| `autoplay`    | `autoPlay`    | Camelcase change              |

## Integration Examples

### With Form Components

```tsx
const CarouselForm = () => (
  <Carousel
    slides={[<FormStep1 key="step1" />, <FormStep2 key="step2" />, <FormStep3 key="step3" />]}
    hideNav={false}
    showDots={true}
    label="Multi-step Form"
  />
);
```

### With Card Components

```tsx
const CardCarousel = () => {
  const cardSlides = cards.map(card => (
    <Card key={card.id} className="mx-2">
      <CardHeader>
        <CardTitle>{card.title}</CardTitle>
      </CardHeader>
      <CardContent>
        <p>{card.description}</p>
      </CardContent>
    </Card>
  ));

  return <Carousel slides={cardSlides} size="xl" showDots={true} autoPlay={true} loop={true} />;
};
```

---

Consider using Carousel with:

- **Card** — For content slides and product showcases
- **Image** — For photo galleries and media displays
- **Button** — For custom navigation controls
- **IconButton** — For play/pause and navigation actions
- **Text** — For slide labels and descriptions
- **Badge** — For slide indicators and status
- **Modal** — For fullscreen carousel experiences
