# Core Concepts: Specs and Workflows

At the heart of Devity lies the **Spec** (short for Specification). A Spec is the blueprint for a user interface flow, screen, or even a small part of a screen within your application.

## What is a Spec?

Think of a Spec as a declarative, structured description of a UI and its behavior. Instead of writing platform-specific UI code (like Flutter Widgets or React Components directly in your app), you define the UI using a hierarchical tree structure represented in a universal format (JSON). This JSON Spec is created and managed via the Devity Web Console and served to your application by the Devity Backend and CDN.

The Devity Client SDK within your application reads this Spec and translates it into actual native UI elements that the user sees and interacts with.

**Key Characteristics of a Spec:**

*   **Declarative:** Describes *what* the UI should look like and how it should behave, not *how* to imperatively build it step-by-step.
*   **Hierarchical:** Composed of nested components (Renderers organizing Widgets).
*   **Platform-Agnostic:** The JSON structure itself is independent of Flutter, React Native, Web, etc. The Client SDK handles the platform-specific translation.
*   **Dynamic:** Can include bindings to dynamic data, expressions for logic, and actions for interactivity.
*   **Versioned:** Specs are versioned to ensure stability and controlled rollouts.

## Specs as Workflows

A single Spec often represents a complete **Workflow** or user journey. This could be:

*   An onboarding flow with multiple screens.
*   A user profile editing screen.
*   A product details page.
*   A multi-step form.
*   A promotional banner display.

A workflow is typically composed of one or more screens. Within a Spec, screens are defined, and navigation between them is handled using specific Actions (like `NavigateAction`). The Spec defines the initial screen to load and the sequence of interactions and transitions within that workflow.

## Structure of a Spec

While the detailed JSON structure is defined in the [Spec Schema](../reference/spec_schema.md), conceptually, a Spec is a tree containing nodes like:

*   **Screen Nodes:** Define individual screens within the workflow.
*   **Renderer Nodes:** Control the layout of child components (e.g., arranging them in a column or row).
*   **Widget Nodes:** Represent the actual UI elements (e.g., Text, Button, Image, TextField).
*   **Action Nodes:** Define operations to be performed on events (e.g., API Call, Navigate, Show Alert).
*   **Rule Nodes:** Define conditions for inter-widget communication.
*   **Data Binding Information:** Specifies how dynamic data connects to widget attributes.
*   **Expressions:** Define logic embedded within the spec.

By composing these elements within the Web Console, you build a complete, self-contained description of a UI workflow that can be served dynamically to your application. 