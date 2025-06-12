# Toggle Component

## Overview

The Toggle component is a versatile binary input control built on Radix UI Switch primitive, designed for enabling and disabling settings, preferences, and features. It provides a clean, accessible way to manage boolean states with support for multiple sizes, validation states, and label configurations. Perfect for user preferences, feature toggles, and settings panels.

## Component API

### Toggle Props

| Prop                | Type                                             | Default     | Description                            |
| ------------------- | ------------------------------------------------ | ----------- | -------------------------------------- |
| `defaultChecked`    | `boolean`                                        | `false`     | Initial checked state                  |
| `onChange`          | `(checked: boolean) => void`                     | -           | Callback when toggle state changes     |
| `disabled`          | `boolean`                                        | `false`     | Disables the toggle                    |
| `label`             | `string`                                         | -           | Label text for the toggle              |
| `icon`              | `React.ReactNode`                                | -           | Icon displayed with the label          |
| `labelPosition`     | `'left' \| 'right' \| 'none'`                    | `'left'`    | Position of label relative to toggle   |
| `validationState`   | `'default' \| 'success' \| 'warning' \| 'error'` | `'default'` | Visual validation state                |
| `validationMessage` | `string`                                         | -           | Helper text displayed below toggle     |
| `helperIcon`        | `React.ReactNode`                                | -           | Icon displayed with validation message |
| `size`              | `'sm' \| 'md' \| 'lg'`                           | `'md'`      | Size variant of the toggle             |
| `className`         | `string`                                         | -           | Additional CSS classes                 |
| `labelClassName`    | `string`                                         | -           | CSS classes for the label              |
| `id`                | `string`                                         | `'toggle'`  | HTML ID attribute                      |
| `name`              | `string`                                         | -           | HTML name attribute for forms          |

### Size Variants

The Toggle component offers three size options for different interface contexts:

| Size | Toggle Size | Knob Size | Typography               | Height | Use Cases                    |
| ---- | ----------- | --------- | ------------------------ | ------ | ---------------------------- |
| `sm` | 28×16px     | 8×8px     | `text-en-desktop-body-m` | 16px   | Compact lists, dense layouts |
| `md` | 36×20px     | 12×12px   | `text-en-desktop-body-m` | 20px   | Standard forms, settings     |
| `lg` | 44×24px     | 16×16px   | `text-en-desktop-body-l` | 24px   | Prominent settings, headers  |

### Validation States

Visual feedback states for different contexts and validation results:

| State     | Purpose                | Text Color                        | Icon Color                       |
| --------- | ---------------------- | --------------------------------- | -------------------------------- |
| `default` | Normal state           | `text-color-neutral-grey-80`      | N/A                              |
| `success` | Successful validation  | `text-color-text-success-subdued` | `text-color-feedback-success-50` |
| `warning` | Warning or caution     | `text-color-text-warning-subdued` | `text-color-feedback-warning-50` |
| `error`   | Error or invalid input | `text-color-text-error-subdued`   | `text-color-feedback-error-50`   |

### Label Positions

Control label placement for optimal layout integration:

| Position | Behavior                             | Use Cases                          |
| -------- | ------------------------------------ | ---------------------------------- |
| `left`   | Label appears to the left of toggle  | Standard form layouts              |
| `right`  | Label appears to the right of toggle | Right-aligned layouts, table cells |
| `none`   | No label displayed                   | Custom layouts, icon-only toggles  |

## Basic Usage

### Simple Toggle

```tsx
import { Toggle } from "gends";

const BasicExample = () => {
  const [enabled, setEnabled] = useState(false);

  return <Toggle label="Enable notifications" checked={enabled} onChange={setEnabled} />;
};
```

### Toggle with Icon

```tsx
import { Toggle } from "gends";
import { IcBell } from "gends";

const IconToggleExample = () => {
  const [notifications, setNotifications] = useState(true);

  return (
    <Toggle
      label="Push notifications"
      icon={<IcBell className="h-gd-16 w-gd-16" />}
      defaultChecked={notifications}
      onChange={setNotifications}
      size="lg"
    />
  );
};
```

## Size Examples

### Small Toggle

Perfect for compact interfaces and dense layouts:

```tsx
const SmallToggleExample = () => (
  <div className="space-y-2">
    <Toggle size="sm" label="Compact setting" defaultChecked={false} />
    <Toggle size="sm" label="Auto-save" defaultChecked={true} />
  </div>
);
```

