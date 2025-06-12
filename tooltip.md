# Tooltip Component

## Overview

The Tooltip component is a versatile contextual information overlay built on Radix UI's Tooltip primitive. It provides on-demand hints, descriptions, and additional information that appears when users hover over or focus on elements. The component offers flexible positioning, custom styling, and comprehensive accessibility support, making it perfect for enhancing user experience with contextual help.

## Component API

### Tooltip Props

| Prop             | Type                                     | Default    | Description                                      |
| ---------------- | ---------------------------------------- | ---------- | ------------------------------------------------ |
| `content`        | `React.ReactNode`                        | -          | Content to display inside the tooltip            |
| `children`       | `React.ReactNode`                        | -          | Element that triggers the tooltip                |
| `side`           | `'top' \| 'right' \| 'bottom' \| 'left'` | `'top'`    | Side where tooltip appears relative to trigger   |
| `align`          | `'start' \| 'center' \| 'end'`           | `'center'` | Alignment of tooltip relative to trigger         |
| `sideOffset`     | `number`                                 | `4`        | Offset distance between tooltip and trigger (px) |
| `className`      | `string`                                 | -          | Additional CSS classes for tooltip content       |
| `arrowClassName` | `string`                                 | -          | CSS classes for the tooltip arrow                |
| `disabled`       | `boolean`                                | `false`    | Whether the tooltip is disabled                  |
| `delayDuration`  | `number`                                 | `0`        | Delay before tooltip appears (milliseconds)      |
| `containerStyle` | `React.CSSProperties`                    | `{}`       | Style object for the tooltip container           |

### Position & Alignment Options

The Tooltip component provides comprehensive positioning control through `side` and `align` props:

| Side     | Description              | Best Used When                           |
| -------- | ------------------------ | ---------------------------------------- |
| `top`    | Appears above trigger    | Default position, sufficient space above |
| `bottom` | Appears below trigger    | Limited space above, forms               |
| `left`   | Appears left of trigger  | Right-aligned layouts, sufficient space  |
| `right`  | Appears right of trigger | Left-aligned layouts, toolbar buttons    |

| Alignment | Behavior                        | Use Cases                           |
| --------- | ------------------------------- | ----------------------------------- |
| `start`   | Aligns to start edge of trigger | Consistent left/top alignment       |
| `center`  | Centers on trigger              | Balanced appearance, default choice |
| `end`     | Aligns to end edge of trigger   | Right/bottom aligned content        |

## Basic Usage

### Simple Tooltip

```tsx
import { Tooltip } from "gends";
import { Button } from "gends";

const BasicExample = () => (
  <Tooltip content="This is a helpful tooltip">
    <Button>Hover me</Button>
  </Tooltip>
);
```

### Tooltip with Custom Content

```tsx
import { Tooltip, Button } from "gends";

const CustomContentExample = () => (
  <Tooltip
    content={
      <div className="flex items-center gap-2">
        <span>✨</span>
        <span>Enhanced tooltip with custom content</span>
      </div>
    }
  >
    <Button variant="outline">Custom tooltip</Button>
  </Tooltip>
);
```

## Position Examples

### Top Position (Default)

```tsx
const TopTooltipExample = () => (
  <div className="space-y-4">
    <Tooltip content="Default top position" side="top">
      <Button>Top tooltip</Button>
    </Tooltip>

    <Tooltip content="Top with start alignment" side="top" align="start">
      <Button>Top start</Button>
    </Tooltip>

    <Tooltip content="Top with end alignment" side="top" align="end">
      <Button>Top end</Button>
    </Tooltip>
  </div>
);
```

### Bottom Position

Perfect for dropdown menus and form elements:

```tsx
const BottomTooltipExample = () => (
  <div className="space-y-4">
    <Tooltip content="Appears below the button" side="bottom">
      <Button>Bottom tooltip</Button>
    </Tooltip>

    <Tooltip content="Form field help text appears below" side="bottom" sideOffset={8}>
      <input type="text" placeholder="Username" className="border rounded px-3 py-2" />
    </Tooltip>
  </div>
);
```

### Left Position

Ideal for right-aligned layouts:

```tsx
const LeftTooltipExample = () => (
  <div className="flex justify-end space-x-4">
    <Tooltip content="Information appears to the left" side="left">
      <Button variant="outline">Left tooltip</Button>
    </Tooltip>

    <Tooltip content="Perfect for navigation items" side="left" align="start">
      <Button size="icon">
        <IcSettings className="h-4 w-4" />
      </Button>
    </Tooltip>
  </div>
);
```

### Right Position

Great for toolbar buttons and left-aligned content:

