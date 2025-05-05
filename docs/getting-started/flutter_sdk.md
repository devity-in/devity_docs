# Getting Started: Flutter SDK

This guide walks you through integrating the Devity Flutter SDK into your existing Flutter application to render server-driven UI.

## 1. Prerequisites

*   A working Flutter development environment (Flutter SDK, Dart SDK).
*   An existing Flutter project.
*   Access to a Devity instance (Console & Backend) and a published Spec.
*   Your Devity API Key and the `specId` of the Spec you want to load.

## 2. Installation

Add the `devity_flutter_sdk` package to your Flutter project's dependencies.

Open your `pubspec.yaml` file and add the following under `dependencies`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  # ... other dependencies
  devity_flutter_sdk: ^1.0.0 # Replace with the latest version
```

Then, run `flutter pub get` in your terminal from your project directory:

```bash
flutter pub get
```

## 3. Initialization

Initialize the Devity SDK early in your application lifecycle, typically in your `main.dart` file before `runApp`.

```dart
import 'package:flutter/material.dart';
import 'package:devity_flutter_sdk/devity_flutter_sdk.dart'; // Import the SDK

void main() async {
  // Ensure Flutter bindings are initialized
  WidgetsFlutterBinding.ensureInitialized();

  // Initialize Devity SDK
  await DevitySDK.initialize(
    apiKey: 'YOUR_API_KEY', // Replace with your actual API Key
    // Optional: Specify backend URL for debug mode or self-hosting
    // backendUrl: 'https://your-devity-backend.com',
    // Optional: Set initial global data
    // initialGlobalData: {'userId': '12345'},
  );

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // ... your app code
}
```

*   **`apiKey` (Required):** Your unique API key obtained from the Devity Console/Backend.
*   **`backendUrl` (Optional):** Use this if you are self-hosting Devity or need to point the SDK to a specific backend instance (e.g., for debugging directly from the backend instead of CDN).
*   **`initialGlobalData` (Optional):** Provide initial data that might be needed globally within your specs.

## 4. Rendering a Spec

Devity provides a `DevityScreen` widget that handles fetching, parsing, and rendering a specified Spec.

Use this widget wherever you want to display a server-driven UI flow in your Flutter application (e.g., as a route in your navigation).

```dart
import 'package:flutter/material.dart';
import 'package:devity_flutter_sdk/devity_flutter_sdk.dart';

class MySDUIScreen extends StatelessWidget {
  final String specId;

  const MySDUIScreen({Key? key, required this.specId}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // AppBar can be native or part of the Spec itself
      appBar: AppBar(
        title: Text('Server-Driven Screen'),
      ),
      body: DevityScreen(
        specId: specId, // The ID of the spec to load
        // Optional: Provide loading and error widgets
        loadingBuilder: (context) => Center(child: CircularProgressIndicator()),
        errorBuilder: (context, error, stackTrace) => Center(
          child: Text('Failed to load UI: $error'),
        ),
        // Optional: Inject data specific to this screen instance
        // screenData: {'productId': 'prod_abc'},
      ),
    );
  }
}

// Example Usage (e.g., in Navigator)
// Navigator.push(
//   context,
//   MaterialPageRoute(builder: (context) => MySDUIScreen(specId: 'onboarding_v2')),
// );
```

*   **`specId` (Required):** The unique ID of the Devity Spec you want to render.
*   **`loadingBuilder` (Optional):** A widget builder function to display while the Spec is being fetched and parsed.
*   **`errorBuilder` (Optional):** A widget builder function to display if fetching or rendering the Spec fails.
*   **`screenData` (Optional):** Data specifically passed into this instance of the rendered spec.

## 5. Next Steps

With these steps, you should be able to display a basic UI defined in your Devity Console within your Flutter app.

Explore the following sections to learn more:

*   [Core Concepts](../core-concepts/): Understand the building blocks like Renderers, Widgets, Actions, etc.
*   [Tutorials](../tutorials/): Follow step-by-step examples.
*   [Advanced Guides](../advanced/): Learn about custom components and more. 