### Medium Toggle (Default)

Standard size for most form and settings contexts:

```tsx
const MediumToggleExample = () => (
  <div className="space-y-4">
    <Toggle size="md" label="Email notifications" defaultChecked={true} />
    <Toggle size="md" label="Dark mode" defaultChecked={false} />
  </div>
);
```

### Large Toggle

Prominent toggles for important settings:

```tsx
const LargeToggleExample = () => (
  <div className="space-y-6">
    <Toggle size="lg" label="Enable two-factor authentication" defaultChecked={false} />
    <Toggle size="lg" label="Public profile" defaultChecked={true} />
  </div>
);
```

## Label Position Examples

### Left-positioned Labels

Standard layout with labels on the left:

```tsx
const LeftLabelExample = () => (
  <div className="space-y-4">
    <Toggle label="Marketing emails" labelPosition="left" defaultChecked={true} />
    <Toggle label="SMS notifications" labelPosition="left" defaultChecked={false} />
  </div>
);
```

### Right-positioned Labels

Alternative layout with labels on the right:

```tsx
const RightLabelExample = () => (
  <div className="space-y-4">
    <Toggle label="Auto-backup" labelPosition="right" defaultChecked={true} />
    <Toggle label="Sync settings" labelPosition="right" defaultChecked={false} />
  </div>
);
```

### No Label (Custom Layout)

Toggle without built-in label for custom layouts:

```tsx
const NoLabelExample = () => (
  <div className="flex items-center justify-between p-4 border rounded-lg">
    <div>
      <h3 className="font-medium">Privacy Mode</h3>
      <p className="text-sm text-color-neutral-grey-70">Hide your online status from other users</p>
    </div>
    <Toggle labelPosition="none" defaultChecked={false} size="lg" />
  </div>
);
```

## Validation State Examples

### Success State

Indicates successful validation or confirmed state:

```tsx
import { IcSuccess } from "gends";

const SuccessStateExample = () => (
  <Toggle
    label="Account verified"
    validationState="success"
    validationMessage="Your account has been successfully verified"
    helperIcon={<IcSuccess className="h-gd-16 w-gd-16" />}
    defaultChecked={true}
    disabled
  />
);
```

### Warning State

Shows caution or important information:

```tsx
import { IcWarning } from "gends";

const WarningStateExample = () => (
  <Toggle
    label="Beta features"
    validationState="warning"
    validationMessage="Beta features may be unstable and subject to change"
    helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
    defaultChecked={false}
  />
);
```

### Error State

Indicates validation errors or problems:

```tsx
import { IcWarning } from "gends";

const ErrorStateExample = () => (
  <Toggle
    label="Public API access"
    validationState="error"
    validationMessage="API access requires account verification"
    helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
    defaultChecked={false}
    disabled
  />
);
```

## Advanced Features

### Disabled States

```tsx
const DisabledExample = () => (
  <div className="space-y-4">
    <Toggle label="Disabled unchecked" disabled defaultChecked={false} />
    <Toggle label="Disabled checked" disabled defaultChecked={true} />
  </div>
);
```

### Controlled Toggle

```tsx
const ControlledExample = () => {
  const [isEnabled, setIsEnabled] = useState(false);
  const [lastChanged, setLastChanged] = useState(null);

  const handleChange = checked => {
    setIsEnabled(checked);
    setLastChanged(new Date().toLocaleTimeString());
  };

  return (
    <div className="space-y-4">
      <Toggle label="Controlled toggle" checked={isEnabled} onChange={handleChange} />
      <div className="text-sm text-color-neutral-grey-70">
        Status: {isEnabled ? "Enabled" : "Disabled"}
        {lastChanged && ` (changed at ${lastChanged})`}
      </div>
    </div>
  );
};
```

### Form Integration

