---
title: Requirements
has_children: false
nav_order: 3
---

This chapter specifies what **UniBo Smart Calendar** must do, focusing exclusively on the expected system behavior and constraints. Requirements are presented with clear goals, and divided in three categories: **Functional**, **Non-functional**, and **Implementation**. For each requirement, we define the related **acceptance criteria** to make validation objective and testable.

## 2.1 Goals

- **G1 — Centralize academic scheduling information:** provide a single web interface where students can view and manage UniBo academic events (lectures, deadlines, etc.).
- **G2 — Enable schedule personalization:** allow users to filter and organize the displayed schedule according to academic dimensions (e.g., course, curriculum, year).
- **G3 — Support conflict awareness:** detect time overlaps between events and clearly surface them to the user.
- **G4 — Ensure interoperability:** allow users to export and synchronize their schedules with external calendar applications via **ICS** and **subscription URL feed**.
- **G5 — Ensure reliability and maintainability:** provide a solution that is testable, reproducible, and consistent across environments (local + CI).

## 2.2 Glossary / Clarifications

- **Event:** a scheduled item (e.g., lecture) with at least title, start/end datetime, and optional metadata (location, notes).
- **Conflict:** two events whose time intervals overlap (adjacent events are not considered conflicts).
- **ICS export:** generation of a downloadable iCalendar (`.ics`) file containing the selected events.
- **Subscription URL feed:** a URL that can be added to external calendar apps to keep events synchronized.

---

## 2.3 Functional Requirements (with User Stories)

To capture expected behavior from the user perspective, we define the following **user stories**. Each includes concise **acceptance criteria** (Given/When/Then).

### US-01 — View weekly schedule
**As a** UniBo student, **I want** to view my weekly timetable in a calendar view **so that** I can understand my lectures at a glance.  
**Acceptance criteria**
- **Given** schedule data is available, **when** I open the Calendar view, **then** events are displayed on the correct day/time.
- **Given** events exist, **when** I change the displayed week, **then** the calendar updates accordingly.

### US-02 — Filter by academic dimensions
**As a** student, **I want** to filter the schedule by **course/program/year/curriculum** **so that** I only see relevant lectures.  
**Acceptance criteria**
- **Given** filters are available, **when** I select a filter value, **then** only matching events remain visible.
- **Given** filters are applied, **when** I reset filters, **then** the full schedule is shown again.

### US-03 — Detect and highlight conflicts
**As a** student, **I want** the system to automatically detect overlapping lectures **so that** I can identify conflicts.  
**Acceptance criteria**
- **Given** two events overlap in time, **when** the schedule is rendered, **then** overlapping events are visually flagged as conflicts.
- **Given** two events are adjacent but not overlapping, **when** rendered, **then** they are not flagged as conflicts.

### US-04 — View events in a list
**As a** student, **I want** to view events as a list **so that** I can quickly scan titles, locations, and times.  
**Acceptance criteria**
- **Given** events exist, **when** I open the Event List page, **then** each event shows at least title and date/time (and location if available).
- **Given** filters are applied, **when** I open the list, **then** it reflects the same filtered dataset.

### US-05 — Export calendar as ICS
**As a** student, **I want** to export my personalized schedule as an **ICS file** **so that** I can import it into external calendar apps.  
**Acceptance criteria**
- **Given** a schedule is loaded, **when** I select “Export ICS”, **then** a valid `.ics` file is generated and downloadable.
- **Given** filters are applied, **when** I export, **then** the ICS contains only the filtered events.

### US-06 — Subscribe via URL feed
**As a** student, **I want** to subscribe to a calendar **URL feed** **so that** my calendar stays synced in Google/Outlook/Apple Calendar.  
**Acceptance criteria**
- **Given** a subscription URL is available, **when** I copy it, **then** it can be used as a calendar subscription source in external apps.
- **Given** the subscription URL is requested, **when** accessed, **then** the system returns a valid calendar feed.

### US-07 — Robust handling of API errors
**As a** student, **I want** clear feedback when schedule retrieval fails **so that** I understand what happened and can retry.  
**Acceptance criteria**
- **Given** the backend returns an error, **when** I request a schedule, **then** the UI shows a user-friendly error state/message.
- **Given** a failure occurred, **when** I retry, **then** the system attempts the request again.

### US-08 — Fast access via caching (if enabled)
**As a** student, **I want** quick access to previously loaded schedules **so that** I can use the app even with unstable connectivity.  
**Acceptance criteria**
- **Given** a schedule was previously loaded, **when** I reopen the app, **then** the schedule loads quickly from cache (if implemented).
- **Given** the network is unavailable, **when** cached data exists, **then** the app can display the last available schedule (if implemented).

---

## 2.4 Non-functional Requirements

### NFR-01 — Performance (interactive usage)
The application should remain responsive during normal usage (navigation, filtering, rendering).  
**Acceptance criteria**
- **Given** the user applies filters, **when** the UI updates, **then** the interaction completes without noticeable lag during typical usage.

### NFR-02 — Reliability and error tolerance
The system must handle failures gracefully (e.g., UniBo source unavailable, network errors).  
**Acceptance criteria**
- **Given** schedule retrieval fails, **when** the error occurs, **then** the UI displays an error state and allows retry.

### NFR-03 — Compatibility / interoperability
Exported or subscribed calendars must be compatible with common calendar apps.  
**Acceptance criteria**
- **Given** an ICS export or subscription feed, **when** imported/subscribed in Google Calendar, Outlook, or Apple Calendar, **then** events appear with correct times and titles.

### NFR-04 — Testability
Core logic and critical UI behavior should be covered by automated tests.  
**Acceptance criteria**
- **Given** the repository is cloned, **when** `npm test` is executed, **then** the test suite completes successfully (locally and in CI).

---

## 2.5 Implementation Requirements

### IR-01 — Technology stack constraints
The project must use a modern JavaScript stack with the selected tooling.  
**Acceptance criteria**
- **Given** the repository, **when** installing dependencies, **then** the project builds and runs using Node.js (v18+) and npm (v9+).

### IR-02 — Frontend framework and UI libraries
The frontend must be implemented in **React** and use the chosen UI/calendar libraries.  
**Acceptance criteria**
- **Given** the application is started, **when** accessing the frontend, **then** the UI renders correctly using the declared libraries.

### IR-03 — Testing and CI constraints
Tests must run locally and automatically in CI on every push/PR.  
**Acceptance criteria**
- **Given** a pull request, **when** CI runs, **then** it executes install → test → build and reports pass/fail status.
