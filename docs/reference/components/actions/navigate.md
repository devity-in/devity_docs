# Action: Navigate

Changes the currently displayed screen within the workflow defined by the Spec.

## `actionType`

`"Navigate"`

## Attributes

*   **`targetScreenId`**: (String | Binding) The `id` of the [Screen](../../../reference/spec_schema.md#2-screen-object) to navigate to. Required.
*   **`transitionType`**: (String, Optional) Specifies the animation used for the transition (e.g., `"slide_left"`, `"fade"`, `"none"`). Defaults may vary by SDK.
*   **`clearHistory`**: (Boolean, Optional) If `true`, clears the navigation history up to this point, preventing the user from navigating back to previous screens in this workflow. Defaults to `false`.
*   **`screenData`**: (Object | Binding, Optional) Data to pass specifically to the target screen instance. Accessible within the target screen via `{{state.screenData...}}`.

## Example

```json
// In top-level "actions" map
"action_goto_details": {
  "id": "action_goto_details",
  "type": "Action",
  "actionType": "Navigate",
  "attributes": {
    "targetScreenId": "screen_product_details",
    "transitionType": "slide_left",
    "screenData": {
      "productId": "{{widget.selected_product.id}}"
    }
  }
}

// Triggered from a button
{
  "widgetType": "Button",
  "attributes": { "text": "View Details" },
  "onClickActionIds": ["action_goto_details"]
}
``` 