```tsx
const FormExample = () => {
  const [formData, setFormData] = useState({
    notifications: true,
    marketing: false,
    newsletter: true,
  });

  const updateSetting = (key, value) => {
    setFormData(prev => ({ ...prev, [key]: value }));
  };

  return (
    <form className="space-y-6">
      <div className="space-y-4">
        <h3 className="text-lg font-medium">Communication Preferences</h3>

        <Toggle
          id="notifications"
          name="notifications"
          label="Email notifications"
          checked={formData.notifications}
          onChange={checked => updateSetting("notifications", checked)}
        />

        <Toggle
          id="marketing"
          name="marketing"
          label="Marketing emails"
          checked={formData.marketing}
          onChange={checked => updateSetting("marketing", checked)}
          validationMessage="Receive updates about new features and promotions"
        />

        <Toggle
          id="newsletter"
          name="newsletter"
          label="Monthly newsletter"
          checked={formData.newsletter}
          onChange={checked => updateSetting("newsletter", checked)}
        />
      </div>

      <Button type="submit">Save Preferences</Button>
    </form>
  );
};
```

## Real-World Examples

### 1. User Settings Panel

```tsx
const UserSettingsPanel = () => {
  const [settings, setSettings] = useState({
    darkMode: false,
    notifications: true,
    autoSave: true,
    publicProfile: false,
    twoFactor: false,
  });

  const updateSetting = (key, value) => {
    setSettings(prev => ({ ...prev, [key]: value }));
  };

  return (
    <div className="max-w-md mx-auto p-6 bg-white rounded-lg shadow">
      <h2 className="text-xl font-semibold mb-6">Account Settings</h2>

      <div className="space-y-6">
        <div>
          <h3 className="text-sm font-medium text-color-neutral-grey-80 mb-3">Appearance</h3>
          <Toggle
            label="Dark mode"
            icon={<IcMoon className="h-gd-16 w-gd-16" />}
            checked={settings.darkMode}
            onChange={checked => updateSetting("darkMode", checked)}
            size="lg"
          />
        </div>

        <div>
          <h3 className="text-sm font-medium text-color-neutral-grey-80 mb-3">Notifications</h3>
          <div className="space-y-3">
            <Toggle
              label="Push notifications"
              icon={<IcBell className="h-gd-16 w-gd-16" />}
              checked={settings.notifications}
              onChange={checked => updateSetting("notifications", checked)}
            />
            <Toggle
              label="Auto-save documents"
              checked={settings.autoSave}
              onChange={checked => updateSetting("autoSave", checked)}
              validationMessage="Automatically save your work every 5 minutes"
            />
          </div>
        </div>

        <div>
          <h3 className="text-sm font-medium text-color-neutral-grey-80 mb-3">Privacy</h3>
          <div className="space-y-3">
            <Toggle
              label="Public profile"
              checked={settings.publicProfile}
              onChange={checked => updateSetting("publicProfile", checked)}
              validationState="warning"
              validationMessage="Your profile will be visible to all users"
              helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
            />
            <Toggle
              label="Two-factor authentication"
              checked={settings.twoFactor}
              onChange={checked => updateSetting("twoFactor", checked)}
              validationState="success"
              validationMessage="Recommended for enhanced security"
              helperIcon={<IcSuccess className="h-gd-16 w-gd-16" />}
              size="lg"
            />
          </div>
        </div>
      </div>
    </div>
  );
};
```

### 2. Feature Flags Dashboard

```tsx
const FeatureFlagsPanel = () => {
  const [features, setFeatures] = useState([
    {
      id: "new-editor",
      name: "New Editor",
      description: "Enhanced text editor with collaboration features",
      enabled: false,
      status: "beta",
    },
    {
      id: "ai-assistant",
      name: "AI Assistant",
      description: "AI-powered writing and code suggestions",
      enabled: true,
      status: "stable",
    },
    {
      id: "advanced-analytics",
      name: "Advanced Analytics",
      description: "Detailed usage statistics and performance metrics",
      enabled: false,
      status: "experimental",
    },
  ]);

  const toggleFeature = (featureId, enabled) => {
    setFeatures(prev =>
      prev.map(feature => (feature.id === featureId ? { ...feature, enabled } : feature))
    );
  };

  const getValidationState = status => {
    switch (status) {
      case "stable":
        return "success";
      case "beta":
        return "warning";
      case "experimental":
        return "error";
      default:
        return "default";
    }
  };

  const getStatusMessage = status => {
    switch (status) {
      case "stable":
        return "Production ready";
      case "beta":
        return "May have minor issues";
      case "experimental":
        return "Use with caution - may be unstable";
      default:
        return "";
    }
  };

  return (
    <div className="max-w-2xl mx-auto p-6">
      <h2 className="text-2xl font-bold mb-6">Feature Flags</h2>

      <div className="space-y-6">
        {features.map(feature => (
          <div key={feature.id} className="border rounded-lg p-4">
            <div className="flex items-start justify-between">
              <div className="flex-1">
                <div className="flex items-center gap-2 mb-2">
                  <h3 className="font-medium">{feature.name}</h3>
                  <Badge
                    appearance={
                      feature.status === "stable"
                        ? "Success"
                        : feature.status === "beta"
                          ? "Warning"
                          : "Error"
                    }
                    text={feature.status}
                    size="s"
                  />
                </div>
                <p className="text-sm text-color-neutral-grey-70 mb-4">{feature.description}</p>
              </div>
            </div>

            <Toggle
              label={`Enable ${feature.name}`}
              labelPosition="none"
              checked={feature.enabled}
              onChange={enabled => toggleFeature(feature.id, enabled)}
              validationState={getValidationState(feature.status)}
              validationMessage={getStatusMessage(feature.status)}
              helperIcon={
                feature.status === "stable" ? (
                  <IcSuccess className="h-gd-16 w-gd-16" />
                ) : (
                  <IcWarning className="h-gd-16 w-gd-16" />
                )
              }
              size="lg"
            />
          </div>
        ))}
      </div>
    </div>
  );
};
```