```tsx
const RightTooltipExample = () => (
  <div className="flex space-x-4">
    <Tooltip content="Action information" side="right">
      <Button size="icon" variant="ghost">
        <IcEdit className="h-4 w-4" />
      </Button>
    </Tooltip>

    <Tooltip content="Additional details on the right" side="right" align="center">
      <Button variant="secondary">Right tooltip</Button>
    </Tooltip>
  </div>
);
```

## Advanced Features

### Custom Delay

Control when tooltips appear:

```tsx
const DelayExample = () => (
  <div className="space-x-4">
    <Tooltip content="Appears immediately" delayDuration={0}>
      <Button>No delay</Button>
    </Tooltip>

    <Tooltip content="Brief pause before showing" delayDuration={300}>
      <Button>Short delay</Button>
    </Tooltip>

    <Tooltip content="Longer pause for careful consideration" delayDuration={1000}>
      <Button>Long delay</Button>
    </Tooltip>
  </div>
);
```

### Custom Styling

```tsx
const StyledTooltipExample = () => (
  <div className="space-x-4">
    <Tooltip
      content="Success message"
      className="bg-green-600 text-white border-green-500"
      arrowClassName="fill-green-600"
    >
      <Button variant="success">Success tooltip</Button>
    </Tooltip>

    <Tooltip
      content="Warning message"
      className="bg-yellow-100 text-yellow-800 border-yellow-300"
      arrowClassName="fill-yellow-100"
    >
      <Button variant="warning">Warning tooltip</Button>
    </Tooltip>

    <Tooltip
      content="Error information"
      className="bg-red-600 text-white border-red-500"
      arrowClassName="fill-red-600"
    >
      <Button variant="destructive">Error tooltip</Button>
    </Tooltip>
  </div>
);
```

### Complex Content

Tooltips can contain rich content:

```tsx
import { IcInfo, IcUser, IcClock } from "gends";

const ComplexTooltipExample = () => (
  <div className="space-x-4">
    <Tooltip
      content={
        <div className="space-y-2">
          <div className="flex items-center gap-2">
            <IcInfo className="h-4 w-4 text-blue-500" />
            <span className="font-medium">User Information</span>
          </div>
          <div className="text-sm space-y-1">
            <div className="flex items-center gap-2">
              <IcUser className="h-3 w-3" />
              <span>John Doe</span>
            </div>
            <div className="flex items-center gap-2">
              <IcClock className="h-3 w-3" />
              <span>Last active: 2 hours ago</span>
            </div>
          </div>
        </div>
      }
      side="right"
      className="max-w-xs"
    >
      <Avatar src="/user-avatar.jpg" fallback="JD" />
    </Tooltip>

    <Tooltip
      content={
        <div className="space-y-2">
          <h4 className="font-medium">Quick Actions</h4>
          <div className="flex flex-col gap-1">
            <button className="text-left hover:bg-gray-100 px-2 py-1 rounded">Edit</button>
            <button className="text-left hover:bg-gray-100 px-2 py-1 rounded">Duplicate</button>
            <button className="text-left hover:bg-red-100 text-red-600 px-2 py-1 rounded">
              Delete
            </button>
          </div>
        </div>
      }
      side="bottom"
      className="p-2"
    >
      <Button size="icon" variant="ghost">
        <IcMoreVertical className="h-4 w-4" />
      </Button>
    </Tooltip>
  </div>
);
```

### Disabled State

```tsx
const DisabledTooltipExample = () => (
  <div className="space-x-4">
    <Tooltip content="This tooltip will show" disabled={false}>
      <Button>Active tooltip</Button>
    </Tooltip>

    <Tooltip content="This tooltip is disabled" disabled={true}>
      <Button variant="outline">No tooltip</Button>
    </Tooltip>
  </div>
);
```

### Custom Offset

Control spacing between tooltip and trigger:

```tsx
const OffsetExample = () => (
  <div className="space-x-4">
    <Tooltip content="Close to trigger" sideOffset={2}>
      <Button>Close</Button>
    </Tooltip>

    <Tooltip content="Standard spacing" sideOffset={8}>
      <Button>Normal</Button>
    </Tooltip>

    <Tooltip content="Far from trigger" sideOffset={16}>
      <Button>Far</Button>
    </Tooltip>
  </div>
);
```

## Real-World Examples

### 1. Form Field Help

