# Avatar Component

## Overview

The Avatar component displays user profile pictures, initials, or fallback icons in a circular format. It supports various sizes, colors, and interactive states, making it perfect for user identification across different interface contexts. The component also includes an AvatarGroup variant for displaying multiple users efficiently.

## Component API

### Avatar Props

| Prop           | Type                                           | Default         | Description                                       |
| -------------- | ---------------------------------------------- | --------------- | ------------------------------------------------- |
| `size`         | `"xs" \| "sm" \| "md" \| "lg" \| "xl"`         | `"md"`          | Size variant of the avatar                        |
| `color`        | `"default" \| "yellow" \| "teal" \| "neutral"` | `"default"`     | Color theme of the avatar background and text     |
| `initials`     | `string`                                       | `"NA"`          | Initials to display when no image is provided     |
| `imgSrc`       | `string`                                       | `""`            | URL of the avatar image                           |
| `disabled`     | `boolean`                                      | `false`         | Whether the avatar is disabled                    |
| `isClickable`  | `boolean`                                      | `true`          | Whether the avatar is clickable                   |
| `showInitials` | `boolean`                                      | `true`          | Whether to show initials instead of an icon       |
| `icon`         | `ReactNode`                                    | `<IcProfile />` | Custom icon to display when showInitials is false |
| `onClick`      | `(ev: MouseEvent<HTMLButtonElement>) => void`  | `() => {}`      | Callback function when avatar is clicked          |
| `avatarName`   | `string`                                       | `""`            | Name used for accessibility (aria-label)          |
| `id`           | `string`                                       | `""`            | ID attribute for the avatar button element        |
| `style`        | `React.CSSProperties`                          | `{}`            | Custom inline styles for the avatar               |
| `classNames`   | `ClassNames`                                   | `{}`            | Custom class names for avatar components          |

### ClassNames Interface

```typescript
interface ClassNames {
  avatarFallback?: string; // Custom classes for the fallback content
  avatarImage?: string; // Custom classes for the avatar image
  avatar?: string; // Custom classes for the avatar container
}
```

### AvatarGroup Props

| Prop         | Type                                   | Default | Description                                            |
| ------------ | -------------------------------------- | ------- | ------------------------------------------------------ |
| `avatarList` | `AvatarItem[]`                         | `[]`    | Array of user objects to display as avatars            |
| `maxAvatars` | `number`                               | `4`     | Maximum number of avatars to show before showing count |
| `size`       | `"xs" \| "sm" \| "md" \| "lg" \| "xl"` | `"md"`  | Size of all avatars in the group                       |
| `showCount`  | `boolean`                              | `true`  | Whether to show count of remaining avatars             |

### AvatarItem Interface

```typescript
interface AvatarItem {
  name: string; // User's full name
  image?: string; // URL of the user's profile image
  initials?: string; // Custom initials (auto-generated from name if not provided)
  count?: number; // Number of users this avatar represents
  color?: "default" | "yellow" | "teal" | "neutral"; // Color theme for the avatar
}
```

## Variants

### Basic Avatar with Default Settings

The default avatar with medium size and default color scheme.

```tsx
import { Avatar } from "gends";

<Avatar />;
```

### Size Variants

Avatar supports five different sizes to fit various UI contexts.

```tsx
// Extra Small (24x24px)
<Avatar size="xs" initials="XS" showInitials={true} />

// Small (32x32px)
<Avatar size="sm" initials="SM" showInitials={true} />

// Medium (40x40px) - Default
<Avatar size="md" initials="MD" showInitials={true} />

// Large (48x48px)
<Avatar size="lg" initials="LG" showInitials={true} />

// Extra Large (56x56px)
<Avatar size="xl" initials="XL" showInitials={true} />
```

### Color Themes

Avatar supports four color themes for different contexts and branding.

```tsx
// Default (Primary colors)
<Avatar color="default" initials="JD" showInitials={true} />

// Yellow (Secondary colors)
<Avatar color="yellow" initials="JS" showInitials={true} />

// Teal (Tertiary colors)
<Avatar color="teal" initials="BJ" showInitials={true} />

// Neutral (Grey colors)
<Avatar color="neutral" initials="CB" showInitials={true} />
```