### 3. Notification Preferences

```tsx
const NotificationPreferences = () => {
  const [preferences, setPreferences] = useState({
    email: {
      marketing: false,
      security: true,
      updates: true,
      newsletter: false,
    },
    push: {
      messages: true,
      mentions: true,
      comments: false,
      likes: false,
    },
    sms: {
      security: true,
      reminders: false,
    },
  });

  const updatePreference = (category, key, value) => {
    setPreferences(prev => ({
      ...prev,
      [category]: { ...prev[category], [key]: value },
    }));
  };

  return (
    <div className="max-w-lg mx-auto p-6">
      <h2 className="text-xl font-semibold mb-6">Notification Preferences</h2>

      <div className="space-y-8">
        <section>
          <h3 className="text-lg font-medium mb-4 flex items-center gap-2">
            <IcMail className="h-5 w-5" />
            Email Notifications
          </h3>
          <div className="space-y-3 pl-7">
            <Toggle
              label="Marketing emails"
              checked={preferences.email.marketing}
              onChange={checked => updatePreference("email", "marketing", checked)}
              validationMessage="Promotions, new features, and special offers"
            />
            <Toggle
              label="Security alerts"
              checked={preferences.email.security}
              onChange={checked => updatePreference("email", "security", checked)}
              validationState="success"
              validationMessage="Login attempts and security updates"
              helperIcon={<IcSuccess className="h-gd-16 w-gd-16" />}
            />
            <Toggle
              label="Product updates"
              checked={preferences.email.updates}
              onChange={checked => updatePreference("email", "updates", checked)}
              validationMessage="New features and improvements"
            />
            <Toggle
              label="Monthly newsletter"
              checked={preferences.email.newsletter}
              onChange={checked => updatePreference("email", "newsletter", checked)}
            />
          </div>
        </section>

        <section>
          <h3 className="text-lg font-medium mb-4 flex items-center gap-2">
            <IcBell className="h-5 w-5" />
            Push Notifications
          </h3>
          <div className="space-y-3 pl-7">
            <Toggle
              label="Direct messages"
              checked={preferences.push.messages}
              onChange={checked => updatePreference("push", "messages", checked)}
              size="lg"
            />
            <Toggle
              label="Mentions"
              checked={preferences.push.mentions}
              onChange={checked => updatePreference("push", "mentions", checked)}
            />
            <Toggle
              label="Comments"
              checked={preferences.push.comments}
              onChange={checked => updatePreference("push", "comments", checked)}
            />
            <Toggle
              label="Likes and reactions"
              checked={preferences.push.likes}
              onChange={checked => updatePreference("push", "likes", checked)}
            />
          </div>
        </section>

        <section>
          <h3 className="text-lg font-medium mb-4 flex items-center gap-2">
            <IcPhone className="h-5 w-5" />
            SMS Notifications
          </h3>
          <div className="space-y-3 pl-7">
            <Toggle
              label="Security alerts"
              checked={preferences.sms.security}
              onChange={checked => updatePreference("sms", "security", checked)}
              validationState="warning"
              validationMessage="Standard messaging rates may apply"
              helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
            />
            <Toggle
              label="Appointment reminders"
              checked={preferences.sms.reminders}
              onChange={checked => updatePreference("sms", "reminders", checked)}
            />
          </div>
        </section>
      </div>

      <div className="mt-8 pt-6 border-t">
        <Button className="w-full">Save Preferences</Button>
      </div>
    </div>
  );
};
```