```tsx
const FormFieldHelpExample = () => {
  const [username, setUsername] = useState("");
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  return (
    <form className="max-w-md mx-auto space-y-6 p-6">
      <h2 className="text-xl font-semibold mb-4">Create Account</h2>

      <div className="space-y-2">
        <label className="flex items-center gap-2 text-sm font-medium">
          Username
          <Tooltip
            content="Choose a unique username between 3-20 characters. Only letters, numbers, and underscores allowed."
            side="right"
            className="max-w-xs"
          >
            <IcInfo className="h-4 w-4 text-blue-500 cursor-help" />
          </Tooltip>
        </label>
        <input
          type="text"
          value={username}
          onChange={e => setUsername(e.target.value)}
          className="w-full border rounded-md px-3 py-2 focus:ring-2 focus:ring-blue-500"
          placeholder="Enter username"
        />
      </div>

      <div className="space-y-2">
        <label className="flex items-center gap-2 text-sm font-medium">
          Email
          <Tooltip
            content="We'll use this email for account verification and important notifications."
            side="right"
            className="max-w-xs"
          >
            <IcInfo className="h-4 w-4 text-blue-500 cursor-help" />
          </Tooltip>
        </label>
        <input
          type="email"
          value={email}
          onChange={e => setEmail(e.target.value)}
          className="w-full border rounded-md px-3 py-2 focus:ring-2 focus:ring-blue-500"
          placeholder="Enter email"
        />
      </div>

      <div className="space-y-2">
        <label className="flex items-center gap-2 text-sm font-medium">
          Password
          <Tooltip
            content={
              <div className="space-y-1">
                <div className="font-medium">Password must contain:</div>
                <ul className="text-sm space-y-1">
                  <li>• At least 8 characters</li>
                  <li>• One uppercase letter</li>
                  <li>• One lowercase letter</li>
                  <li>• One number</li>
                  <li>• One special character</li>
                </ul>
              </div>
            }
            side="right"
            className="max-w-xs"
          >
            <IcInfo className="h-4 w-4 text-blue-500 cursor-help" />
          </Tooltip>
        </label>
        <input
          type="password"
          value={password}
          onChange={e => setPassword(e.target.value)}
          className="w-full border rounded-md px-3 py-2 focus:ring-2 focus:ring-blue-500"
          placeholder="Enter password"
        />
      </div>

      <Button type="submit" className="w-full">
        Create Account
      </Button>
    </form>
  );
};
```

### 2. Toolbar with Action Tooltips

```tsx
const ToolbarExample = () => {
  const [selection, setSelection] = useState({
    bold: false,
    italic: false,
    underline: false,
  });

  const toggleFormat = format => {
    setSelection(prev => ({ ...prev, [format]: !prev[format] }));
  };

  return (
    <div className="max-w-2xl mx-auto p-6">
      <h2 className="text-xl font-semibold mb-4">Text Editor</h2>

      {/* Toolbar */}
      <div className="border rounded-lg p-2 mb-4">
        <div className="flex items-center gap-1">
          <Tooltip content="Bold (Ctrl+B)" side="bottom" delayDuration={500}>
            <Button
              size="icon"
              variant={selection.bold ? "default" : "ghost"}
              onClick={() => toggleFormat("bold")}
            >
              <IcBold className="h-4 w-4" />
            </Button>
          </Tooltip>

          <Tooltip content="Italic (Ctrl+I)" side="bottom" delayDuration={500}>
            <Button
              size="icon"
              variant={selection.italic ? "default" : "ghost"}
              onClick={() => toggleFormat("italic")}
            >
              <IcItalic className="h-4 w-4" />
            </Button>
          </Tooltip>

          <Tooltip content="Underline (Ctrl+U)" side="bottom" delayDuration={500}>
            <Button
              size="icon"
              variant={selection.underline ? "default" : "ghost"}
              onClick={() => toggleFormat("underline")}
            >
              <IcUnderline className="h-4 w-4" />
            </Button>
          </Tooltip>

          <div className="w-px h-6 bg-gray-300 mx-2" />

          <Tooltip content="Insert Link (Ctrl+K)" side="bottom" delayDuration={500}>
            <Button size="icon" variant="ghost">
              <IcLink className="h-4 w-4" />
            </Button>
          </Tooltip>

          <Tooltip content="Insert Image" side="bottom" delayDuration={500}>
            <Button size="icon" variant="ghost">
              <IcImage className="h-4 w-4" />
            </Button>
          </Tooltip>

          <div className="w-px h-6 bg-gray-300 mx-2" />

          <Tooltip
            content={
              <div className="space-y-1">
                <div className="font-medium">Text Alignment</div>
                <div className="text-sm">
                  Left (Ctrl+Shift+L)
                  <br />
                  Center (Ctrl+Shift+E)
                  <br />
                  Right (Ctrl+Shift+R)
                </div>
              </div>
            }
            side="bottom"
            className="max-w-xs"
            delayDuration={500}
          >
            <Button size="icon" variant="ghost">
              <IcAlignLeft className="h-4 w-4" />
            </Button>
          </Tooltip>

          <Tooltip content="More options" side="bottom" delayDuration={500}>
            <Button size="icon" variant="ghost">
              <IcMoreHorizontal className="h-4 w-4" />
            </Button>
          </Tooltip>
        </div>
      </div>

      {/* Editor Area */}
      <textarea
        className="w-full h-40 border rounded-lg p-4 resize-none focus:ring-2 focus:ring-blue-500"
        placeholder="Start typing your content here..."
      />
    </div>
  );
};
```

