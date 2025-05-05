# Backend API Design (Initial Outline)

This document outlines the initial design for the Devity Backend API, primarily serving the Web Console and potentially the Client SDK in specific modes (e.g., debug).

## 1. General Principles

*   **API Style:** TBD (RESTful or GraphQL). Examples below assume RESTful for now.
*   **Authentication:** APIs will be protected. Web Console interactions likely use session-based auth (secure cookies or JWT) after user login. SDK debug interactions likely use API Keys.
*   **Authorization:** Role-Based Access Control (RBAC) will be enforced based on the authenticated user and their permissions (e.g., can edit spec, can publish spec).
*   **Base URL:** TBD (e.g., `https://api.devity.app/v1`)
*   **Error Handling:** Standard HTTP status codes will be used (e.g., 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 500 Internal Server Error). Error responses should include a clear error message or code.

## 2. Authentication Endpoints

*(Endpoints for user login, logout, potentially registration if not handled by a separate auth service/SSO)*

*   **`POST /auth/login`**: Authenticate user (e.g., email/password), return session token/cookie.
*   **`POST /auth/logout`**: Invalidate current session.
*   **`GET /auth/me`**: Get details of the currently authenticated user.

## 3. Spec Management Endpoints

*(Endpoints for creating, reading, updating, and deleting Specs)*

*   **`GET /specs`**: List all specs accessible to the user (potentially with filtering/pagination).
    *   Response: Array of spec summaries (id, name, last updated, current published version).
*   **`POST /specs`**: Create a new spec.
    *   Request Body: Initial spec details (e.g., name).
    *   Response: The newly created spec object (full or summary).
*   **`GET /specs/{specId}`**: Get the latest draft/working version of a specific spec.
    *   Response: Full spec definition (internal representation, not necessarily final JSON).
*   **`PUT /specs/{specId}`**: Update/save the draft/working version of a specific spec.
    *   Request Body: The full spec definition to save.
    *   Response: Updated spec object or success status.
*   **`DELETE /specs/{specId}`**: Delete a spec (consider soft delete).
    *   Response: Success status.
*   **`GET /specs/{specId}/versions`**: List historical versions of a spec.
    *   Response: Array of version summaries (version number, createdAt, publisher).
*   **`GET /specs/{specId}/versions/{versionNumber}`**: Get the content of a specific historical version.
    *   Response: Full spec definition for that version.

## 4. Publishing Workflow Endpoints

*(Endpoints related to the Maker-Checker process and publishing to CDN)*

*   **`POST /specs/{specId}/publish/request`**: Submit the current draft for review.
    *   Request Body: Optional comments.
    *   Response: Status indicating review pending.
*   **`GET /publish/requests`**: List pending review requests (for reviewers).
    *   Response: Array of review request summaries.
*   **`POST /publish/requests/{requestId}/approve`**: Approve a publish request.
    *   Request Body: Optional comments.
    *   Response: Status indicating published version number, triggering background publish-to-CDN job.
*   **`POST /publish/requests/{requestId}/reject`**: Reject a publish request.
    *   Request Body: Optional comments/reason.
    *   Response: Status indicating rejection.
*   **`GET /specs/{specId}/published`**: Get the currently published version details (version number, CDN URL - maybe?).
    *   Response: Published version info.

## 5. SDK Endpoints (Debug/Direct Mode)

*(Endpoints specifically for SDK interaction, authenticated via API Key)*

*   **`GET /sdk/specs/{specId}`**: Get the latest *draft* version of a spec (bypasses CDN and publishing workflow). Requires API Key auth.
    *   Response: Spec JSON (in the final format consumable by the SDK).
*   **`GET /sdk/specs/{specId}/published`**: Get the latest *published* version of a spec (could be an alternative to CDN fetch, still requires API Key). Useful if CDN is unavailable or for specific checks.
    *   Response: Spec JSON.

## 6. Component Management Endpoints (If Applicable)

*(If custom components/types are managed via Console/Backend)*

*   **`GET /components/widgets`**: List custom widgets.
*   **`POST /components/widgets`**: Create/register a custom widget definition.
*   *(Similar endpoints for custom actions, types)*

## 7. User/Project Management Endpoints (If Applicable)

*(If user roles, teams, or projects are managed within this backend)*

*   **`GET /users`**: List users (Admin only).
*   **`POST /users/{userId}/roles`**: Assign roles (Admin only).
*   *(Endpoints for managing projects/teams)*

---

*(This is a preliminary outline. Specific request/response bodies, parameters, and error details need further definition.)* 