# Advanced: Custom Widgets

While Devity provides a library of standard [Widgets](../core-concepts/widgets.md), you will often need UI elements specific to your application's design language or functionality. Devity's extensibility allows you to create custom native Flutter widgets and render them based on your server-driven Specs.

## Why Use Custom Widgets?

*   **Unique UI/UX:** Implement components that are not part of the standard library (e.g., custom charts, branded cards, complex interactive elements).
*   **Platform Integration:** Create widgets that deeply integrate with platform-specific features or native SDKs.
*   **Performance Optimization:** Build highly optimized widgets for specific use cases where standard compositions might be insufficient.
*   **Encapsulation:** Encapsulate complex UI logic and state within a reusable Flutter widget, controlled via attributes from the Spec.

## Process Overview

1.  **Create:** Build your custom widget in your Flutter application codebase like any other Flutter widget.
2.  **Define Interface:** Determine which attributes of your widget need to be configurable from the server Spec.
3.  **Build Builder:** Create a builder function that takes the Spec definition (attributes, context) and returns an instance of your custom Flutter widget.
4.  **Register:** Register your builder function with the Devity SDK, associating it with a unique `widgetType` string.
5.  **Use in Spec:** Use the registered `widgetType` within your Specs in the Devity Console, configuring its attributes as needed.

## 1. Creating the Flutter Widget

Build your custom widget using standard Flutter practices. It can be stateful or stateless.

```dart
// Example: A simple custom widget
import 'package:flutter/material.dart';

class MyCustomRatingWidget extends StatelessWidget {
  final int maxRating;
  final double currentRating;
  final Color starColor;

  const MyCustomRatingWidget({
    Key? key,
    this.maxRating = 5,
    required this.currentRating,
    this.starColor = Colors.orange,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Your widget build logic here (e.g., displaying stars)
    return Row(
      mainAxisSize: MainAxisSize.min,
      children: List.generate(maxRating, (index) {
        return Icon(
          index < currentRating ? Icons.star : Icons.star_border,
          color: starColor,
        );
      }),
    );
  }
}
```

## 2. Defining the Builder Function

The Devity SDK needs a way to create an instance of your widget when it encounters the corresponding `widgetType` in the Spec. You provide a builder function for this.

*(Note: The exact signature of the builder function will depend on the final SDK API design. It will likely receive the widget's definition from the Spec and potentially other context.)*

```dart
// Hypothetical Builder Function Signature
// typedef CustomWidgetBuilder = Widget Function(BuildContext context, Map<String, dynamic> attributes, Map<String, dynamic>? style);

Widget myCustomRatingWidgetBuilder(BuildContext context, Map<String, dynamic> attributes, Map<String, dynamic>? style) {
  // Extract attributes from the spec definition, providing defaults
  final int maxRating = attributes['maxRating'] as int? ?? 5;
  // IMPORTANT: Handle potential data types and nulls carefully!
  final double currentRating = (attributes['currentRating'] as num?)?.toDouble() ?? 0.0;
  final String colorString = attributes['starColor'] as String? ?? '#FFA500'; // Default orange

  // TODO: Convert colorString to Color object
  final Color starColor = Color(int.parse(colorString.substring(1, 7), radix: 16) + 0xFF000000);

  // TODO: Apply common styling properties from the 'style' map if needed

  return MyCustomRatingWidget(
    maxRating: maxRating,
    currentRating: currentRating,
    starColor: starColor,
  );
}
```

**Key Considerations for Builders:**

*   **Attribute Parsing:** Carefully parse attributes from the map, handle potential type mismatches (data from JSON might not be the exact Dart type needed), and provide sensible defaults.
*   **Error Handling:** Implement robust error handling if required attributes are missing or invalid.
*   **Styling:** Decide how to handle common `style` properties passed from the Spec (padding, margin, etc.). You might wrap your custom widget in a `Container` or use the properties directly if applicable.
*   **Context:** Utilize the `BuildContext` if needed.

## 3. Registering the Widget

Register your builder function with the SDK during initialization, typically in `main.dart`, associating it with the unique `widgetType` string you will use in your Specs.

```dart
// In main.dart, after DevitySDK.initialize

DevitySDK.registerCustomWidget(
  'MyRatingWidget', // The unique widgetType used in the Spec
  myCustomRatingWidgetBuilder, // The builder function
);
```

*(See [SDK API Reference](../reference/flutter_sdk_api.md) for the exact registration method)*

## 4. Using in the Spec

Now, in the Devity Console, you can add a widget and set its `widgetType` to `"MyRatingWidget"`. The attributes you defined (e.g., `maxRating`, `currentRating`, `starColor`) will be available in the Attribute Inspector for configuration.

```json
// Example usage within a Spec's children array
{
  "id": "product_rating",
  "type": "Widget",
  "widgetType": "MyRatingWidget", // Registered custom type
  "attributes": {
    "currentRating": "{{api.productDetails.response.body.averageRating}}", // Dynamic binding
    "maxRating": 5,
    "starColor": "#FFC107" // Amber color
  }
}
```

The SDK will now use your registered `myCustomRatingWidgetBuilder` function to render `MyCustomRatingWidget` whenever it encounters `"widgetType": "MyRatingWidget"` in the JSON Spec. 