### 3. Data Table with Cell Information

```tsx
const DataTableExample = () => {
  const users = [
    {
      id: 1,
      name: "John Doe",
      email: "john@example.com",
      role: "Admin",
      status: "Active",
      lastLogin: "2024-01-15T10:30:00Z",
      permissions: ["read", "write", "delete", "manage_users"],
    },
    {
      id: 2,
      name: "Jane Smith",
      email: "jane@example.com",
      role: "Editor",
      status: "Active",
      lastLogin: "2024-01-14T15:45:00Z",
      permissions: ["read", "write"],
    },
    {
      id: 3,
      name: "Bob Johnson",
      email: "bob@example.com",
      role: "Viewer",
      status: "Inactive",
      lastLogin: "2024-01-10T09:15:00Z",
      permissions: ["read"],
    },
  ];

  const formatDate = dateString => {
    return new Date(dateString).toLocaleDateString("en-US", {
      year: "numeric",
      month: "short",
      day: "numeric",
      hour: "2-digit",
      minute: "2-digit",
    });
  };

  return (
    <div className="max-w-6xl mx-auto p-6">
      <h2 className="text-xl font-semibold mb-4">User Management</h2>

      <div className="border rounded-lg overflow-hidden">
        <table className="w-full">
          <thead className="bg-gray-50">
            <tr>
              <th className="text-left p-4 font-medium">Name</th>
              <th className="text-left p-4 font-medium">Email</th>
              <th className="text-left p-4 font-medium">Role</th>
              <th className="text-left p-4 font-medium">Status</th>
              <th className="text-left p-4 font-medium">Last Login</th>
              <th className="text-left p-4 font-medium">Actions</th>
            </tr>
          </thead>
          <tbody>
            {users.map(user => (
              <tr key={user.id} className="border-t hover:bg-gray-50">
                <td className="p-4">
                  <Tooltip
                    content={
                      <div className="space-y-2">
                        <div className="font-medium">User Details</div>
                        <div className="text-sm space-y-1">
                          <div>ID: {user.id}</div>
                          <div>Email: {user.email}</div>
                          <div>Role: {user.role}</div>
                        </div>
                      </div>
                    }
                    side="right"
                    className="max-w-xs"
                  >
                    <div className="flex items-center gap-2 cursor-help">
                      <Avatar
                        src={`/avatars/${user.id}.jpg`}
                        fallback={user.name
                          .split(" ")
                          .map(n => n[0])
                          .join("")}
                      />
                      <span>{user.name}</span>
                    </div>
                  </Tooltip>
                </td>
                <td className="p-4">{user.email}</td>
                <td className="p-4">
                  <Tooltip
                    content={
                      <div className="space-y-2">
                        <div className="font-medium">Permissions</div>
                        <ul className="text-sm space-y-1">
                          {user.permissions.map(permission => (
                            <li key={permission}>• {permission.replace("_", " ")}</li>
                          ))}
                        </ul>
                      </div>
                    }
                    side="top"
                    className="max-w-xs"
                  >
                    <Badge
                      variant={
                        user.role === "Admin"
                          ? "default"
                          : user.role === "Editor"
                            ? "secondary"
                            : "outline"
                      }
                    >
                      {user.role}
                    </Badge>
                  </Tooltip>
                </td>
                <td className="p-4">
                  <Badge variant={user.status === "Active" ? "success" : "secondary"}>
                    {user.status}
                  </Badge>
                </td>
                <td className="p-4">
                  <Tooltip content={`Full timestamp: ${formatDate(user.lastLogin)}`} side="top">
                    <span className="text-sm text-gray-600 cursor-help">
                      {formatDate(user.lastLogin).split(",")[0]}
                    </span>
                  </Tooltip>
                </td>
                <td className="p-4">
                  <div className="flex gap-2">
                    <Tooltip content="Edit user" side="top">
                      <Button size="icon" variant="ghost">
                        <IcEdit className="h-4 w-4" />
                      </Button>
                    </Tooltip>
                    <Tooltip content="Delete user" side="top">
                      <Button size="icon" variant="ghost">
                        <IcTrash className="h-4 w-4" />
                      </Button>
                    </Tooltip>
                  </div>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
};
```