### Avatar with Image

Display user profile pictures with automatic fallback to initials.

```tsx
<Avatar imgSrc="https://github.com/shadcn.png" avatarName="GitHub User" initials="GH" />
```

### Avatar with Custom Initials

Display custom initials instead of auto-generated ones.

```tsx
<Avatar initials="FY" showInitials={true} avatarName="Fynd User" color="teal" />
```

### Avatar with Custom Icon

Use custom icons instead of initials when no image is available.

```tsx
import { IcFavorite } from "gends";

<Avatar icon={<IcFavorite />} showInitials={false} avatarName="Favorite User" color="yellow" />;
```

### Interactive Avatar

Avatar with click functionality and custom event handling.

```tsx
<Avatar
  initials="CU"
  showInitials={true}
  onClick={event => {
    console.log("Avatar clicked!", event);
    // Handle avatar click - navigate to profile, show menu, etc.
  }}
  avatarName="Clickable User"
  isClickable={true}
/>
```

### Disabled Avatar

Non-interactive avatar with reduced opacity for disabled states.

```tsx
<Avatar initials="DU" showInitials={true} disabled={true} avatarName="Disabled User" />
```

### Non-Clickable Avatar

Avatar without click functionality for display-only contexts.

```tsx
<Avatar initials="NU" showInitials={true} isClickable={false} avatarName="Non-clickable User" />
```

## AvatarGroup Variants

### Basic Avatar Group

Display multiple users with automatic overflow handling.

```tsx
import { AvatarGroup } from "gends";

<AvatarGroup
  avatarList={[
    { name: "John Doe" },
    { name: "Jane Smith", initials: "JS", color: "yellow" },
    { name: "Bob Johnson", color: "teal" },
    { name: "Charlie Black", count: 3 },
  ]}
  maxAvatars={5}
  showCount={true}
/>;
```

### Avatar Group with Many Users

Handle large groups with automatic count display.

```tsx
<AvatarGroup
  avatarList={[
    { name: "User 1", color: "default" },
    { name: "User 2", color: "teal" },
    { name: "User 3", color: "yellow" },
    { name: "User 4", color: "neutral" },
    { name: "User 5", color: "default" },
    { name: "User 6", color: "teal" },
    { name: "User 7", color: "yellow" },
    { name: "User 8", color: "neutral" },
  ]}
  maxAvatars={3}
  showCount={true}
  size="sm"
/>
```

### Avatar Group with Custom Images

Mix of users with profile images and initials.

```tsx
<AvatarGroup
  avatarList={[
    {
      name: "John Doe",
      image: "https://example.com/john.jpg",
    },
    {
      name: "Jane Smith",
      initials: "JS",
      color: "yellow",
    },
    {
      name: "Bob Johnson",
      image: "https://example.com/bob.jpg",
    },
  ]}
  maxAvatars={4}
  size="lg"
/>
```

### Compact Avatar Group

Small avatar group for tight spaces.

```tsx
<AvatarGroup
  avatarList={[
    { name: "Compact User 1", color: "default" },
    { name: "Compact User 2", color: "teal" },
    { name: "Compact User 3", color: "yellow" },
  ]}
  maxAvatars={2}
  showCount={true}
  size="xs"
/>
```

## Accessibility Features

- **ARIA Labels**: Proper aria-label support for screen readers
- **Keyboard Navigation**: Full keyboard support with Tab and Enter
- **Focus Management**: Clear focus indicators with color-themed borders
- **High Contrast**: Color themes meet WCAG accessibility standards
- **Screen Reader Support**: Descriptive labels for user identification

## Styling Customization

### Custom Classes

Apply custom styling through the classNames prop.

```tsx
<Avatar
  initials="CS"
  showInitials={true}
  classNames={{
    avatar: "ring-2 ring-blue-500",
    avatarFallback: "bg-gradient-to-r from-blue-400 to-purple-500",
    avatarImage: "grayscale hover:grayscale-0 transition-all",
  }}
/>
```

### Inline Styles

Apply custom inline styles for specific use cases.

