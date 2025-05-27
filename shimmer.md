# Shimmer

Simple skeleton placeholder used while content is loading. Thin wrapper around the `Skeleton` primitive with configurable size, colour and border‐radius.

---

## 1. Quick start

```tsx
import Shimmer from '@/components/genesis/atoms/shimmer/shimmer';

<Shimmer height="20px" width="100%" />
```

---

## 2. Customisation

Prop | Default | Description
---- | ------- | -----------
`width` | `'100%'` | Any CSS length
`height` | `'1rem'` | Any CSS length
`backgroundColor` | `#e0e0e0` | Fallback when theme token not required
`borderRadius` | `4px` | Same syntax as CSS `border-radius`

`className` and `style` are forwarded to the underlying `<div>`.

---

## 3. Recipes

### Article placeholder

```tsx
<article>
  <Shimmer height="36px" width="70%" />
  <div className="space-y-2 mt-4">
    {Array.from({ length: 5 }).map((_, i) => (
      <Shimmer key={i} height="14px" />
    ))}
  </div>
</article>
```

### Avatar skeleton circle

```tsx
<Shimmer width="40px" height="40px" borderRadius="50%" />
```

---