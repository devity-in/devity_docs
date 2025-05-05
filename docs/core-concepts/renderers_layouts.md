# Core Concepts: Renderers and Layouts

In Devity, **Renderers** are special components defined in a Spec whose primary purpose is to control the **layout** and arrangement of their child components on the screen. They are the containers that organize Widgets and potentially other nested Renderers.

## Layout Philosophy

Similar to how layout widgets work in frameworks like Flutter (e.g., `Column`, `Row`, `Stack`), Devity Renderers provide common layout patterns. Instead of writing layout code in your app, you define the layout structure declaratively within the Spec JSON.

Any complex screen can be broken down into a hierarchy of nested Renderers and the Widgets they contain.

## Role of Renderers

*   **Structure:** Define how child components are positioned relative to each other (e.g., vertically, horizontally, overlaid).
*   **Organization:** Group related UI elements.
*   **Nesting:** Renderers can contain other Renderers, allowing for complex and flexible layouts.
*   **Styling:** Renderers themselves can often have common [styling properties](./styling.md) applied (like padding, background color, borders).

## Common Renderer Types

The specific types of renderers available are defined in the [Spec Schema](../reference/spec_schema.md) under the `rendererType` property. Common examples mirroring native layout concepts include:

*   **`Column`:** Arranges children vertically.
*   **`Row`:** Arranges children horizontally.
*   **`Stack`:** Overlays children on top of each other.
*   **`Grid`:** Arranges children in a grid format.
*   **`Scrollable`:** Allows its content (typically a single child Renderer like `Column` or `Row`) to scroll if it exceeds the available space.
*   **`Padded`:** Applies padding around a single child component.
*   *(Other types like `Expanded`, `Center`, etc., might also be defined)*

Each `rendererType` will have specific attributes defined in the schema and component reference to control its behavior (e.g., alignment, spacing for `Column`/`Row`).

## Standard Screen Layout

Devity often suggests a standard top-level screen structure using specific Renderers:

1.  **Top Renderer:** (Optional) Sticks to the top of the screen, typically used for headers or banners that should remain visible above the main content.
2.  **Main Renderer:** Contains the primary content of the screen. Often a `Scrollable` renderer wrapping a `Column` or `Row` to handle content that might exceed screen height.
3.  **Bottom Renderer:** (Optional) Sticks to the bottom of the screen, commonly used for action buttons (like Submit, Next) or summary information.

Within these root renderers (especially the Main Renderer), you nest further Renderers and Widgets to build the desired screen layout.

Refer to the [Component Reference](../reference/components/renderers/) for detailed documentation on each available Renderer type and its specific attributes. 