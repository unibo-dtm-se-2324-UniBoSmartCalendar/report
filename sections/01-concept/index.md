---
title: Concept
has_children: false
nav_order: 2
---

## Disclaimer on the use of Generative AI

During the development of **UniBo Smart Calendar**, Generative AI tools were used extensively as **programming assistants**. Their main contribution was in supporting the implementation of non-trivial code, such as proposing solution approaches, generating initial code drafts, clarifying the usage of specific libraries/frameworks, and suggesting refactorings to improve readability and maintainability.

Importantly, AI-generated suggestions were treated as **starting points**, not as final deliverables. All AI-assisted code was **reviewed, understood, corrected, and adapted** by the team, and then validated through manual testing and automated checks (unit/integration tests and CI). The team ensured that the implemented behavior matched the intended functionality and quality standards.

While AI tools could be used to explore alternative solutions or clarify technical options, all **final decisions** regarding system behavior, architecture, and project scope were taken by the team. In addition, none of the authors has a formal background in Software Engineering, therefore Generative AI tools were also used to bridge knowledge gaps and accelerate learning; nevertheless, the team made an explicit effort to **understand and justify** the adopted solutions rather than applying them blindly.

The authors take **full responsibility** for the final software artifact and for the content of this report.

# Concept

**UniBo Smart Calendar** is a **web-based application with a graphical user interface** designed to help University of Bologna students manage academic schedules in a clearer and more efficient way. The project combines a **React web frontend** (user-facing GUI) with a **Node.js/Express backend** that provides **web services** for schedule retrieval and transformation.

From a product perspective, the system can be described as:

- **Web Application (GUI):** students interact through a browser to view their timetable, navigate different views, and apply filters.  
- **Web Service(s):** the backend exposes endpoints that fetch and process university schedule sources and return clean data to the client.  
- **Lightweight data processing component:** the system parses and normalizes raw scheduling information (original UniBo calendar sources) into structured data suitable for rendering and calendar interoperability.

For delivery and accessibility, the application can be deployed on a cloud platform such as **Vercel**, enabling users to access the system via the web and, when configured, consume the calendar feed remotely.

The main use cases supported by the product are:
1. **Schedule visualization and organization:** users can view lectures and academic events in a calendar layout and access supporting lists/pages for better readability.  
2. **Personalization through filtering:** schedules can be filtered by course, program/curriculum, and academic year to focus on the relevant subset of events.  
3. **Conflict awareness:** the application detects temporal overlaps between lectures (“conflicts”) and visually highlights them to help students identify clashes in their timetable.  
4. **Calendar interoperability:** users can export their schedule in **ICS format** and subscribe to a **calendar URL feed**, enabling synchronization with external calendar platforms such as Google Calendar, Outlook, and Apple Calendar.
