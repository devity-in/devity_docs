# Core Concepts: Styling

Devity allows you to control the visual appearance of UI elements defined in your Spec using **Styling Properties**. This ensures that the server-driven UI aligns with your application's design language.

## The `style` Object

Most [Renderer](./renderers_layouts.md) and [Widget](./widgets.md) objects within a Spec can include an optional `style` attribute. This attribute holds an object containing key-value pairs that define common visual properties.

```json
{
  "id": "welcome_card",
  "type": "Renderer",
  "rendererType": "Column",
  "style": {
    "padding": {"top": 16, "bottom": 16, "left": 12, "right": 12},
    "margin": {"bottom": 20},
    "backgroundColor": "#FFFFFF",
    "cornerRadius": 8,
    "border": {
      "width": 1,
      "color": "#E0E0E0"
    }
    // ... other common style properties
  },
  "children": [ ... ]
}
```

## Scope of Styling

*   **Common Properties:** Devity defines a set of standard styling properties (like padding, margin, background color, border, corner radius, potentially width/height constraints, flex properties for Row/Column children, etc.) that are generally applicable across different renderers and widgets.
*   **Static Values:** Typically, values within the `style` object are **static** (defined directly in the Spec JSON) and cannot use dynamic [Data Binding](./data_binding.md) or [Expressions](./expressions.md). This simplifies rendering and ensures consistent styling that isn't constantly re-evaluated based on data changes.
*   **Widget-Specific Styling:** Some highly specific visual attributes might be handled directly within a Widget's main `attributes` object rather than the common `style` object (e.g., `fontSize` or `fontWeight` for a `Text` widget).

## Styling Goals

*   **Consistency:** Provide a standard way to apply common visual treatments.
*   **Flexibility:** Allow customization of spacing, backgrounds, borders, etc.
*   **Simplicity:** Avoid overly complex styling logic within the core SDUI spec. More intricate styling might be handled by custom widgets or potentially a future theme system.

## Available Properties

The exact set of supported styling properties and their expected value formats (e.g., padding objects, color strings, number values) will be formally defined in the [Spec Schema](../reference/spec_schema.md) and detailed in the reference documentation.

Commonly expected properties include:

*   `padding`: Inner spacing (e.g., `{ "all": 8 }` or `{ "horizontal": 16, "vertical": 8 }`).
*   `margin`: Outer spacing.
*   `backgroundColor`: Background color (e.g., `"#FF0000"`, `"rgba(0,0,255,0.5)"`).
*   `cornerRadius`: Radius for rounded corners (e.g., `8` or `{ "topLeft": 10, "bottomRight": 10 }`).
*   `border`: Defines border width, color, style (e.g., `{ "width": 2, "color": "#0000FF" }`).
*   `width`, `height`: Potential fixed or max/min dimensions.
*   `alignment`: How content is aligned within a component (relevant for Stacks, Rows, Columns).
*   *(Potentially gradient backgrounds, shadows, etc.)*

By applying these style properties within the Spec, you can control the look and feel of your server-driven UI without needing to modify client-side code. 