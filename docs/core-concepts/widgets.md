# Core Concepts: Widgets

While [Renderers](./renderers_layouts.md) define the layout and structure, **Widgets** are the fundamental building blocks that make up the actual user interface elements that users see and interact with.

## What are Widgets?

Widgets represent concrete UI elements like text labels, buttons, images, input fields, sliders, etc. They are the visual components placed *inside* Renderers.

In a Devity Spec, each Widget is defined by:

1.  **`widgetType`:** A string identifier specifying the kind of widget (e.g., `Text`, `Button`, `Image`, `TextField`).
2.  **`attributes`:** An object containing properties specific to that `widgetType` which control its appearance and content (e.g., the `text` value for a `Text` widget, the `imageUrl` for an `Image` widget, placeholder text for a `TextField`).
3.  **`style`:** Common [styling properties](./styling.md) (like padding, margin, background) applicable to most widgets.
4.  **Interaction Hooks:** Properties to link user interactions (like taps) to specific [Actions](./actions_events.md) (e.g., `onClickActionIds`).

## Role of Widgets

*   **Visual Representation:** Display information (Text, Image) or interactive elements (Button, TextField).
*   **User Interaction:** Capture user input (TextField, Slider, Checkbox) or trigger events (Button taps).
*   **Content:** Hold the actual content seen by the user, configured via attributes.
*   **Data Display:** Can display dynamic data bound via their attributes (see [Data Binding](./data_binding.md)).

## Common Widget Types

Devity aims to provide a rich library of common widgets. The specific types available are defined in the [Spec Schema](../reference/spec_schema.md) under the `widgetType` property. Examples include:

*   `Text`: Displays static or dynamic text.
*   `Button`: An interactive button that can trigger actions.
*   `Image`: Displays images from URLs or assets.
*   `TextField`: Allows users to input text.
*   `Checkbox`: A standard checkbox.
*   `DatePicker`: Allows users to select a date.
*   `Slider`: Allows users to select a value from a range.
*   `Dropdown`: A dropdown selection menu.
*   `ListView`/`RecyclerView`: Efficiently displays lists of data (often using templates).
*   *(And many more...)*

## Custom Widgets

While Devity provides standard widgets, the framework is designed to be extensible. Developers can create their own **custom native widgets** within their Flutter application and register them with the Devity SDK. These custom widgets can then be referenced by a unique `widgetType` within the Spec, allowing server-driven control over proprietary or highly specialized UI components.

See the [Custom Widgets](../advanced/custom_widgets.md) guide for details on implementation.

Refer to the [Component Reference](../reference/components/widgets/) for detailed documentation on each available standard Widget type and its specific attributes. 