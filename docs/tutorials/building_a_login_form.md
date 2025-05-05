# Tutorial: Building a Simple Login Form

This tutorial demonstrates how to create a basic login form using Devity, including input fields, a submit button, data binding, basic validation (via rules/expressions), and calling an API action.

## Prerequisites

*   Completion of the [Getting Started Guide](../getting-started/flutter_sdk.md).
*   Access to the Devity Console.

## Steps

1.  **Create a New Spec:**
    *   *(Instructions on creating a new Spec in the Console)*
2.  **Design the Layout:**
    *   Add a `Column` Renderer.
    *   Add two `TextField` Widgets (for email and password).
    *   Add a `Button` Widget (for submit).
    *   *(Console screenshots/GIFs would be helpful here)*
3.  **Configure Widgets:**
    *   Set `id`s for TextFields (e.g., `emailInput`, `passwordInput`) and Button (`submitButton`).
    *   Set placeholder text, keyboard types for TextFields.
    *   Set initial text for the Button (e.g., "Login").
4.  **Implement Basic Validation/Button Enable:**
    *   Define a Rule (`rule_enable_login`) that triggers on changes to `emailInput` or `passwordInput` values.
    *   Set the Rule's condition using an [Expression](../core-concepts/expressions.md) to check if both fields are not empty (e.g., `!isEmpty({{widget.emailInput.value}}) && !isEmpty({{widget.passwordInput.value}})`).
    *   Define an Action (`action_enable_login`) of type `UpdateWidgetState` targeting `submitButton` to set its `enabled` attribute to `true`.
    *   Define another Action/Rule (`action_disable_login`) to set `enabled` to `false` if the condition is not met.
    *   Link the rule to the action(s).
    *   Set the initial state of the `submitButton` to `enabled: false`.
5.  **Define the Login API Action:**
    *   Create an Action (`action_call_login_api`) of type `ApiCall`.
    *   Configure its attributes:
        *   `url`: Your login API endpoint.
        *   `method`: `POST`.
        *   `body`: Bind to the widget values (e.g., `{ "email": "{{widget.emailInput.value}}", "password": "{{widget.passwordInput.value}}" }`).
6.  **Handle API Response Actions:**
    *   Define Actions for success (`action_navigate_home`) and failure (`action_show_login_error`).
    *   Use the `onSuccessActionIds` and `onFailureActionIds` attributes of the `ApiCall` action (`action_call_login_api`) to trigger these.
7.  **Link Button Tap to Actions:**
    *   Set the `onClickActionIds` attribute of the `submitButton` to `["action_call_login_api"]`.
8.  **Test the Spec:**
    *   Use the Console preview or Debug mode with the SDK.
    *   Load the Spec in your Flutter app using the `DevityScreen` widget.

## Conclusion

*(Summary of what was achieved)*

## Full Spec JSON (Example)

```json
// (Provide a sample JSON structure for the completed tutorial)
{
  "specId": "login_tutorial",
  // ... rest of the spec
}
``` 