### 4. Navigation with Contextual Help

```tsx
const NavigationExample = () => {
  const [currentPage, setCurrentPage] = useState("dashboard");

  const navigationItems = [
    {
      id: "dashboard",
      label: "Dashboard",
      icon: IcHome,
      description: "Overview of your account activity, recent transactions, and quick stats.",
      shortcut: "Ctrl+D",
    },
    {
      id: "projects",
      label: "Projects",
      icon: IcFolder,
      description: "Manage your projects, create new ones, and collaborate with team members.",
      shortcut: "Ctrl+P",
    },
    {
      id: "tasks",
      label: "Tasks",
      icon: IcCheckSquare,
      description: "View and manage your personal tasks and assignments.",
      shortcut: "Ctrl+T",
    },
    {
      id: "calendar",
      label: "Calendar",
      icon: IcCalendar,
      description: "Schedule meetings, view deadlines, and manage your time effectively.",
      shortcut: "Ctrl+Shift+C",
    },
    {
      id: "analytics",
      label: "Analytics",
      icon: IcBarChart,
      description:
        "Detailed reports and insights about your project performance and team productivity.",
      shortcut: "Ctrl+A",
    },
    {
      id: "settings",
      label: "Settings",
      icon: IcSettings,
      description: "Configure your account preferences, team settings, and application options.",
      shortcut: "Ctrl+,",
    },
  ];

  return (
    <div className="flex h-screen">
      {/* Sidebar */}
      <div className="w-64 bg-gray-900 text-white p-4">
        <h1 className="text-xl font-bold mb-8">MyApp</h1>

        <nav className="space-y-2">
          {navigationItems.map(item => {
            const Icon = item.icon;
            const isActive = currentPage === item.id;

            return (
              <Tooltip
                key={item.id}
                content={
                  <div className="space-y-2">
                    <div className="flex items-center justify-between gap-4">
                      <span className="font-medium">{item.label}</span>
                      <kbd className="text-xs bg-gray-700 px-2 py-1 rounded">{item.shortcut}</kbd>
                    </div>
                    <p className="text-sm">{item.description}</p>
                  </div>
                }
                side="right"
                className="max-w-xs"
                delayDuration={300}
              >
                <button
                  onClick={() => setCurrentPage(item.id)}
                  className={`w-full flex items-center gap-3 px-3 py-2 rounded-lg transition-colors ${
                    isActive
                      ? "bg-blue-600 text-white"
                      : "text-gray-300 hover:bg-gray-800 hover:text-white"
                  }`}
                >
                  <Icon className="h-5 w-5" />
                  <span>{item.label}</span>
                </button>
              </Tooltip>
            );
          })}
        </nav>

        <div className="mt-8 pt-8 border-t border-gray-700">
          <Tooltip
            content={
              <div className="space-y-2">
                <div className="font-medium">Help & Support</div>
                <div className="text-sm space-y-1">
                  <div>• Documentation</div>
                  <div>• Video tutorials</div>
                  <div>• Contact support</div>
                  <div>• Feature requests</div>
                </div>
              </div>
            }
            side="right"
            className="max-w-xs"
          >
            <button className="w-full flex items-center gap-3 px-3 py-2 rounded-lg text-gray-300 hover:bg-gray-800 hover:text-white transition-colors">
              <IcHelpCircle className="h-5 w-5" />
              <span>Help</span>
            </button>
          </Tooltip>
        </div>
      </div>

      {/* Main Content */}
      <div className="flex-1 p-8">
        <h2 className="text-2xl font-bold mb-4 capitalize">{currentPage}</h2>
        <p className="text-gray-600">
          This is the {currentPage} page. Navigate using the sidebar or keyboard shortcuts.
        </p>
      </div>
    </div>
  );
};
```

### 5. Status Indicators with Detailed Information

