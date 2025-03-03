# Devity Flutter SDK Guide

Welcome to the **Devity Flutter SDK Guide**. This document explains how to integrate and use the Devity SDK to dynamically render UI based on server-driven specifications.

## Installation
To install the Devity SDK in your Flutter project, add the following dependency to your `pubspec.yaml`:

```yaml
dependencies:
  devity_sdk: latest_version
```
Then, run:
```sh
flutter pub get
```

## Initialization
Initialize the SDK in your main application file:

```dart
import 'package:devity_sdk/devity_sdk.dart';

void main() {
  DevitySDK.initialize(
    baseUrl: "https://api.devity.com", // Replace with actual API URL
    authToken: "your_auth_token", // Optional authentication token
  );
  runApp(MyApp());
}
```

## Fetching and Rendering a Spec
To render a UI spec, fetch it from the backend and pass it to the `DevityRenderer` widget:

```dart
import 'package:flutter/material.dart';
import 'package:devity_sdk/devity_sdk.dart';

class SpecScreen extends StatefulWidget {
  final String specId;
  const SpecScreen({required this.specId, Key? key}) : super(key: key);

  @override
  _SpecScreenState createState() => _SpecScreenState();
}

class _SpecScreenState extends State<SpecScreen> {
  late Future<DevitySpec> spec;

  @override
  void initState() {
    super.initState();
    spec = DevitySDK.getSpec(widget.specId);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Dynamic UI")),
      body: FutureBuilder<DevitySpec>(
        future: spec,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return Center(child: CircularProgressIndicator());
          } else if (snapshot.hasError) {
            return Center(child: Text("Error loading UI"));
          } else {
            return DevityRenderer(spec: snapshot.data!);
          }
        },
      ),
    );
  }
}
```

## Handling Actions
Devity SDK allows handling predefined actions such as navigation, API calls, and alerts. Define action handlers as follows:

```dart
DevitySDK.setActionHandler((context, action) {
  switch (action.type) {
    case "navigate":
      Navigator.pushNamed(context, action.data["route"]);
      break;
    case "alert":
      showDialog(
        context: context,
        builder: (_) => AlertDialog(
          title: Text(action.data["title"] ?? ""),
          content: Text(action.data["message"] ?? ""),
        ),
      );
      break;
    default:
      print("Unknown action: ${action.type}");
  }
});
```

## Debugging Mode
For development, you can fetch the spec directly from the backend instead of the CDN:

```dart
DevitySDK.enableDebugMode();
```

## Conclusion
With the Devity Flutter SDK, you can build dynamic, server-driven UIs without the need for frequent app releases. For more details, visit the [Devity Docs](https://github.com/your-org/devity_docs).

