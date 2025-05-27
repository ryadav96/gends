# Avatar

Circular representation of a person or entity. Supports image, initials, optional fallback icon and vibrant colour themes. Includes an **AvatarGroup** utility for stacked lists.

---

## 1. Quick start

```tsx
import { Avatar, AvatarGroup } from 'gends';

// Single avatar
<Avatar avatarName="Jane Doe" imgSrc="https://picsum.photos/200" />;

// Grouped avatars
<AvatarGroup
  avatarList=[
    { name: 'Jane Doe', image: 'https://picsum.photos/300' },
    { name: 'John Smith' },               // will render initials
    { name: 'Sam', color: 'teal' }
  ]
/>;
```

---

## 2. Sizes

| size | Diameter | Text scale |
|------|----------|------------|
| `xs` | 24 px | `body-xs` |
| `sm` | 32 px | `body-s` |
| `md` | 40 px | `body-m` (default) |
| `lg` | 48 px | `body-l` |
| `xl` | 56 px | `body-l` |

```tsx
<Avatar size="xs" initials="XS" />
<Avatar size="sm" initials="SM" />
<Avatar size="md" initials="MD" />
<Avatar size="lg" initials="LG" />
<Avatar size="xl" initials="XL" />
```

---

## 3. Colour themes

| colour | BG | Text/icon |
|--------|----|-----------|
| `default` | Primary-20 | Primary-60 |
| `yellow`  | Secondary-20 | Secondary-60 |
| `teal`    | Tertiary-20 | Tertiary-60 |
| `neutral` | Grey-20 | Grey-100 |

```tsx
<Avatar color="teal" initials="TL" />
```

---

## 4. Fallback logic

Order of precedence:

1. `imgSrc` – if provided and loads successfully.
2. `initials` – from prop or auto-generated from `name`.
3. `icon` – custom React node (defaults to <IcProfile />).

---

## 5. Interactivity

```tsx
<Avatar isClickable onClick={() => console.log('open profile')} />

<Avatar disabled avatarName="Disabled" />
```

`isClickable` adds pointer cursor + hover states. Disabled greys out and blocks events.

---

## 6. AvatarGroup

Prop | Type | Default | Description
---- | ---- | ------- | -----------
`avatarList` | `{ name; image?; initials?; color?; count? }[]` | – | Data for each bubble. `count` lets you aggregate duplicates.
`maxAvatars` | `number` | `4` | How many to render before collapsing into **+N**.
`size` | same as Avatar | `md` | Shared size.
`showCount` | `boolean` | `true` | Show **+N** overflow bubble.

```tsx
<AvatarGroup avatarList={team} maxAvatars={3} size="sm" />
```

---

## 7. Full prop reference (Avatar)

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `size` | `'xs' \| 'sm' \| 'md' \| 'lg' \| 'xl'` | `'md'` | Diameter |
| `color` | `'default' \| 'yellow' \| 'teal' \| 'neutral'` | `'default'` | Background colour theme |
| `initials` | `string` | `'NA'` | Two-letter fallback |
| `imgSrc` | `string` | – | Avatar image URL |
| `showInitials` | `boolean` | `true` | Hide initials and always show icon when `false` |
| `icon` | `ReactNode` | `<IcProfile />` | Custom fallback icon |
| `isClickable` | `boolean` | `true` | Enable pointer & hover |
| `disabled` | `boolean` | `false` | Reduce opacity & block events |
| `onClick` | `(e) => void` | – | Click handler |
| `avatarName` | `string` | – | `aria-label` text |
| `classNames` | `{ avatar; avatarImage; avatarFallback }` | – | Style hooks |

---

## 8. Recipes

### Status badge overlay

```tsx
<div className="relative inline-block">
  <Avatar size="lg" imgSrc="…" />
  <span className="absolute bottom-0 right-0 h-3 w-3 bg-green-500 rounded-full ring-2 ring-white" />
</div>
```

### Clickable group with overflow

```tsx
<AvatarGroup avatarList={developers} maxAvatars={5} onClick={openModal} />
```

---
