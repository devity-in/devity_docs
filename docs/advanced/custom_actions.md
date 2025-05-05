# Advanced: Custom Actions

Devity's standard [Actions](../core-concepts/actions_events.md) cover common operations like navigation, API calls, and basic state updates. However, your application might require specific logic or platform interactions not covered by the built-in actions. Custom Actions allow you to bridge this gap by triggering your own native Dart/Flutter code from a Devity Spec.

## Why Use Custom Actions?

*   **Platform Integration:** Interact with native device features (GPS, camera, Bluetooth, local database like SQLite/Hive) or platform-specific SDKs.
*   **Complex Business Logic:** Execute intricate business logic that is easier to write and maintain in Dart than in Spec expressions or rules.
*   **Third-Party SDKs:** Call methods from other Flutter packages or SDKs integrated into your app.
*   **Reusable Native Code:** Encapsulate frequently used native operations triggered from multiple Specs.

## Process Overview

1.  **Create Handler Function:** Write a Dart function in your Flutter application that performs the desired logic.
2.  **Define Interface:** Determine what parameters (attributes) your custom action needs from the Spec.
3.  **Register Handler:** Register your handler function with the Devity SDK, associating it with a unique `actionType` string.
4.  **Use in Spec:** Use the registered `actionType` when defining Actions in the Devity Console, configuring its attributes as needed.

## 1. Creating the Handler Function

Write an asynchronous Dart function that performs the desired task. This function will receive context and the attributes defined for the action in the Spec.

*(Note: The exact signature of the handler function will depend on the final SDK API design. It will likely receive the action's attributes and potentially other context like the current BuildContext or SDK state accessors.)*

```dart
// Example: A custom action to save data to a local database (e.g., using Hive)

// Hypothetical Handler Function Signature
// typedef CustomActionHandler = Future<void> Function(BuildContext? context, Map<String, dynamic> attributes);

Future<void> saveUserDataLocallyHandler(BuildContext? context, Map<String, dynamic> attributes) async {
  try {
    // Extract attributes passed from the Spec
    final String userId = attributes['userId'] as String;
    final String userDataJson = attributes['userDataJson'] as String; // Assuming data is passed as JSON string

    // --- Your Native Logic Here --- 
    print('Executing custom action: saveUserDataLocally');
    // Example using Hive (assuming Hive box is open)
    // final userBox = Hive.box('user_data');
    // await userBox.put(userId, userDataJson);
    print('Saved data for user $userId locally.');
    // --- End Native Logic --- 

  } catch (e, stackTrace) {
    print('Error executing custom action saveUserDataLocally: $e\n$stackTrace');
    // Handle errors appropriately - maybe throw to let SDK know?
  }
}
```

**Key Considerations for Handlers:**

*   **Asynchronous:** Handlers are often `async` as they might involve I/O (network, disk).
*   **Attribute Parsing:** Safely extract and parse attributes from the map, handling potential `null` values and type errors.
*   **Error Handling:** Implement robust error handling within your function.
*   **Context:** Use the provided `BuildContext` if needed for navigation, showing dialogs (though standard actions might be better for UI changes), or accessing providers.
*   **Accessing SDK State:** The SDK might provide mechanisms within the handler context to read current state or data (e.g., `sdkContext.getWidgetValue('widgetId')`).

## 2. Registering the Handler

Register your handler function with the SDK during initialization, typically in `main.dart`, associating it with the unique `actionType` string you will use in your Specs.

```dart
// In main.dart, after DevitySDK.initialize

DevitySDK.registerCustomAction(
  'saveUserDataLocally', // The unique actionType used in the Spec
  saveUserDataLocallyHandler, // The handler function
);
```

*(See [SDK API Reference](../reference/flutter_sdk_api.md) for the exact registration method)*

## 3. Using in the Spec

Now, in the Devity Console, you can create an Action and set its `actionType` to `"saveUserDataLocally"`. The attributes your handler expects (e.g., `userId`, `userDataJson`) can be configured in the Attribute Inspector, potentially using dynamic [Data Binding](../core-concepts/data_binding.md).

```json
// Example Action definition in the Spec's top-level "actions" map
"action_save_profile": {
  "id": "action_save_profile",
  "type": "Action",
  "actionType": "saveUserDataLocally", // Registered custom type
  "attributes": {
    "userId": "{{state.globalData.userId}}",
    "userDataJson": "{{api.saveProfile.request.body}}" // Example: binding to API request body
  }
}

// Triggering the custom action, perhaps after a successful API call
"action_call_save_api": {
  "id": "action_call_save_api",
  "type": "Action",
  "actionType": "ApiCall",
  "attributes": {
     // ... API call config ...
     "onSuccessActionIds": ["action_save_profile", "action_show_success_toast"]
  }
}
```

When the Devity SDK needs to execute an action with `actionType: "saveUserDataLocally"`, it will invoke your registered `saveUserDataLocallyHandler` function, passing the attributes defined in the Spec. 