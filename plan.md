```markdown
# Implementation Plan: Facebook Profile Locator (Educational Demo)

This plan outlines the creation of an educational demo that simulates locating a user’s location from a Facebook profile URL. The implementation avoids any real scraping or API integration and instead uses simulated responses to respect privacy and legal boundaries. The demo will include a modern, clean UI and robust error handling.

---

## 1. Create a New Page for the Feature

### File: `src/app/fb-locator/page.tsx`
- **Purpose:** Display the UI with an input field for the Facebook profile URL and show the location result.
- **Steps:**
  - Mark the file as a client component by adding `"use client"` at the top.
  - Create a centered container with a clean heading (e.g., “Facebook Profile Locator”).
  - Add a styled text input with placeholder text (e.g., “Enter your Facebook profile URL”).
  - Add a button labeled “Locate” to trigger the location search.
  - Use React hooks (`useState`) to manage the URL input, loading state, error messages, and response results.
  - On form submission, call the backend API endpoint (`/api/fb-locator`) via `fetch` to send the Facebook URL.
  - Display a loading indicator (e.g., “Loading…”) when the request is processing.
  - On success, render the returned location information in a styled results card.
  - On error, show a concise error message.

---

## 2. Create an API Endpoint for Simulated Location Extraction

### File: `src/app/api/fb-locator/route.ts`
- **Purpose:** Process incoming POST requests with a Facebook URL and return a simulated location.
- **Steps:**
  - Implement a POST handler that reads JSON data from the request.
  - Validate that the request payload contains a `url` property. Use a basic regular expression to check if the URL begins with `https://www.facebook.com/`.
  - If validation fails, return a 400 response with an appropriate error message.
  - If the URL is valid, simulate location extraction (for example, return a static object: `{ location: "New York, USA" }`). Optionally, use simple heuristics (e.g., if the URL contains a particular keyword, return a different location).
  - Include error handling via try/catch blocks and return a 500 status for unexpected errors.

---

## 3. UI/UX Considerations

- **Styling & Layout:**
  - Use modern typography and spacing achieved via CSS in `src/app/globals.css` or inline styles.
  - Ensure the input field and button have ample padding, clear borders, and a consistent color palette (avoiding icon libraries or external images).
  - The results card should be styled with gentle borders, rounded corners, and a clear visual hierarchy.
- **User Feedback & Error Handling:**
  - Validate input on the client-side and highlight errors if the entered URL does not match the Facebook URL format.
  - Display real-time status (e.g., disabling the button when a request is in progress).
  - Provide clear messages for both successful retrieval and error conditions.

---

## 4. Testing and Best Practices

- **API Endpoint Testing:**
  - Use `curl` to test the API endpoint. For example:
    ```bash
    curl -X POST http://localhost:3000/api/fb-locator \
      -H "Content-Type: application/json" \
      -d '{"url": "https://www.facebook.com/sampleprofile"}'
    ```
  - Verify that invalid URLs return a 400 response with an error message.
- **Error Handling:**
  - Both the client and API code contain proper try/catch blocks.
  - Return error responses with appropriate HTTP status codes.
- **Coding Best Practices:**
  - Ensure code is modular and well-commented.
  - Use template literals for any dynamic string or URL construction.

---

## 5. Integration Summary

- **No modifications** are required for project-wide files like `next.config.ts`, `tsconfig.json`, or `globals.css` unless further styling adjustments are needed.
- This feature is self-contained under the `fb-locator` route (both client page and API endpoint).
- Future improvements may include more realistic heuristics or integration with location-detection services (with user consent).

---

## Summary

- A new page (`src/app/fb-locator/page.tsx`) provides a modern UI for inputting a Facebook profile URL.
- An API endpoint (`src/app/api/fb-locator/route.ts`) processes POST requests and simulates location extraction.
- Input validation ensures URLs start with `https://www.facebook.com/`; errors are gracefully handled.
- The client-side UI uses state management to show loading indicators, results, and error messages.
- Styling uses clean typography, spacing, and layout without external icon libraries.
- Comprehensive error handling and testing with curl commands ensure robustness and best practice compliance.
