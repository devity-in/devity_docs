# Core Concepts: Expressions

Beyond simple [Data Binding](./data_binding.md), Devity Specs often require embedded logic to compute values, make decisions, or format data dynamically. **Expressions** provide a way to define this logic directly within the Spec JSON.

## What are Expressions?

Expressions are small, evaluate-able snippets of code or logic defined using a specific syntax understood by the Devity SDK. They allow you to perform operations on data (both static and dynamic) available within the Spec's context.

**Purpose of Expressions:**

*   **Conditional Logic:** Determine whether a condition is true or false (e.g., for Rules, enabling/disabling widgets).
*   **Computed Values:** Calculate new values based on existing data (e.g., calculating a total price, formatting a date).
*   **Data Transformation:** Modify or format data before displaying it (e.g., converting a status code to a user-friendly string, converting units).
*   **Dynamic Styling:** (Potentially) Compute style values based on data.

## Expression Syntax

*(Note: The exact syntax needs to be finalized. It could be based on common expression languages like JEXL, CEL, or a custom DSL. The examples below use a hypothetical syntax.)*

Expressions typically involve:

*   **Operands:** Values being operated on. These can be:
    *   Literals (Strings, Numbers, Booleans: `'Hello'`, `123`, `true`).
    *   References to dynamic data via the [Data Binding](./data_binding.md) syntax (e.g., `{{widget.quantity.value}}`, `{{api.product.response.body.price}}`).
*   **Operators:** Symbols performing operations:
    *   Arithmetic: `+`, `-`, `*`, `/`, `%`
    *   Comparison: `==`, `!=`, `<`, `<=`, `>`, `>=`
    *   Logical: `&&` (AND), `||` (OR), `!` (NOT)
    *   (Potentially others like ternary `?:`, string concatenation, etc.)
*   **Functions:** Predefined functions for common tasks (e.g., `isEmpty()`, `length()`, `toLowerCase()`, `formatDate()`, `contains()`).

**Examples:**

```json
// Condition for a Rule: Enable button if both fields are non-empty
{
  "condition": "!isEmpty({{widget.email.value}}) && !isEmpty({{widget.password.value}})"
}

// Computed text value: Display total price
{
  "widgetType": "Text",
  "attributes": {
    "text": "Total: ${{ formatCurrency({{api.cart.response.body.totalAmount}}, 'USD') }}"
  }
}

// Conditional visibility (hypothetical 'visible' attribute):
// Show admin section only if user role is 'admin'
{
  "rendererType": "Column",
  "attributes": {
    "visible": "{{state.globalData.userRole}} == 'admin'"
  },
  "children": [ ... ]
}

// Data transformation: Show 'Complete' or 'Pending' based on status code
{
  "widgetType": "Text",
  "attributes": {
    "text": "{{ {{api.order.response.body.statusCode}} == 2 ? 'Complete' : 'Pending' }}"
  }
}
```

## Where are Expressions Used?

Expressions are commonly used in:

*   **Rule Conditions:** Determining if a rule should trigger its actions.
*   **Widget Attributes:** Calculating attribute values dynamically (e.g., text content, visibility, enabled state).
*   **Action Attributes:** Providing dynamic parameters to actions.
*   **Data Binding:** Complex bindings might involve expression evaluation.

## Evaluation

The Devity SDK includes an expression evaluation engine. When it encounters an expression:

1.  It parses the expression string.
2.  It resolves any embedded data bindings to get current values.
3.  It performs the specified operations and function calls.
4.  It returns the resulting value (e.g., Boolean for conditions, String/Number/etc. for computed values).

Similar to data binding, the SDK typically re-evaluates expressions when their underlying data dependencies change, ensuring the UI reflects the current state.

The specific syntax, supported operators, and available functions will be formally defined in the [Spec Schema](../reference/spec_schema.md). 