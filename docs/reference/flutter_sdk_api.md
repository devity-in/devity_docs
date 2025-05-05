# Flutter SDK API Reference

This document provides API reference documentation for the public classes and methods exposed by the `devity_flutter_sdk` package.

*(Note: This document will be populated with detailed API information generated from the source code comments as the SDK is developed.)*

## 1. Conceptual Structure (Internal)

While the public API might be simple, internally the SDK will likely consist of several modules:

*   **Networking/Fetching:** Handles retrieving Spec JSON from CDN or Backend.
*   **Parsing:** Parses the JSON string into an internal representation (e.g., tree of component models).
*   **Component Registry:** Manages standard and custom Widget/Action builders.
*   **Rendering Engine:** Traverses the internal representation and builds the Flutter widget tree using registered builders.
*   **State Management:** Holds the current state (global data, screen data, API responses, widget values) and manages updates.
*   **Data Binding Resolver:** Evaluates binding expressions against the current state.
*   **Expression Engine:** Parses and evaluates expressions used in conditions and bindings.
*   **Action Executor:** Looks up and executes standard and custom actions, interacting with state and other modules.
*   **Rule Engine:** Listens for state changes (triggers) and evaluates rule conditions.

## 2. Public API

### 2.1 Initialization & Configuration (`DevitySDK`)

Static class for global SDK setup.

*   **`Future<void> initialize({required String apiKey, String? backendUrl, String? cdnUrl, Map<String, dynamic>? initialGlobalData, DevityLogLevel? logLevel})`**
    *   Initializes the SDK. Must be called once before using other SDK features, typically in `main.dart`.
    *   `apiKey` (Required): Your project's API Key.
    *   `backendUrl` (Optional): Override the default backend URL (for self-hosting or debug).
    *   `cdnUrl` (Optional): Override the default CDN base URL.
    *   `initialGlobalData` (Optional): Seed the global data state accessible via bindings like `{{state.globalData...}}`.
    *   `logLevel` (Optional): Configure SDK logging level (e.g., `none`, `error`, `info`, `debug`).

*   **`void registerCustomWidget(String widgetType, CustomWidgetBuilder builder)`**
    *   Registers a builder function for a custom widget type.
    *   `widgetType`: The unique string identifier used in the Spec JSON.
    *   `builder`: The function that takes context, attributes, style and returns the Flutter widget. (See [Custom Widgets Guide](../advanced/custom_widgets.md)).

*   **`void registerCustomAction(String actionType, CustomActionHandler handler)`**
    *   Registers a handler function for a custom action type.
    *   `actionType`: The unique string identifier used in the Spec JSON.
    *   `handler`: The function that executes the custom logic, receiving context and attributes. (See [Custom Actions Guide](../advanced/custom_actions.md)).

*   *(Other potential static methods: e.g., `updateGlobalData`, `getGlobalData`, `setLogLevel`)*

### 2.2 Rendering UI (`DevityScreen` Widget)

The primary way to display Devity content.

*   **`DevityScreen({Key? key, required String specId, int? version, bool? useDraft, WidgetBuilder? loadingBuilder, DevityErrorWidgetBuilder? errorBuilder, Map<String, dynamic>? screenData})`**
    *   A `StatefulWidget` that manages the lifecycle of fetching, parsing, and rendering a Spec.
    *   `specId` (Required): The ID of the spec to load.
    *   `version` (Optional): Load a specific published version number. If omitted, loads the latest published version.
    *   `useDraft` (Optional, default: `false`): If `true`, attempts to load the latest *draft* version directly from the backend (requires API key auth and debug mode enabled potentially). Overrides `version`.
    *   `loadingBuilder` (Optional): Widget displayed during initial spec load.
    *   `errorBuilder` (Optional): Widget displayed if the spec fails to load or parse.
    *   `screenData` (Optional): Initial data passed to the screen instance, accessible via `{{state.screenData...}}`.

### 2.3 Lower-Level APIs (Potentially)

*(Consider if lower-level access is needed, e.g., pre-fetching specs, accessing parsed spec data directly, manually triggering actions. These might be added later if required.)*

*   `Future<Spec?> fetchSpec(String specId, {int? version, bool useDraft = false})`: Manually fetch/cache a spec.
*   `Widget buildSpec(BuildContext context, Spec spec, {Map<String, dynamic>? screenData})`: Manually render a pre-fetched/parsed spec.

## 3. Type Definitions

*(Define key typedefs used in the public API)*

*   **`typedef CustomWidgetBuilder = Widget Function(BuildContext context, Map<String, dynamic> attributes, Map<String, dynamic>? style);`**
*   **`typedef CustomActionHandler = Future<void> Function(BuildContext? context, Map<String, dynamic> attributes);`**
*   **`typedef DevityErrorWidgetBuilder = Widget Function(BuildContext context, Object error, StackTrace? stackTrace);`**

--- 