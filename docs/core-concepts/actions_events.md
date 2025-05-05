# Core Concepts: Actions and Events

Devity Specs aren't just static UI descriptions; they define dynamic and interactive experiences. **Actions** are the mechanism for handling events and executing logic within a server-driven workflow.

## What are Actions?

Actions represent specific operations or tasks that can be performed in response to an event. Think of them as predefined functions that the Devity SDK knows how to execute. Examples include navigating to another screen, calling a backend API, showing an alert message, or updating the state of a widget.

In a Devity Spec, Actions are typically defined:

1.  **Reusably:** In the top-level `actions` map of the Spec, allowing them to be referenced by ID from multiple places.
2.  **Inline:** (Potentially) Directly within an event hook property of a widget (though reusable actions are often preferred for clarity).

Each Action has:

*   **`actionType`:** A string identifier specifying the kind of operation (e.g., `Navigate`, `ApiCall`, `ShowAlert`, `UpdateWidgetState`).
*   **`attributes`:** An object containing properties specific to that `actionType` (e.g., the `targetScreenId` for `Navigate`, the `url` and `method` for `ApiCall`).

## Events: Triggering Actions

Actions are triggered by **Events**. Common event sources include:

*   **User Interactions:** Tapping a `Button`, submitting a `TextField`, changing the value of a `Slider`.
    *   Widgets expose specific attribute hooks for these events (e.g., `onClickActionIds`, `onSubmitActionIds`, `onValueChangedActionIds`). These attributes usually contain an array of Action IDs to be executed.
*   **Screen Lifecycle:** Events that occur when a screen is loaded or potentially dismissed.
    *   Screen objects have hooks like `onLoadActions`.
*   **Rules:** Actions can be triggered by [Rules](./rules.md) when certain conditions are met based on widget states or data changes.
*   **API Responses:** An `ApiCall` action might trigger subsequent actions based on the success or failure of the network request.

## Event Handling Flow

When an event occurs (e.g., a user taps a Button defined with `onClickActionIds: ["action_validate", "action_submit"]`):

1.  **Trigger:** The SDK detects the event (button tap).
2.  **Identify Actions:** It retrieves the list of Action IDs associated with that event (`["action_validate", "action_submit"]`).
3.  **Lookup Actions:** It finds the full definition of each Action from the Spec's top-level `actions` map.
4.  **Execute Sequentially:** The SDK executes the identified Actions *in the order they are listed* in the array.
    *   It executes `action_validate`.
    *   If `action_validate` completes successfully (and doesn't halt execution), it then executes `action_submit`.
5.  **Handle Results:** Actions can potentially update data, change widget states, or navigate, leading to UI updates or further events.

This sequential execution allows for creating chains of logic (e.g., validate input, then call API, then navigate on success).

## Common Action Types

The specific `actionType` values available are defined in the [Spec Schema](../reference/spec_schema.md). Common examples include:

*   `Navigate`: Changes the currently displayed screen.
*   `ApiCall`: Makes a network request to a specified backend endpoint.
*   `ShowAlert`: Displays a native alert dialog or toast message.
*   `UpdateWidgetState`: Modifies the attributes or state of another widget (e.g., enabling/disabling a button, changing text).
*   `SetData`: Updates data stored in the spec's state (global, screen, or widget data).
*   `ValidateInput`: Performs validation checks on input widgets.
*   *(And potentially others like `ShowLoading`, `DismissScreen`, etc.)*

## Custom Actions

Similar to Custom Widgets, developers can create custom native logic within their Flutter app and register it as a **Custom Action** with the Devity SDK. This allows triggering platform-specific code or complex business logic directly from the server-driven Spec.

See the [Custom Actions](../advanced/custom_actions.md) guide for details.

Refer to the [Component Reference](../reference/components/actions/) for detailed documentation on each available standard Action type and its specific attributes. 