### 4. Privacy Settings

```tsx
const PrivacySettings = () => {
  const [privacy, setPrivacy] = useState({
    profileVisibility: "public",
    showEmail: false,
    showPhone: false,
    allowMessages: true,
    dataTracking: false,
    analyticsOptOut: true,
  });

  const updatePrivacySetting = (key, value) => {
    setPrivacy(prev => ({ ...prev, [key]: value }));
  };

  return (
    <div className="max-w-2xl mx-auto p-6">
      <h2 className="text-2xl font-bold mb-2">Privacy Settings</h2>
      <p className="text-color-neutral-grey-70 mb-8">
        Control how your information is shared and used
      </p>

      <div className="space-y-8">
        <section>
          <h3 className="text-lg font-semibold mb-4">Profile Visibility</h3>
          <div className="space-y-4">
            <Toggle
              label="Show email address"
              checked={privacy.showEmail}
              onChange={checked => updatePrivacySetting("showEmail", checked)}
              validationState="warning"
              validationMessage="Your email will be visible to other users"
              helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
            />
            <Toggle
              label="Show phone number"
              checked={privacy.showPhone}
              onChange={checked => updatePrivacySetting("showPhone", checked)}
              validationState="error"
              validationMessage="Not recommended for privacy protection"
              helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
            />
            <Toggle
              label="Allow direct messages"
              checked={privacy.allowMessages}
              onChange={checked => updatePrivacySetting("allowMessages", checked)}
              validationMessage="Other users can send you private messages"
            />
          </div>
        </section>

        <section>
          <h3 className="text-lg font-semibold mb-4">Data & Analytics</h3>
          <div className="space-y-4">
            <Toggle
              label="Disable usage tracking"
              checked={privacy.analyticsOptOut}
              onChange={checked => updatePrivacySetting("analyticsOptOut", checked)}
              validationState="success"
              validationMessage="We won't track your usage patterns"
              helperIcon={<IcSuccess className="h-gd-16 w-gd-16" />}
              size="lg"
            />
            <Toggle
              label="Opt out of data collection"
              checked={privacy.dataTracking}
              onChange={checked => updatePrivacySetting("dataTracking", checked)}
              validationMessage="Limit data collection for service improvement"
            />
          </div>
        </section>
      </div>
    </div>
  );
};
```

### 5. Admin Control Panel

```tsx
const AdminControlPanel = () => {
  const [systemSettings, setSystemSettings] = useState({
    maintenanceMode: false,
    userRegistration: true,
    apiAccess: true,
    debugMode: false,
    backupEnabled: true,
    auditLogging: true,
  });

  const updateSystemSetting = (key, value) => {
    setSystemSettings(prev => ({ ...prev, [key]: value }));
  };

  const criticalSettings = ["maintenanceMode", "apiAccess"];

  return (
    <div className="max-w-3xl mx-auto p-6">
      <div className="flex items-center gap-3 mb-8">
        <IcSettings className="h-8 w-8" />
        <h1 className="text-3xl font-bold">System Administration</h1>
      </div>

      <div className="grid gap-8 md:grid-cols-2">
        <section className="space-y-6">
          <h2 className="text-xl font-semibold">System Controls</h2>

          <div className="space-y-4">
            <div className="p-4 border border-color-feedback-error-50 rounded-lg bg-color-feedback-error-20">
              <Toggle
                label="Maintenance mode"
                checked={systemSettings.maintenanceMode}
                onChange={checked => updateSystemSetting("maintenanceMode", checked)}
                validationState="error"
                validationMessage="This will disable the site for all users"
                helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
                size="lg"
              />
            </div>

            <Toggle
              label="User registration"
              checked={systemSettings.userRegistration}
              onChange={checked => updateSystemSetting("userRegistration", checked)}
              validationMessage="Allow new users to create accounts"
            />

            <div className="p-4 border border-color-feedback-warning-50 rounded-lg bg-color-feedback-warning-20">
              <Toggle
                label="API access"
                checked={systemSettings.apiAccess}
                onChange={checked => updateSystemSetting("apiAccess", checked)}
                validationState="warning"
                validationMessage="Disabling will affect all integrations"
                helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
                size="lg"
              />
            </div>

            <Toggle
              label="Debug mode"
              checked={systemSettings.debugMode}
              onChange={checked => updateSystemSetting("debugMode", checked)}
              validationState="error"
              validationMessage="Only enable for troubleshooting"
              helperIcon={<IcWarning className="h-gd-16 w-gd-16" />}
            />
          </div>
        </section>

        <section className="space-y-6">
          <h2 className="text-xl font-semibold">Security & Monitoring</h2>

          <div className="space-y-4">
            <Toggle
              label="Automatic backups"
              checked={systemSettings.backupEnabled}
              onChange={checked => updateSystemSetting("backupEnabled", checked)}
              validationState="success"
              validationMessage="Daily backups at 2:00 AM UTC"
              helperIcon={<IcSuccess className="h-gd-16 w-gd-16" />}
              size="lg"
            />

            <Toggle
              label="Audit logging"
              checked={systemSettings.auditLogging}
              onChange={checked => updateSystemSetting("auditLogging", checked)}
              validationState="success"
              validationMessage="Track all administrative actions"
              helperIcon={<IcSuccess className="h-gd-16 w-gd-16" />}
            />
          </div>

          <div className="p-4 bg-color-neutral-grey-20 rounded-lg">
            <h3 className="font-medium mb-2">System Status</h3>
            <div className="space-y-2 text-sm">
              <div className="flex justify-between">
                <span>Uptime:</span>
                <span className="font-mono">23d 14h 32m</span>
              </div>
              <div className="flex justify-between">
                <span>Active users:</span>
                <span className="font-mono">1,247</span>
              </div>
              <div className="flex justify-between">
                <span>API calls (24h):</span>
                <span className="font-mono">45,621</span>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
  );
};
```