```tsx
const StatusIndicatorsExample = () => {
  const systems = [
    {
      name: "API Gateway",
      status: "operational",
      uptime: "99.98%",
      responseTime: "45ms",
      lastIncident: "None in the last 30 days",
      details:
        "All API endpoints are responding normally. Average response time is well within acceptable limits.",
    },
    {
      name: "Database",
      status: "operational",
      uptime: "99.95%",
      responseTime: "12ms",
      lastIncident: "2 days ago - Brief maintenance",
      details:
        "Database performance is optimal. Recent maintenance improved query execution times by 15%.",
    },
    {
      name: "CDN",
      status: "degraded",
      uptime: "99.87%",
      responseTime: "120ms",
      lastIncident: "Ongoing - Investigating slow responses",
      details:
        "Some edge locations experiencing higher than normal latency. Engineers are investigating the cause.",
    },
    {
      name: "Email Service",
      status: "maintenance",
      uptime: "99.92%",
      responseTime: "N/A",
      lastIncident: "Scheduled maintenance in progress",
      details:
        "Planned maintenance to upgrade email infrastructure. Service will be restored within 2 hours.",
    },
    {
      name: "Authentication",
      status: "operational",
      uptime: "99.99%",
      responseTime: "25ms",
      lastIncident: "None in the last 90 days",
      details: "Authentication service is performing excellently with no recent issues reported.",
    },
  ];

  const getStatusColor = status => {
    switch (status) {
      case "operational":
        return "green";
      case "degraded":
        return "yellow";
      case "maintenance":
        return "blue";
      case "outage":
        return "red";
      default:
        return "gray";
    }
  };

  const getStatusIcon = status => {
    switch (status) {
      case "operational":
        return <IcCheckCircle className="h-4 w-4" />;
      case "degraded":
        return <IcAlertTriangle className="h-4 w-4" />;
      case "maintenance":
        return <IcTool className="h-4 w-4" />;
      case "outage":
        return <IcXCircle className="h-4 w-4" />;
      default:
        return <IcHelpCircle className="h-4 w-4" />;
    }
  };

  return (
    <div className="max-w-4xl mx-auto p-6">
      <h2 className="text-2xl font-bold mb-6">System Status</h2>

      <div className="grid gap-4">
        {systems.map(system => {
          const color = getStatusColor(system.status);
          const icon = getStatusIcon(system.status);

          return (
            <div key={system.name} className="border rounded-lg p-4">
              <div className="flex items-center justify-between">
                <div className="flex items-center gap-3">
                  <Tooltip
                    content={
                      <div className="space-y-3">
                        <div className="font-medium">{system.name} Details</div>
                        <div className="space-y-2 text-sm">
                          <div className="flex justify-between gap-4">
                            <span>Status:</span>
                            <span className="capitalize font-medium">{system.status}</span>
                          </div>
                          <div className="flex justify-between gap-4">
                            <span>Uptime (30d):</span>
                            <span className="font-medium">{system.uptime}</span>
                          </div>
                          <div className="flex justify-between gap-4">
                            <span>Response Time:</span>
                            <span className="font-medium">{system.responseTime}</span>
                          </div>
                          <div className="border-t pt-2">
                            <div className="font-medium mb-1">Last Incident:</div>
                            <div>{system.lastIncident}</div>
                          </div>
                          <div className="border-t pt-2">
                            <div className="font-medium mb-1">Details:</div>
                            <div>{system.details}</div>
                          </div>
                        </div>
                      </div>
                    }
                    side="right"
                    className="max-w-sm"
                  >
                    <div className={`flex items-center gap-2 text-${color}-600 cursor-help`}>
                      {icon}
                      <span className="font-medium">{system.name}</span>
                    </div>
                  </Tooltip>
                </div>

                <div className="flex items-center gap-4">
                  <Tooltip
                    content={`Average response time over the last 24 hours: ${system.responseTime}`}
                    side="left"
                  >
                    <div className="text-sm text-gray-600 cursor-help">
                      {system.responseTime !== "N/A" ? `${system.responseTime} avg` : "Offline"}
                    </div>
                  </Tooltip>

                  <Tooltip
                    content={`System uptime percentage over the last 30 days: ${system.uptime}`}
                    side="left"
                  >
                    <Badge
                      variant={
                        system.status === "operational"
                          ? "success"
                          : system.status === "degraded"
                            ? "warning"
                            : system.status === "maintenance"
                              ? "secondary"
                              : "destructive"
                      }
                      className="cursor-help"
                    >
                      {system.uptime}
                    </Badge>
                  </Tooltip>
                </div>
              </div>
            </div>
          );
        })}
      </div>

      <div className="mt-8 p-4 bg-gray-50 rounded-lg">
        <div className="flex items-center gap-2 mb-3">
          <IcInfo className="h-5 w-5 text-blue-500" />
          <span className="font-medium">Status Legend</span>
        </div>
        <div className="grid grid-cols-2 md:grid-cols-4 gap-4 text-sm">
          <Tooltip content="All systems functioning normally" side="top">
            <div className="flex items-center gap-2 cursor-help">
              <IcCheckCircle className="h-4 w-4 text-green-600" />
              <span>Operational</span>
            </div>
          </Tooltip>
          <Tooltip content="Some functionality may be impacted" side="top">
            <div className="flex items-center gap-2 cursor-help">
              <IcAlertTriangle className="h-4 w-4 text-yellow-600" />
              <span>Degraded</span>
            </div>
          </Tooltip>
          <Tooltip content="Scheduled maintenance in progress" side="top">
            <div className="flex items-center gap-2 cursor-help">
              <IcTool className="h-4 w-4 text-blue-600" />
              <span>Maintenance</span>
            </div>
          </Tooltip>
          <Tooltip content="Service is currently unavailable" side="top">
            <div className="flex items-center gap-2 cursor-help">
              <IcXCircle className="h-4 w-4 text-red-600" />
              <span>Outage</span>
            </div>
          </Tooltip>
        </div>
      </div>
    </div>
  );
};
```

