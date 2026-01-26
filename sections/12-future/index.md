---
title: Future work
has_children: false
nav_order: 13
---

# Known issues and future work

This section summarizes the main limitations of **UniBo Smart Calendar** at the time of delivery and outlines realistic improvements for future iterations. The goal is to be transparent about what is missing or imperfect and to provide a concrete roadmap for extending the product.

## 12.1 Known issues (current limitations)

### K1 | Dependency on UniBo sources
The system relies on UniBo-provided calendar sources (ICS/JSON endpoints). If URLs, formats, or field semantics change, schedule retrieval and parsing may break or produce incomplete data.

### K2 | Calendar interoperability differences
Although ICS export and subscription are supported, external calendar applications (Google Calendar, Outlook, Apple Calendar) may interpret certain fields differently (e.g., timezones, recurring rules, descriptions). Some events might appear with minor formatting differences depending on the client.

### K3 | Limited resilience under unstable connectivity
When connectivity is poor or UniBo servers are slow/unavailable, users may experience failures in schedule retrieval. The UI can show error states and allow retry, but the overall experience depends on network stability. If local caching/offline mode is not fully implemented, the application cannot guarantee access without a connection.

### K4 | Performance constraints for large schedules
Rendering a very high number of events (e.g., multiple curricula/years at once) may introduce UI lag, especially during filtering or re-render operations. Performance is acceptable for typical usage but may degrade with extreme inputs.

### K5 | Coverage gaps and scenario completeness
Automated tests cover core scenarios, but edge cases are not exhaustive (e.g., unusual event formats, rare overlaps, invalid/missing fields, extreme schedules). This may allow regressions or unexpected behaviors to slip through in less common cases.

---

## 12.2 Missing or partially implemented features

### M1 | Full offline-first experience
A robust offline mode (persistent cache, explicit “last updated” timestamp, and offline indicators) may be incomplete or not fully integrated, limiting usability without connectivity.

### M2 | User persistence and personalization
The current system may not persist user preferences across devices/sessions (e.g., favorite filters, default view, selected curriculum). There is no user profile or login-based personalization.

### M3 | Advanced schedule planning
The application focuses on visualizing and exporting schedules. More advanced “study planning” features (e.g., creating multiple timetable variants, comparing plans, saving scenarios) are not fully supported.

### M4 | Extended event semantics
Some academic scheduling elements (e.g., cancellations, room changes, exam sessions, lab groups, special notes) may not be fully represented or normalized, depending on what UniBo provides and what the parser extracts.

---

## 12.3 Future work (roadmap)

### 12.3.1 Frontend / UX improvements
- **Accessibility (a11y):** improve keyboard navigation, ARIA labeling, focus management, and contrast compliance.
- **Mobile responsiveness:** optimize layout for smaller screens and touch interactions (filters, calendar navigation, list readability).
- **Better conflict visualization:** add clearer conflict explanations (e.g., tooltip with overlapping events, conflict list summary, “conflict-only” filter).
- **User preferences persistence:** save default view (week/month/list), last-used filters, and UI preferences (local storage or server-side profiles).
- **Improved error UX:** add actionable error messages (e.g., “source unavailable”, “invalid feed”), retry with backoff, and connection status hints.

### 12.3.2 Backend / data processing improvements
- **Source robustness:** add stricter validation and fallback behavior if UniBo provides partial or inconsistent data.
- **Richer normalization:** standardize timezones, locations, and titles more consistently; enrich metadata where possible.
- **Caching strategy:** implement a reliable caching layer (server-side and/or client-side) with expiration rules and “last updated” metadata.
- **Scalability:** optimize parsing and response generation for heavy usage (batch requests, reduced recomputation, improved performance under load).

### 12.3.3 QA / CI-CD / operations improvements
- **Broader test suite:** add more tests for edge cases (invalid ICS, missing fields, unusual overlaps, time boundaries).
- **Coverage targets:** define and track coverage thresholds in CI (where appropriate) to prevent regressions.
- **Smoke tests after deployment:** add lightweight post-deploy checks to ensure core endpoints and the subscription URL are working.
- **Release automation:** streamline version tagging and release artifact creation from CI to reduce manual steps.

---

## 12.4 Expected impact of future work
Addressing the items above would improve:
- **Reliability** (less fragile source handling, better caching, stronger tests),
- **Usability** (more responsive UI, improved mobile/a11y, clearer conflict UX),
- **Adoption** (simpler subscription/export experience across calendar platforms),
- **Maintainability** (cleaner data contracts and automated quality gates).