## Accessibility Features

The Toggle component includes comprehensive accessibility support following WAI-ARIA guidelines:

### Keyboard Navigation

- **Tab**: Navigate to the toggle control
- **Space/Enter**: Toggle the switch state
- **Escape**: Move focus away (when applicable)

### Screen Reader Support

- Proper `role="switch"` semantics
- `aria-checked` state management
- `aria-labelledby` for associated labels
- `aria-describedby` for validation messages
- `aria-disabled` for disabled states

### Visual Accessibility

- High contrast focus indicators
- Color-blind friendly state indicators
- Minimum touch target size (44px for large variant)
- Clear visual state differences

```tsx
// Accessibility example
<Toggle
  id="accessibility-example"
  label="High contrast mode"
  aria-describedby="contrast-help"
  onChange={handleToggle}
  size="lg"
/>
<div id="contrast-help" className="text-sm text-color-neutral-grey-70">
  Increases contrast for better visibility
</div>
```

## Genesis Design System Integration

### Design Tokens

The Toggle component leverages Genesis design tokens for consistent theming:

```tsx
// CSS custom properties used internally
const toggleTokens = {
  // Colors
  trackDefault: "var(--gd-neutral-grey-80)",
  trackChecked: "var(--gd-primary-50)",
  knobDefault: "var(--gd-neutral-grey-80)",
  knobChecked: "var(--gd-neutral-white)",

  // Focus states
  focusRing: "var(--gd-primary-60)",

  // Typography
  labelColor: "var(--gd-text-default)",
  helperColor: "var(--gd-text-subdued-1)",

  // Spacing
  gapSmall: "var(--gd-spacing-8)",
  gapMedium: "var(--gd-spacing-16)",
};
```

### Component Integration

```tsx
// Seamless integration with other Genesis components
const IntegratedExample = () => (
  <Card className="p-6">
    <CardHeader>
      <h3 className="text-en-desktop-heading-xl">Notification Settings</h3>
    </CardHeader>
    <CardContent className="space-y-4">
      <Toggle
        label="Email notifications"
        defaultChecked={true}
        icon={<IcMail className="h-gd-16 w-gd-16" />}
      />
      <Toggle
        label="Push notifications"
        defaultChecked={false}
        icon={<IcBell className="h-gd-16 w-gd-16" />}
      />
    </CardContent>
    <CardFooter>
      <Button className="w-full">Save Settings</Button>
    </CardFooter>
  </Card>
);
```

## Best Practices

### Label and Helper Text

