---
title: Self-evaluation
has_children: false
nav_order: 12
---

# Self-evaluation

## Giulia

### Role and contributions
During the development of **UniBo Smart Calendar**, I mainly worked as Frontend Architect & UI/UX contributor. My work focused on building the user-facing layer and ensuring that the application was usable, navigable, and consistent with the required features.

Concretely, my main contributions were:
- **Project scaffold and baseline setup**: client structure, initial configuration, and ensuring the project could run and build correctly.
- **UI shell implementation**: including the main navigation structure and the core interface components (calendar view container, filters, and base pages such as settings/notifications/statistics where applicable).

### Strengths of my work (and of the product, from my perspective)
- **User-centered structure:** I contributed to a clear UI flow (from adding timetables to visualizing and filtering the schedule), which makes the application approachable for students.
- **Feature completeness at UI level:** the project offers a coherent interface for calendar visualization, filtering, conflict awareness, and interoperability features (export/subscription), which are the main user-visible outcomes.
- **Collaboration and integration mindset:** contributing to merges and keeping the UI consistent with shared utilities/services helped reduce integration issues late in the project.

### Weaknesses / areas for improvement
In my opinion, the user interface could be made smoother and even more intuitive, i.e. clearer loading states, error feedback, and more guided feedback for incorrect inputs.

### What I learned
This project strengthened my ability to design and implement a non-trivial React-based UI with modular components and service integration, to manage a codebase and contribute effectively to shared integration branches, and to reason about usability constraints (filters, conflicts, navigation) and translate them into implementable UI behavior.

### Final reflection
I particularly enjoyed working on this project because it aligned well with my interest in a user-centered perspective, which is consistent with my academic background. Moreover, my internship experience, where I worked with Jira and had responsibilities similar to a Product Owner (e.g., managing issues, aligning features to user needs, and structuring work into clear deliverables), made the UI/UX and interaction design aspects especially engaging. This project allowed me to apply that mindset directly to a concrete product.
Overall, I believe my contribution was consistent with my role: delivering a functional and navigable frontend, supporting the project baseline, and ensuring integration stability. Given more time, I would focus on improving UX details (feedback, accessibility, responsiveness).

## Simone

### Role and Responsibilities
In the **UniBo Smart Calendar** project, I covered the role of **DevOps & QA Specialist**. My primary objective was to establish the engineering "baseline" regarding infrastructure, automated verification, and repository governance, ensuring the team could work on a stable and standardized foundation.

My specific contributions, aligned with the project's changelog, included:
1.  **CI/CD Implementation (v0.2.0):** I designed the Continuous Integration pipeline using GitHub Actions to automate the testing and build processes.
2.  **Quality Assurance Strategy (v0.4.0):** I architected and implemented the comprehensive test suite, covering domain logic, UI components, and API error handling.
3.  **Repository Governance (v0.2.0 & v0.4.1):** I established the project's versioning rules (SemVer), licensing (MIT), and standardized documentation (README structure and status badges).
4.  **Deployment Infrastructure:** I managed the cloud hosting configuration on Vercel, ensuring the frontend and backend proxy could be deployed seamlessly from the same repository.

### Technical Challenges & Solutions

#### Challenge 1: CI Pipeline for a Monorepo Structure
**Context:** Our project contains both client and server logic in a single repository, which initially complicated the build process in the CI environment.
* **Solution:** I configured the `.github/workflows/ci.yml` to properly handle dependency installation (`npm ci`) and caching. This ensured that both the React frontend and the backend utilities were verified in a single, efficient workflow run, preventing "works on my machine" issues.

#### Challenge 2: Establishing a Robust QA Baseline
**Context:** As indicated in Release 0.4.0, the application required a test suite that covered not just the "happy paths" but also edge cases.
* **Solution:** I integrated **Vitest** as our test runner due to its speed and Vite compatibility. I wrote the critical smoke tests (`smoke.test.jsx`) and API error tests (`api.error.test.js`) to validate that the system degrades gracefully when the university servers are unreachable—a key requirement for the "QA Specialist" role.

#### Challenge 3: Standardization & Documentation
**Context:** With multiple contributors, the project risked becoming fragmented in terms of style and documentation.
* **Solution:** In Release 0.4.1, I formalized the repository structure. I updated the `README.md` to include clear "Setup & Installation" and "Architecture" sections, and added dynamic badges to provide immediate visual feedback on the build status and versioning.

