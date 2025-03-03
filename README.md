# Devity Documentation

Welcome to the Devity documentation repository. This repository contains all essential guides, API references, SDK usage instructions, infrastructure details, and best practices for using Devity effectively.

## Overview
Devity is a **Server-Driven UI (SDUI) framework** that allows dynamic UI rendering controlled via a backend. It consists of the following key components:
- **Devity Console** (Frontend): Built using **Flutter**, this web-based console allows users to define UI specs dynamically.
- **Devity Backend**: Developed using **FastAPI**, it processes and stores UI specifications, validates configurations, and manages versioning.
- **Devity SDKs**: Currently, the **Flutter SDK** (Dart) is available. A **Next.js SDK** (React) will be introduced in the future.
- **AI Assistant**: Integrated into Devity Console to assist in rapid UI spec creation.

## Repository Structure
- `docs/` - Contains all documentation files.
- `docs/sdk-guides/` - Guides for integrating Devity SDKs.
- `docs/tutorials/` - Step-by-step guides for various features.
- `docs/api-reference/` - API documentation.
- `docs/ai-assistant.md` - Details on AI-assisted spec creation.
- `docs/deployment.md` - Deployment instructions.
- `docs/faq.md` - Frequently Asked Questions.

## How to Use this Repository
1. Clone the repository:
   ```sh
   git clone https://github.com/your-org/devity-docs.git
   cd devity-docs
   ```
2. View the documentation locally:
   ```sh
   pip install mkdocs-material
   mkdocs serve
   ```
   Then, open `http://127.0.0.1:8000/` in your browser.

## Contributions
Contributions are welcome! Feel free to submit PRs to improve documentation.