```tsx
<Avatar
  initials="IS"
  showInitials={true}
  style={{
    transform: "rotate(45deg)",
    borderRadius: "12px",
    boxShadow: "0 4px 12px rgba(0,0,0,0.15)",
  }}
/>
```

## Size and Spacing Reference

| Size | Dimensions | Use Case                   |
| ---- | ---------- | -------------------------- |
| `xs` | 24x24px    | Compact lists, dense UI    |
| `sm` | 32x32px    | Secondary elements, groups |
| `md` | 40x40px    | Default, general use       |
| `lg` | 48x48px    | Prominent placement        |
| `xl` | 56x56px    | Headers, featured content  |

## Color Theme Guide

| Theme     | Primary Use                   | Background   | Text Color   |
| --------- | ----------------------------- | ------------ | ------------ |
| `default` | General users, primary brand  | Primary-20   | Primary-60   |
| `yellow`  | Secondary brand, highlights   | Secondary-20 | Secondary-60 |
| `teal`    | Success states, special roles | Tertiary-20  | Tertiary-60  |
| `neutral` | System users, inactive states | Grey-20      | Grey-100     |

## Best Practices

### User Identification

- Always provide meaningful `avatarName` for accessibility
- Use consistent color themes across user types
- Include fallback initials for users without profile images
- Consider using images for known users, initials for new/anonymous users

### Performance Optimization

- Optimize image sources (WebP format, appropriate sizing)
- Use lazy loading for large avatar groups
- Consider virtualization for very large user lists
- Cache frequently accessed user images

### UX Guidelines

- Use larger sizes for primary user identification
- Group related users with consistent styling
- Provide hover states for interactive avatars
- Use disabled state sparingly and with clear context

### AvatarGroup Guidelines

- Keep maxAvatars reasonable (typically 3-5) for readability
- Use showCount to communicate total user participation
- Consider size based on available space and content hierarchy
- Maintain consistent spacing in grouped layouts

## Integration Examples

### User Profile Header

```tsx
<div className="flex items-center gap-4">
  <Avatar
    size="xl"
    imgSrc="https://example.com/user.jpg"
    avatarName="John Doe"
    initials="JD"
    onClick={() => navigateToProfile()}
  />
  <div>
    <h1 className="text-xl font-semibold">John Doe</h1>
    <p className="text-gray-600">Software Engineer</p>
  </div>
</div>
```

### Comment Section

```tsx
<div className="flex gap-3">
  <Avatar size="sm" initials="JS" showInitials={true} color="teal" avatarName="Jane Smith" />
  <div className="flex-1">
    <div className="bg-gray-100 rounded-lg p-3">
      <p className="font-semibold">Jane Smith</p>
      <p>This looks great! Thanks for sharing.</p>
    </div>
  </div>
</div>
```

### Team Members List

```tsx
<AvatarGroup
  avatarList={teamMembers.map(member => ({
    name: member.fullName,
    image: member.profileImage,
    color: member.role === "admin" ? "yellow" : "default",
  }))}
  maxAvatars={5}
  size="md"
  showCount={true}
/>
```

### Navigation Bar

```tsx
<nav className="flex justify-between items-center p-4">
  <Logo />
  <Avatar
    size="sm"
    imgSrc={currentUser.avatar}
    avatarName={currentUser.name}
    onClick={() => toggleUserMenu()}
    isClickable={true}
  />
</nav>
```

## Technical Notes

- Avatar uses Radix UI Avatar primitive for robust image loading and fallback handling
- Images are automatically optimized with proper aspect ratio and centering
- Focus states include 4px border with theme-appropriate colors
- AvatarGroup uses negative margin for overlapping effect (-space-x-4)
- Z-index is automatically managed in AvatarGroup for proper layering
- All sizes use Genesis spacing tokens for consistency
- Color themes utilize Genesis design system color variables
- Component is fully responsive and works across all device sizes

## Migration Guide

When upgrading from older versions:

1. Update import paths to use `gends` package
2. Replace `userName` prop with `avatarName` for consistency
3. Use `showInitials` boolean instead of `displayType` enum
4. Update color values to new theme names if using custom colors
5. Replace custom styling props with `classNames` object structure