## Accessibility Features

The Tooltip component includes comprehensive accessibility support following WAI-ARIA guidelines:

### Keyboard Navigation

- **Tab**: Navigate to tooltip triggers
- **Enter/Space**: Activate tooltip when trigger is focused
- **Escape**: Close tooltip
- **Arrow Keys**: Navigate within tooltip content (if interactive)

### Screen Reader Support

- Automatic `role="tooltip"` assignment
- `aria-describedby` linking between trigger and content
- Proper focus management
- Content announced when tooltip appears

### Visual Accessibility

- High contrast support
- Respects reduced motion preferences
- Adequate color contrast ratios
- Clear focus indicators

```tsx
// Accessibility example
<Tooltip content="Accessible tooltip with proper ARIA labels" delayDuration={100}>
  <Button
    aria-label="More information about this feature"
    className="focus:ring-2 focus:ring-blue-500"
  >
    <IcInfo className="h-4 w-4" />
  </Button>
</Tooltip>
```

## Genesis Design System Integration

### Design Tokens

The Tooltip component leverages Genesis design tokens for consistent theming:

```tsx
// CSS custom properties used internally
const tooltipTokens = {
  // Colors
  background: "var(--gd-background-primary)",
  foreground: "var(--gd-text-primary)",
  border: "var(--gd-border-default)",

  // Shadows
  shadow: "var(--gd-shadow-lg)",

  // Spacing
  padding: "var(--gd-spacing-12) var(--gd-spacing-16)",
  borderRadius: "var(--gd-radius-md)",

  // Typography
  fontSize: "var(--gd-text-sm)",
  lineHeight: "var(--gd-leading-normal)",
};
```

### Component Integration

```tsx
// Seamless integration with other Genesis components
const IntegratedExample = () => (
  <Card className="p-6">
    <CardHeader>
      <div className="flex items-center gap-2">
        <h3 className="text-en-desktop-heading-xl">Project Settings</h3>
        <Tooltip content="Configure your project preferences and team settings">
          <IcInfo className="h-5 w-5 text-blue-500" />
        </Tooltip>
      </div>
    </CardHeader>
    <CardContent className="space-y-4">
      <div className="flex items-center justify-between">
        <span>Public project</span>
        <Tooltip content="Make this project visible to all team members">
          <Toggle defaultChecked={false} />
        </Tooltip>
      </div>
      <div className="flex items-center justify-between">
        <span>Enable notifications</span>
        <Tooltip content="Receive updates about project activity">
          <Toggle defaultChecked={true} />
        </Tooltip>
      </div>
    </CardContent>
  </Card>
);
```

## Best Practices

### Content Guidelines

```tsx
// ✅ Good: Concise, helpful information
<Tooltip content="Save changes (Ctrl+S)">
  <Button>Save</Button>
</Tooltip>

// ✅ Good: Structured content for complex information
<Tooltip
  content={
    <div>
      <div className="font-medium">Keyboard Shortcuts</div>
      <div className="text-sm mt-1">
        Save: Ctrl+S<br/>
        Undo: Ctrl+Z<br/>
        Redo: Ctrl+Y
      </div>
    </div>
  }
>
  <Button>Actions</Button>
</Tooltip>

// ❌ Avoid: Redundant information
<Tooltip content="Click this button">
  <Button>Click me</Button>
</Tooltip>
```

### Positioning Strategy