```tsx
// ✅ Good: Clear, descriptive labels and helpful messaging
<Toggle
  label="Two-factor authentication"
  validationState="success"
  validationMessage="Recommended for enhanced account security"
  helperIcon={<IcSuccess />}
/>

// ❌ Avoid: Vague labels without context
<Toggle label="Setting 1" />
```

### State Management

```tsx
// ✅ Good: Controlled component with proper state management
const [notifications, setNotifications] = useState(false);

<Toggle
  label="Email notifications"
  checked={notifications}
  onChange={setNotifications}
/>

// ✅ Good: Uncontrolled with default value
<Toggle
  label="Auto-save"
  defaultChecked={true}
  onChange={(checked) => console.log('Auto-save:', checked)}
/>
```

### Responsive Design

```tsx
// ✅ Good: Responsive toggle sizing
const ResponsiveToggle = () => {
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768);

  return (
    <Toggle
      label="Mobile notifications"
      size={isMobile ? "sm" : "md"}
      labelPosition={isMobile ? "right" : "left"}
    />
  );
};
```

### Performance Optimization

```tsx
// ✅ Good: Memoized toggle for better performance
const OptimizedToggle = memo(({ label, onChange, ...props }) => {
  const handleChange = useCallback(
    checked => {
      onChange?.(checked);
    },
    [onChange]
  );

  return <Toggle label={label} onChange={handleChange} {...props} />;
});
```

## Common Pitfalls & Troubleshooting

### Missing Label Accessibility

```tsx
// ❌ Problem: Toggle without proper labeling
<Toggle labelPosition="none" />

// ✅ Solution: Always provide accessible labeling
<Toggle
  labelPosition="none"
  aria-label="Enable dark mode"
  id="dark-mode-toggle"
/>
```

### Inconsistent State Management

```tsx
// ❌ Problem: Mixing controlled and uncontrolled patterns
<Toggle
  checked={isChecked}
  defaultChecked={true}  // This will be ignored
  onChange={setIsChecked}
/>

// ✅ Solution: Choose controlled OR uncontrolled
<Toggle
  checked={isChecked}
  onChange={setIsChecked}
/>
```

### Poor Validation UX

```tsx
// ❌ Problem: Confusing validation state
<Toggle
  label="Enable feature"
  validationState="error"
  validationMessage="Feature enabled successfully"  // Contradictory
/>

// ✅ Solution: Consistent validation messaging
<Toggle
  label="Enable beta features"
  validationState="warning"
  validationMessage="Beta features may be unstable"
  helperIcon={<IcWarning />}
/>
```

## Migration Guide

### From Basic HTML Checkbox

```tsx
// Legacy HTML checkbox
<label>
  <input type="checkbox" onChange={handleChange} />
  Enable notifications
</label>

// Migrate to Genesis Toggle
<Toggle
  label="Enable notifications"
  onChange={handleChange}
/>
```

### From Other Toggle Libraries

```tsx
// React Switch example
<Switch
  checked={enabled}
  onChange={setEnabled}
  onColor="#007bff"
  offColor="#ccc"
/>

// Genesis Toggle equivalent
<Toggle
  checked={enabled}
  onChange={setEnabled}
  size="md"
/>
```

### TypeScript Integration

```tsx
interface ToggleOption {
  id: string;
  label: string;
  description?: string;
  defaultValue: boolean;
  disabled?: boolean;
}

const TypedToggleGroup: React.FC<{ options: ToggleOption[] }> = ({ options }) => {
  const [values, setValues] = useState<Record<string, boolean>>(
    options.reduce(
      (acc, option) => ({
        ...acc,
        [option.id]: option.defaultValue,
      }),
      {}
    )
  );

  const handleToggle = (id: string, checked: boolean) => {
    setValues(prev => ({ ...prev, [id]: checked }));
  };

  return (
    <div className="space-y-4">
      {options.map(option => (
        <Toggle
          key={option.id}
          id={option.id}
          label={option.label}
          checked={values[option.id]}
          onChange={checked => handleToggle(option.id, checked)}
          disabled={option.disabled}
          validationMessage={option.description}
        />
      ))}
    </div>
  );
};
```

## Conclusion

The Genesis Toggle component provides a robust, accessible solution for binary input controls across various application contexts. Its comprehensive API supports multiple sizes, validation states, and label configurations while maintaining consistent design system integration. The component's built-in accessibility features and thoughtful state management make it suitable for everything from simple settings panels to complex administrative interfaces.