### Professional Growth & Learning Outcomes

This project allowed me to specialize in the operational side of software engineering:
* **Automated Quality Gates:** I learned the importance of blocking bad code *before* it merges. By enforcing tests in the CI pipeline, I shifted our quality checks left, catching regressions early.
* **Infrastructure as Code:** Managing the `vercel.json` and GitHub Actions workflows gave me practical experience in defining infrastructure through configuration files rather than manual server setups.
* **Release Management:** I gained experience in maintaining a `CHANGELOG` and adhering to Semantic Versioning, understanding how these practices facilitate better collaboration and project tracking.

### Final Conclusion
As the DevOps & QA Specialist, I am satisfied with the stability and quality of the final artifact. The automated pipeline and comprehensive test suite provide a safety net that allowed the backend and frontend developers to move quickly. The infrastructure is now fully automated, requiring zero manual intervention for deployment, which meets the professional standards expected of a modern software project.

### Alessandro

#### Role and Responsibilities

In the **UniBo Smart Calendar** project, I covered the role of **Backend Engineer & Logic**. My primary objective was to build the application's "engine" by managing the acquisition of data from university servers, its normalization, and the development of the business logic for conflict resolution.

My specific contributions, aligned with the project's changelog, included:

* **Backend Proxy Development (v0.1.0 & v0.3.0):** I designed the Express server to function as a proxy, resolving CORS issues and allowing reliable fetching of schedule data from UniBo servers.
* **Conflict Detection Engine (v0.3.0):** I created and implemented the proprietary algorithm for the automatic identification of temporal overlaps between lectures, which is the heart of the domain logic.
* **Data Normalization and Parsing (v0.3.0):** I developed the backend services to clean and standardize raw data, ensuring the frontend receives event objects ready for rendering.
* **iCalendar (.ICS) Export:** I integrated the logic for generating `.ics` files to allow the subscription and export of the personalized calendar to external apps such as Google Calendar and Outlook.

#### Technical Challenges & Solutions

**Challenge 1: Overcoming CORS Restrictions**

* **Context:** The browser blocked direct requests to the University's timetable servers for security reasons, preventing data loading on the client side.
* **Solution:** I implemented the `/api/fetch-schedule` proxy endpoint in the `server/index.js` file. By using the `axios` library on the server side, I bypassed browser restrictions, allowing the backend to download the data and serve it to the frontend safely and transparently.

**Challenge 2: Developing an Efficient Conflict Detection Algorithm**

* **Context:** With fragmented schedules and multiple courses, visually identifying overlaps was the main challenge of the project.
* **Solution:** I developed the `conflictUtils.js` module. The algorithm analyzes each event against others in the same time frame, marking "overlaps" with specific metadata that the frontend uses for visual flagging, drastically improving the utility of the schedule for the student.

**Challenge 3: Standardizing the ICS Format for Export**

* **Context:** The events received from UniBo servers were not compliant with the international iCalendar standard required by apps like Apple Calendar or Outlook.
* **Solution:** I implemented the `generateICSContent` function in the backend using the `ics` library. This process transforms the events filtered by the user into an RFC 5545 compliant data stream, allowing for perfect cross-platform synchronization.

#### Professional Growth & Learning Outcomes

This project allowed me to specialize in server-side software engineering competencies:

* **Proxy Architecture and APIs:** I learned how to manage communications between heterogeneous systems and how to structure a backend that acts as a normalization layer for non-structured external data.
* **Complex Domain Logic:** Developing the conflict management system taught me the importance of separating heavy computational logic from the interface rendering, optimizing overall performance.
* **Interoperability and Standards:** The implementation of the `.ics` format gave me a practical understanding of global data exchange standards and how critical data validation is at the entry and exit points.

#### Final Conclusion

As the Backend Engineer, I am satisfied with the implemented data architecture. The "Data Flow" I designed—which moves from the proxy server to the client via the parser—ensures that the application is robust and scalable. The conflict resolution logic and the export system provide real added value, transforming a simple schedule viewer into a professional academic planning tool that meets the software engineering standards required for this project.