```tsx
// ✅ Good: Consider available space
const SmartPositioning = ({ preferredSide = "top" }) => (
  <Tooltip
    content="This tooltip adjusts position based on available space"
    side={preferredSide}
    // Radix automatically handles collision detection
  >
    <Button>Smart tooltip</Button>
  </Tooltip>
);

// ✅ Good: Consistent alignment for related elements
<div className="flex gap-2">
  <Tooltip content="First action" side="bottom" align="center">
    <Button>Action 1</Button>
  </Tooltip>
  <Tooltip content="Second action" side="bottom" align="center">
    <Button>Action 2</Button>
  </Tooltip>
</div>;
```

### Performance Optimization

```tsx
// ✅ Good: Memoized tooltip content for complex renders
const OptimizedTooltip = memo(({ data, children }) => {
  const tooltipContent = useMemo(
    () => (
      <div className="space-y-1">
        <div className="font-medium">{data.title}</div>
        <div className="text-sm">{data.description}</div>
      </div>
    ),
    [data.title, data.description]
  );

  return <Tooltip content={tooltipContent}>{children}</Tooltip>;
});

// ✅ Good: Appropriate delay for frequent interactions
<Tooltip content="Frequent action" delayDuration={100}>
  <Button>Quick action</Button>
</Tooltip>;
```

## Common Pitfalls & Troubleshooting

### Content Overflow

```tsx
// ❌ Problem: Very long content without width constraints
<Tooltip content="This is an extremely long tooltip that could extend beyond the viewport width and become difficult to read">
  <Button>Long tooltip</Button>
</Tooltip>

// ✅ Solution: Set maximum width and allow wrapping
<Tooltip
  content="This is an extremely long tooltip that could extend beyond the viewport width and become difficult to read"
  className="max-w-xs"
>
  <Button>Constrained tooltip</Button>
</Tooltip>
```

### Interactive Content Issues

```tsx
// ❌ Problem: Complex interactive content that's hard to use
<Tooltip
  content={
    <div>
      <button onClick={() => doSomething()}>
        This button is hard to click
      </button>
    </div>
  }
>
  <Button>Bad interactive tooltip</Button>
</Tooltip>

// ✅ Solution: Use popovers for interactive content
<Popover>
  <PopoverTrigger>
    <Button>Interactive content</Button>
  </PopoverTrigger>
  <PopoverContent>
    <div className="space-y-2">
      <Button onClick={() => doSomething()}>
        Easy to click
      </Button>
    </div>
  </PopoverContent>
</Popover>
```

### Mobile Touch Considerations

```tsx
// ❌ Problem: Tooltip on mobile without alternative
<Tooltip content="Hidden on mobile" side="top">
  <Button>Mobile unfriendly</Button>
</Tooltip>;

// ✅ Solution: Provide alternative for mobile
const MobileFriendlyTooltip = ({ content, children }) => {
  const [isMobile, setIsMobile] = useState(false);

  useEffect(() => {
    setIsMobile("ontouchstart" in window);
  }, []);

  if (isMobile) {
    return (
      <Popover>
        <PopoverTrigger>{children}</PopoverTrigger>
        <PopoverContent>{content}</PopoverContent>
      </Popover>
    );
  }

  return <Tooltip content={content}>{children}</Tooltip>;
};
```

## Migration Guide

### From Basic Title Attributes

```tsx
// Legacy HTML title attribute
<button title="Save your work">
  Save
</button>

// Migrate to Genesis Tooltip
<Tooltip content="Save your work">
  <Button>Save</Button>
</Tooltip>
```

### From Other Tooltip Libraries

```tsx
// React Tooltip example
<ReactTooltip id="example" />
<button data-tip="Tooltip content" data-for="example">
  Button
</button>

// Genesis Tooltip equivalent
<Tooltip content="Tooltip content">
  <Button>Button</Button>
</Tooltip>
```

### TypeScript Integration

```tsx
interface TooltipWrapperProps {
  content: React.ReactNode;
  children: React.ReactNode;
  position?: "top" | "right" | "bottom" | "left";
  delay?: number;
}

const TooltipWrapper: React.FC<TooltipWrapperProps> = ({
  content,
  children,
  position = "top",
  delay = 0,
}) => (
  <Tooltip content={content} side={position} delayDuration={delay}>
    {children}
  </Tooltip>
);

// Usage with type safety
<TooltipWrapper content="Type-safe tooltip" position="right" delay={300}>
  <Button>TypeScript button</Button>
</TooltipWrapper>;
```

## Conclusion

The Genesis Tooltip component provides a robust, accessible solution for contextual information display across various application contexts. Its comprehensive positioning system, custom styling capabilities, and seamless integration with the Genesis Design System make it suitable for everything from simple help text to complex interactive interfaces. The component's built-in accessibility features and thoughtful API design ensure excellent user experience across all devices and user needs.
