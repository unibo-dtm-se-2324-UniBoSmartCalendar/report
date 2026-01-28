---
title: Development
has_children: false
nav_order: 5
---

# Development


### 3.1 DVCS and Versioning Strategy

Version control was managed using Git, adopting the Software Versioning methodologies discussed during the course to assign unique identifiers to specific states of the software.

**Versioning Approach (SemVer):**
The project strictly follows Semantic Versioning (SemVer) using the X.Y.Z format.

* **Major (X):** Incremented for changes that are incompatible with the previous version. The project is currently at the stable version 1.0.0.
* **Minor (Y):** Incremented for the addition of new backward-compatible features (e.g., the addition of the statistics dashboard).
* **Patch (Z):** Incremented for backward-compatible bug fixes (e.g., fixes in event parsing).

**Commit Conventions (Conventional Commits):**
To ensure a readable and automatable change history, the team adopted the Conventional Commits standard. Commit messages follow the format `type(scope)!: description`, where:

* **feat:** introduces a new feature (corresponds to a Minor version increment).
* **fix:** resolves a bug (corresponds to a Patch version increment).
* **docs, style, test, chore:** used for changes that do not impact production logic.

The use of the exclamation mark (!) or the wording **BREAKING CHANGE** in the commit body indicates structural changes that require a Major version increment.

**Branch and Release Management:**
Development was divided into milestones tracked in the `CHANGELOG.md`, which chronologically documents releases (e.g., v0.1.0 initial scaffold, v0.4.0 test suite). This approach facilitates requirement traceability and ensures the stability of the main branch.

---

### 3.2 Implementation Details

**Network Protocols:**
Communication between the React frontend and the Node.js backend takes place via the HTTP/HTTPS protocol. A Proxy Server was implemented in the backend to handle requests to the University of Bologna servers. This technical choice is necessary to overcome browser CORS restrictions when retrieving the original timetables.

**Data Representation:**

* **JSON:** Used for API message exchange and for local persistence of profile configurations.
* **iCalendar (.ics):** Standard format used for timetable export and calendar subscription, ensuring interoperability with Google Calendar and Outlook.

**State Management and Persistence:**
The system adopts a hybrid model. User preferences are saved in the browser’s LocalStorage, while the server maintains a temporary Map (`profileStore`) to dynamically generate `.ics` files associated with a unique `profileId`.

**Authentication:**
An identification mechanism based on anonymous client-side generated profiles (UUIDs) is used, eliminating the need for complex databases or mandatory logins, in line with the goal of providing a fast tool for students.

---

### 3.3 Technological Details

**Technology Stack:**

* **Frontend:** React 18 for managing a reactive, component-based user interface.
* **Backend:** Node.js with the Express framework for API handling and parsing logic.
* **UI Framework:** Material UI (MUI v5) to ensure a modern and accessible design.

**Core Libraries:**

* **axios:** For asynchronous API calls.
* **ics:** For generating files compliant with the iCalendar standard.
* **react-big-calendar:** Main component for graphical event visualization.

**Testing and Quality:**
The project uses Vitest as the test runner, chosen for its speed and compatibility with the modern ecosystem (Vite/React). The CI pipeline (GitHub Actions) automatically runs tests on every push to prevent regressions.


