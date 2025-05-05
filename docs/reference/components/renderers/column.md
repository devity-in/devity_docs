# Renderer: Column

Arranges child components vertically.

## `rendererType`

`"Column"`

## Attributes

*(List specific attributes for Column, e.g., `mainAxisAlignment`, `crossAxisAlignment`, `spacing`)*

*   **`attributeName`**: (Type) Description.

## Style Properties

*(List common style properties applicable, e.g., `padding`, `backgroundColor`)*

## Children

Accepts an array of [Renderer](../index.md) or [Widget](../../widgets/index.md) objects.

## Example

```json
{
  "id": "my_column",
  "type": "Renderer",
  "rendererType": "Column",
  "attributes": {
    // ... column specific attributes
  },
  "style": {
    "padding": {"all": 16}
  },
  "children": [
    { "widgetType": "Text", "attributes": { "text": "Item 1" } },
    { "widgetType": "Text", "attributes": { "text": "Item 2" } }
  ]
}
``` 