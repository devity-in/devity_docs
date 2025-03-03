# Devity Next.js SDK Guide

Welcome to the **Devity Next.js SDK Guide**. This document provides instructions for integrating the Devity SDK into your Next.js application to dynamically render UI based on server-driven specifications.

## Installation
To install the Devity SDK in your Next.js project, use the following command:

```sh
npm install @devity/sdk
```
Or, if using Yarn:
```sh
yarn add @devity/sdk
```

## Initialization
Initialize the SDK in your project by configuring it with the API endpoint and optional authentication token. Create a `devityConfig.ts` file:

```typescript
import { DevitySDK } from "@devity/sdk";

export const devity = new DevitySDK({
  baseUrl: "https://api.devity.com", // Replace with actual API URL
  authToken: "your_auth_token", // Optional authentication token
});
```

## Fetching and Rendering a Spec
To render a UI spec dynamically, fetch it from the backend and use the provided `DevityRenderer` component:

```typescript
import { useEffect, useState } from "react";
import { DevityRenderer, DevitySpec } from "@devity/sdk";
import { devity } from "../devityConfig";

export default function SpecPage({ specId }: { specId: string }) {
  const [spec, setSpec] = useState<DevitySpec | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchSpec() {
      try {
        const response = await devity.getSpec(specId);
        setSpec(response);
      } catch (error) {
        console.error("Failed to load spec", error);
      } finally {
        setLoading(false);
      }
    }
    fetchSpec();
  }, [specId]);

  if (loading) return <p>Loading...</p>;
  if (!spec) return <p>Error loading spec</p>;

  return <DevityRenderer spec={spec} />;
}
```

## Handling Actions
Devity SDK allows handling predefined actions such as navigation, API calls, and modals. Define action handlers globally:

```typescript
devity.setActionHandler((action, context) => {
  switch (action.type) {
    case "navigate":
      window.location.href = action.data["url"];
      break;
    case "alert":
      alert(action.data["message"]);
      break;
    default:
      console.warn("Unknown action: ", action.type);
  }
});
```

## Debugging Mode
For development purposes, enable debug mode to fetch specs directly from the backend instead of the CDN:

```typescript
devity.enableDebugMode();
```

## Conclusion
The Devity Next.js SDK allows you to create dynamic, server-driven UIs with minimal effort. For more details, visit the [Devity Docs](https://github.com/your-org/devity_docs).

