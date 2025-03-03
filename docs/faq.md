# Frequently Asked Questions (FAQ)

## General Questions

### What is Devity?
Devity is a **Server-Driven UI (SDUI) framework** that allows developers to create dynamic and configurable UI experiences controlled from a backend. It consists of **Devity Console**, **Devity Backend**, and **Devity SDKs**.

### How does Devity differ from traditional UI development?
Traditional UI development requires releasing new app versions for UI changes. With Devity, UI updates happen dynamically via a backend-driven JSON spec, reducing deployment time and enhancing flexibility.

### Who can benefit from using Devity?
- **App developers** who want to reduce release cycles and make UI updates without requiring users to update their apps.
- **Product teams** who need dynamic UI workflows without developer intervention.
- **Enterprises** looking for a scalable and centralized UI management system.

## Technical Questions

### What technologies power Devity?
- **Devity Console:** Built using **Flutter Web**.
- **Devity Backend:** Developed with **FastAPI**.
- **Devity SDKs:** Initially available in **Flutter (Dart)**, with a **Next.js SDK planned** for future releases.

### How does Devity handle UI updates?
UI updates are controlled via **JSON specs** stored in a **CDN**. The client app fetches the latest spec, ensuring instant UI updates without requiring a new app release.

### What happens if there is an error in the JSON spec?
Devity has built-in validation mechanisms to prevent invalid specs from being published. Additionally, apps can fall back to a **previously cached version** in case of spec retrieval issues.

## Deployment & Integration

### How do I deploy Devity Backend and Console?
Refer to the [Deployment Guide](deployment.md) for step-by-step instructions on setting up Devity Backend, Console, and SDKs.

### Can I self-host Devity?
Yes, you can self-host Devity Backend and Console on your infrastructure. The recommended setup includes **Docker, Kubernetes, and a CDN** for JSON specs.

### Does Devity require an internet connection?
- **For dynamic updates:** Yes, since the JSON spec is fetched from a backend or CDN.
- **For offline usage:** The last fetched spec can be cached and used when offline.

## Customization & Extensibility

### Can I create custom widgets?
Yes, Devity supports **custom widgets and actions**, allowing developers to extend the framework for specific use cases.

### How do I define business logic in Devity?
Devity allows defining business logic via **Expressions, Rules, and Actions**, enabling conditional logic, API calls, and UI interactions.

## Future Roadmap

### What’s planned for future releases?
- **Next.js SDK** for web applications.
- **AI-powered Spec Assistant** for guided UI creation.
- **Versioning & rollback support** for UI specs.

### Where can I track updates?
Check the official repository and documentation for the latest updates and feature releases.

## Support & Community

### Where can I get help with Devity?
- **Official Documentation:** [Link to Docs]
- **GitHub Issues:** Report bugs or request features.
- **Community Forum:** Join discussions with other developers.

### How can I contribute to Devity?
We welcome contributions! Check out the contribution guidelines in the repository for details on how to submit code, documentation, or feedback.

