# Creating a Spec in Devity

This tutorial walks you through the process of creating a new spec in the **Devity Console**, defining UI components, and deploying it for use in your applications.

## Prerequisites
Before you begin, ensure you have:
- Access to the **Devity Console**
- A registered account and the required permissions to create specs
- Basic understanding of UI components and layouts

## Step 1: Navigate to the Spec Builder
1. Log in to the **Devity Console**.
2. Go to the **Spec Builder** section.
3. Click on **Create New Spec**.

## Step 2: Define Spec Metadata
- Enter a **Spec Name** (e.g., `UserRegistrationForm`)
- Optionally, provide a **Description** for documentation purposes
- Choose the **Version** to manage updates effectively

## Step 3: Add Renderers and Widgets
1. **Create Renderers**:
   - Add a **Top Renderer** (e.g., Header with a title)
   - Add a **Main Renderer** (e.g., Form fields, images, text blocks)
   - Add a **Bottom Renderer** (e.g., Submit button, footer links)
2. **Drag and Drop Widgets**:
   - Use the widget picker to select UI elements (TextFields, Buttons, Dropdowns, etc.)
   - Configure each widget’s properties (labels, placeholder text, required fields)

## Step 4: Configure Actions
Actions define user interactions such as button clicks or form submissions.
- Select a widget (e.g., Submit button)
- Assign an action (e.g., `onClick -> Call API`)
- Configure API details (endpoint, request method, parameters)

## Step 5: Define Rules and Expressions
- Use **Rules** to enable inter-widget communication (e.g., enabling a button when all fields are filled)
- Use **Expressions** to define dynamic behaviors (e.g., conditional visibility of a section)

## Step 6: Preview and Validate
- Click **Preview** to simulate the UI
- Use the **Inspector Tool** to debug any missing configurations
- Ensure all fields and actions behave as expected

## Step 7: Publish and Deploy
1. Click **Publish** to submit the spec for approval (if maker-checker is enabled)
2. Once approved, the spec is published to the CDN
3. Use the Devity SDK in your app to fetch and render the spec dynamically

## Next Steps
- Modify existing specs using the **Versioning System**
- Implement dynamic data binding with APIs
- Explore advanced UI customization using **Custom Widgets**

---

By following these steps, you can create and deploy dynamic UI specifications efficiently using **Devity**.
