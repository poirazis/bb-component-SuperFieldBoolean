# Super Field - Boolean

A flexible boolean input component for Budibase applications supporting both checkbox and switch interfaces with customizable labels and validation.

## 🚀 Features

### Boolean Input Types

- **Checkbox Interface**: Traditional checkbox for boolean selection
- **Switch Interface**: Modern toggle switch for on/off states
- **Field Binding**: Dedicated boolean field type with type safety
- **Default Values**: Pre-set true/false states

### Display & Formatting

- **Custom Labels**: Configurable text labels for true/false states
- **Value Templates**: Custom formatting for display text
- **Help Text**: Contextual guidance for boolean choices
- **Icons**: Visual indicators for boolean states

### Validation & Logic

- **Boolean Validation**: Required field validation
- **Conditional Logic**: Dynamic behavior based on boolean state
- **Event Handling**: On change events with boolean context
- **State Management**: Clean true/false value handling

### User Experience

- **Intuitive Controls**: Familiar checkbox or modern switch interfaces
- **Accessibility**: Full keyboard navigation and screen reader support
- **Visual Feedback**: Clear visual states for enabled/disabled/readonly
- **Responsive Design**: Adapts to different screen sizes

### Styling & Layout

- **Flexible Positioning**: Label placement options (above, left, hidden)
- **Field Modes**: Form input or inline editing styles
- **Size Configuration**: Adjustable width and span settings
- **Theme Integration**: Consistent with Budibase design system

## 📝 Usage Instructions

### Basic Setup

1. Add the Super Field - Boolean component to your form
2. Choose between checkbox or switch control type
3. Bind to a boolean data field
4. Configure label and help text

### Configuration Options

- **Control Type**: Select checkbox for traditional, switch for modern UI
- **Default Value**: Set initial true/false state
- **Validation**: Make field required if needed
- **Events**: Attach actions to state changes

### Common Use Cases

- **Settings Panels**: User preferences and configuration options
- **Terms Acceptance**: Agreement checkboxes for forms
- **Feature Toggles**: Enable/disable application features
- **Survey Questions**: Yes/no or true/false responses
- **Status Indicators**: Active/inactive or enabled/disabled states

## 🔧 Configuration Options

| Setting         | Type     | Description                   |
| --------------- | -------- | ----------------------------- |
| Field           | Boolean  | Boolean field binding         |
| Label           | String   | Display label text            |
| Default Value   | Boolean  | Pre-set true/false value      |
| Help Text       | String   | Help/instruction text         |
| Formatted Value | Template | Custom display formatting     |
| Validation      | Rules    | Boolean validation (required) |
| Control Type    | Select   | Checkbox or Switch interface  |
| Disabled        | Boolean  | Disable interaction           |
| Read Only       | Boolean  | Read-only mode                |
| Icon            | Icon     | Visual indicator icon         |
| Field Mode      | Select   | Form or inline input style    |
| Label Position  | Select   | Label placement               |
| Size            | Number   | Component width span          |

## 📋 Events

### On Change

Triggered when the boolean value changes.

**Context:**

- `value`: The current boolean value (true/false)
- `field`: The bound field information

## 🎨 Styling

The component integrates with Budibase's styling system:

- **Size Variants**: Compact and standard sizes
- **Color Theming**: Consistent with application theme
- **Custom CSS**: Advanced styling customization
- **Responsive**: Mobile-friendly design

## 🔍 Best Practices

- Use switches for settings that feel like on/off toggles
- Use checkboxes for terms acceptance or multiple selections
- Provide clear labels that indicate the true/false meaning
- Consider accessibility with proper labeling
- Use help text for complex boolean decisions
- Test both keyboard and mouse interaction
