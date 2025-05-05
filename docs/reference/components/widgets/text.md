# Widget: Text

Displays a string of text.

## `widgetType`

`"Text"`

## Attributes

*(List specific attributes for Text, e.g., `text`, `fontSize`, `fontWeight`, `color`, `textAlign`, `maxLines`, etc.)*

*   **`text`**: (String | Binding) The text content to display. Required.
*   **`fontSize`**: (Number | Binding) Size of the font.
*   **`fontWeight`**: (String | Binding) e.g., `"bold"`, `"normal"`.
*   **`color`**: (String | Binding) Text color (e.g., `"#333333"`).

## Style Properties

*(List common style properties applicable, e.g., `padding`, `margin`, `backgroundColor`)*

## Example

```json
{
  "id": "greeting_text",
  "type": "Widget",
  "widgetType": "Text",
  "attributes": {
    "text": "Hello, {{state.globalData.userName}}!",
    "fontSize": 20,
    "fontWeight": "bold"
  },
  "style": {
    "margin": {"bottom": 10}
  }
}
``` 