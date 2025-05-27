# Breadcrumb

Navigation component that indicates the current page’s location within a hierarchy. Auto-collapses long paths and supports custom separators, icons and link components.

---

## 1. Quick start

```tsx
import Breadcrumb from 'gends';

const items = [
  { label: 'Home', isHome: true, href: '/' },
  { label: 'Library', href: '/library' },
  { label: 'Data', isCurrent: true },
];

<Breadcrumb items={items} />;
```

---

## 2. Collapsing logic

Property | Behaviour | Default
---------|-----------|---------
`maxItems` | Always show this many (from the end) | `4`
`collapseAfter` | Force dropdown when index ≥ value (mobile only etc.) | `undefined`

Hidden items are grouped behind an **ellipsis dropdown** – click to reveal.

---

## 3. Customisation hooks

Hook | Purpose
---- | -------
`separator` | React node rendered between items (defaults to `<IcChevronRight />`).
`ellipsisComponent` | Override the *…* element.
`linkComponent` | Supply your own router-aware link (Next.js `<Link>`, React-Router `<NavLink>` …).
`renderItem` | `(item, index, isLast) => ReactNode` for total control.

Class name props (`itemClassName`, `separatorClassName`, `ellipsisClassName`) let you tweak styling without touching children.

---

## 4. Icons

Items can carry their own icon or use the default *home* glyph:

```tsx
{ label: 'Dashboard', icon: <IcDashboard /> }
```

If `showDefaultIcon` is truthy on the first item, the home icon is injected automatically.

---

## 5. Accessibility

* Uses `<nav aria-label="Breadcrumb">` and an ordered list.
* `aria-current="page"` is applied to the last crumb.

---

## 6. Full prop reference

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `items` | `BreadcrumbItem[]` | – | Data describing each node |
| `maxItems` | `number` | `4` | Show N items before collapsing |
| `separator` | `ReactNode` | `<IcChevronRight />` | Visual divider |
| `ellipsisComponent` | `ReactNode` | `<IcMoreHorizontal />` | Render when path is collapsed |
| `linkComponent` | `ElementType` | – | Custom anchor replacement |
| `renderItem` | Function | – | Custom render factory |
| `collapseAfter` | `number` | – | Force collapse after index |
| `testIdPrefix` | `string` | `'breadcrumb'` | Data-test-id root for automation |
| Styling hooks | `itemClassName`, `separatorClassName`, `ellipsisClassName`, `className` |

BreadcrumbItem type:

```ts
type BreadcrumbItem = {
  label: ReactNode;
  href?: string;
  isCurrent?: boolean;
  isHome?: boolean;
  icon?: ReactNode;
  showDefaultIcon?: boolean;
  onClick?: (e) => void;
  className?: string;
  testId?: string;
};
```

---

## 7. Recipes

### Next.js link

```tsx
import NextLink from 'next/link';

<Breadcrumb items={items} linkComponent={NextLink} />
```

### Custom separator

```tsx
<Breadcrumb items={items} separator="/" />
```

