---
title: Validation
has_children: false
nav_order: 6
---

# Validation

This section details the validation activities performed to ensure the **UniBo Smart Calendar** artifact meets its requirements. The validation process relies on a robust automated testing framework powered by **Vitest**.

## 5.1. Automated Testing Strategy

The project utilizes **Vitest** as the primary test runner, chosen for its speed and compatibility with the Vite ecosystem. The testing configuration is defined in `vitest.config.mjs`, utilizing the `jsdom` environment to simulate a browser for React components.

### 5.1.1. Test Development Process
Tests are executed via the `npm test` script (`vitest run`). The suite is configured to support:
* **Component Testing:** Using `@testing-library/react` and `@testing-library/jest-dom` to verify UI rendering and user interactions.
* **Global Setup:** A dedicated setup file located at `tests/setupTests.js` initializes the testing environment and global mocks before suites run.

### 5.1.2. Detailed Test Breakdown
The repository organizes tests into specific categories within the `tests/` directory:

1.  **API Verification:**
    * `api.fetch-success.test.js`: Validates that the application can successfully retrieve and parse data when the University endpoints are reachable.
    * `api.error.test.js`: Ensures the application handles network failures and API errors gracefully without crashing.

2.  **Logic & Utility Testing:**
    * `conflictUtils.test.js` & `conflictUtils.extra.test.js`: Verifies the complex logic responsible for detecting overlapping events in the student's schedule.
    * `eventUtils.test.js`: Tests the helper functions that manipulate calendar event objects.

3.  **UI & Smoke Testing:**
    * `smoke.test.jsx`: A high-level test that mounts the application to ensure it does not crash on startup (Basic Sanity Check).
    * `ScheduleContainer.render.test.jsx`: Specifically verifies that the main schedule component renders correctly given a set of props.

### 5.1.3. Code Coverage
To ensure high reliability, code coverage metrics are generated using the command:
```bash
npm run coverage
```

This executes vitest run --coverage, analyzing which lines of code are executed during testing. This metric allows the team to identify untested paths in the logic, particularly within the calendar parsing utilities.

### 5.1.4. Success Criteria
The validation process enforces strict success criteria:

CI Gate: The GitHub Actions pipeline (ci.yml) explicitly runs npm test as a blocking step. If any test fails, the build is marked as failed, preventing merging or deployment.

Browser Compatibility: The browserslist configuration in package.json ensures the build targets modern browsers (Chrome, Firefox, Safari) for development, while supporting a broader range (>0.2%, not dead) for production.

## 5.2. Acceptance Test

User Acceptance Testing (UAT) was conducted to validate the system against the core business requirements. Unlike the automated unit tests which verify code correctness, these tests verified the end-to-end user workflows in the production environment hosted on Vercel.

### 5.2.1. Test Scenarios & Outcomes

The acceptance test plan focused on the three primary functionalities of the system: Discovery, Customization, and Export.

#### Scenario A: Course Discovery & Visualization
**Objective:** Verify that a student can find their specific course among the thousands available in the University database.
* **Procedure:**
    1.  User lands on the homepage (`/`).
    2.  User types "Ingegneria del Software" into the `CourseSelector` component.
    3.  System queries the API and presents a dropdown of matching results.
    4.  User selects the specific course "Ingegneria del Software - 2023/2024".
* **Outcome:** **PASSED**.
    * The fuzzy search logic implemented in the backend correctly filters the University's dataset.
    * Upon selection, the application state updates, and the `CalendarView` component renders the schedule immediately.
    * **Verified Component:** `src/components/CourseSelector.jsx`.

#### Scenario B: Advanced Filtering (Curriculum & Year)
**Objective:** Verify that the calendar can be decluttered to show only relevant lessons.
* **Procedure:**
    1.  After selecting a course, the user interacts with the `CalendarFilters` sidebar.
    2.  User toggles the "Curriculum" filter to "Curriculum A".
    3.  User toggles the "Year" filter to "Year 2".
* **Outcome:** **PASSED**.
    * The `EventList` component updates in real-time.
    * Lessons belonging to "Year 1" or "Curriculum B" are visually removed from the DOM.
    * **Verified Component:** `src/components/CalendarFilters.jsx` and `src/components/YearFilter.jsx`.

#### Scenario C: ICS Export & Interoperability
**Objective:** Verify that the generated calendar file is compatible with external calendar software (Google Calendar, Outlook, Apple Calendar).
* **Procedure:**
    1.  User clicks the "Export .ICS" button.
    2.  The browser requests the endpoint `/calendar.ics`.
    3.  The request is routed via `vercel.json` rewrites to the backend server.
    4.  The server generates a standard iCalendar file using the `ics` library.
* **Outcome:** **PASSED**.
    * The file downloads successfully with the correct MIME type (`text/calendar`).
    * Importing the file into Google Calendar places events in the correct time slots (handling the CET/CEST timezone conversion correctly).
    * **Verified Logic:** `api/server.js` and `vercel.json` routing.

### 5.2.2. Comments w.r.t. Requirements' Acceptance Criteria

The outcomes of these scenarios directly satisfy the acceptance criteria defined during the requirements engineering phase:

| Requirement ID | Description | Acceptance Criteria | Validation Comment |
| :--- | :--- | :--- | :--- |
| **REQ-01 (Data)** | **Accurate Data Representation** | The system must display course times exactly as they appear on the official University website. | **Met.** Validated by `Scenario A` and cross-referenced with `tests/eventUtils.test.js`, which explicitly tests timestamp parsing accuracy. |
| **REQ-02 (UX)** | **Filtering Efficiency** | Users must be able to hide irrelevant courses (e.g., electives they do not take). | **Met.** Validated by `Scenario B`. The modular design of `CalendarFilters.jsx` allows for instantaneous client-side filtering without reloading the page. |
| **REQ-03 (Interop)** | **Standardized Export** | The system must produce RFC-5545 compliant `.ics` files. | **Met.** Validated by `Scenario C`. The use of the robust `ics` node library in `server/index.js` ensures strict adherence to the iCalendar standard. |
| **REQ-04 (Resilience)**| **Error Handling** | The system must not crash if the University API is down. | **Met.** Validated by the resilience tests in `tests/api.error.test.js`, confirming that the app displays user-friendly error toasts via `NotificationManager.jsx` instead of a white screen. |
