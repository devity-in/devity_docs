# Core Concepts: Rules

While direct user interactions on a widget can trigger [Actions](./actions_events.md), sometimes you need widgets to react to changes in *other* widgets or data sources. **Rules** are the mechanism in Devity for defining this inter-widget communication and conditional logic.

## What are Rules?

Rules allow you to define a relationship between a **trigger** event (like a data change), a **condition** (an [Expression](./expressions.md) that evaluates to true/false), and a set of **actions** to execute if the condition is met.

**Purpose of Rules:**

*   **Inter-Widget Communication:** Enable one widget to affect another (e.g., entering text in a field enables a button).
*   **Conditional UI Updates:** Change the state or appearance of widgets based on application state or user input elsewhere (e.g., show/hide a section, change text color based on validation).
*   **Complex Validation:** Implement validation logic that depends on multiple inputs.
*   **Automated Actions:** Trigger actions automatically when certain data conditions are met, without direct user interaction on the target.

## Structure of a Rule

A Rule, typically defined in the top-level `rules` map of a Spec, consists of three main parts:

1.  **`trigger`:** Defines *what* causes the rule to be evaluated. This often involves listening to changes in specific data sources:
    *   Widget values (e.g., `widget.emailInput.value` changes).
    *   API response data (e.g., `api.userData.response` is received).
    *   State variables (e.g., `state.cartTotal` changes).
    *(The exact trigger definition syntax will be in the Spec Schema)*.
2.  **`condition`:** An [Expression](./expressions.md) that is evaluated *when the trigger occurs*. The expression must resolve to a boolean (`true` or `false`).
3.  **`actionIds`:** An array of Action IDs (referencing actions defined in the top-level `actions` map) that will be executed *if and only if* the `condition` expression evaluates to `true`.

**Example Scenario: Enabling a Submit Button**

Imagine you want a submit button (`widget.submitButton`) to be enabled only when both an email field (`widget.emailInput`) and a password field (`widget.passwordInput`) are not empty.

A Rule could be defined like this (conceptual):

```json
// In top-level "rules" map
"rule_enable_submit": {
  "id": "rule_enable_submit",
  "type": "Rule",
  "trigger": {
    // Trigger whenever email OR password value changes
    "listenTo": ["widget.emailInput.value", "widget.passwordInput.value"]
  },
  "condition": "!isEmpty({{widget.emailInput.value}}) && !isEmpty({{widget.passwordInput.value}})",
  "actionIds": ["action_enable_submit_button"]
}

// In top-level "actions" map
"action_enable_submit_button": {
  "id": "action_enable_submit_button",
  "type": "Action",
  "actionType": "UpdateWidgetState",
  "attributes": {
    "targetWidgetId": "submitButton",
    "newState": { "enabled": true }
  }
}

// Potentially another rule/action needed to disable the button if the condition becomes false
```

## Evaluation Flow

1.  **Trigger Occurs:** The SDK detects a change specified in a rule's `trigger` (e.g., user types in `emailInput`).
2.  **Evaluate Condition:** The SDK evaluates the `condition` expression associated with that rule using the current data state.
3.  **Execute Actions (if true):** If the condition evaluates to `true`, the SDK looks up and executes the actions listed in `actionIds` sequentially, just like regular event handling.
4.  **Do Nothing (if false):** If the condition evaluates to `false`, no actions associated with the rule are executed.

Rules provide a powerful way to create reactive UIs where different parts respond intelligently to changes in the overall application state, driven entirely by the server-defined Spec.

The detailed structure for defining triggers and conditions will be available in the [Spec Schema](../reference/spec_schema.md). 