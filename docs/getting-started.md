# Getting Started with Devity

Welcome to **Devity**, the Server-Driven UI (SDUI) framework that enables dynamic UI updates without requiring app releases. This guide will help you set up Devity and start building your first SDUI-powered application.

## Prerequisites
Before getting started, ensure you have the following installed:

- **Flutter** (for Devity Console & SDK) – [Install Flutter](https://flutter.dev/docs/get-started/install)
- **Python 3.9+** (for Devity Backend) – [Install Python](https://www.python.org/downloads/)
- **FastAPI & Uvicorn** – Backend dependencies
- **PostgreSQL** (or preferred database) for storing UI specs
- **CDN or Cloud Storage** (for hosting JSON UI specs)

## Installation & Setup

### 1. Clone the Devity Repositories
```sh
# Clone Devity Console
git clone https://github.com/your-org/devity-console.git

# Clone Devity Backend
git clone https://github.com/your-org/devity-backend.git

# Clone Devity SDK (Flutter)
git clone https://github.com/your-org/devity-sdk-flutter.git
```

### 2. Setting Up Devity Backend
Navigate to the `devity-backend` directory and create a virtual environment:
```sh
cd devity-backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```
Install dependencies:
```sh
pip install -r requirements.txt
```
Run the FastAPI server:
```sh
uvicorn main:app --reload
```
Access the API documentation at `http://localhost:8000/docs`.

### 3. Setting Up Devity Console
Navigate to the `devity-console` directory and run:
```sh
flutter pub get
flutter run
```
This starts the Devity Console, where you can design UI workflows visually.

### 4. Running Devity SDK (Flutter)
To integrate Devity into your Flutter app, add the SDK to `pubspec.yaml`:
```yaml
dependencies:
  devity_sdk:
    git:
      url: https://github.com/your-org/devity-sdk-flutter.git
```
Then, fetch dependencies:
```sh
flutter pub get
```
Initialize Devity in your Flutter app:
```dart
import 'package:devity_sdk/devity_sdk.dart';

void main() {
  runApp(DevityApp());
}
```

## Creating Your First UI Spec
1. Open **Devity Console**.
2. Create a new **Spec**.
3. Add **Renderers, Widgets, and Actions** to define your UI.
4. Publish the Spec to CDN.
5. Run your app – the UI updates dynamically!

## Next Steps
- Learn about **JSON UI Spec format**.
- Explore **AI-assisted spec creation**.
- Dive deeper into **dynamic data binding and actions**.

For detailed documentation, visit the [Devity Docs](https://github.com/your-org/devity_docs).

