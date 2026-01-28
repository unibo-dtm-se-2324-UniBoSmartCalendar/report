---
title: Home
layout: home
has_children: false
nav_order: 1
---

# UniBo Smart Calendar

### Authors
- [Alessandro De Faveri](mailto:alessandro.defaveri2@studio.unibo.it)
- [Simone Mastria](mailto:simone.mastria@studio.unibo.it)
- [Giulia Rizzo](mailto:giulia.rizzo9@studio.unibo.it)

## Abstract

UniBo Smart Calendar is a web-based calendar application designed for University of Bologna students to solve the problem of fragmented and difficult-to-manage academic schedules. Unlike the standard university portal, which often forces students to consult multiple pages and formats, the system aggregates multiple course lectures into a single, user-friendly interface. Starting from UniBo’s official scheduling information, the application retrieves and processes academic calendars by intercepting requests and downloading the original university JSON data, then parsing and normalizing it into clean and consistent structures.
 
A core contribution of the project is a conflict detection engine, based on a proprietary overlap-identification algorithm that automatically detects temporal collisions between lectures and visually flags them to the user. This enables students to quickly identify problematic timetable configurations and to support decision-making when selecting courses or curricular options. In addition, the system provides a smart parsing backend that cleans raw data and computes useful metadata, and a local caching mechanism that improves performance and ensures fast access even under limited connectivity conditions.
 
The platform supports cross-platform interoperability through calendar export in ICS format and full calendar subscription via URL, allowing seamless synchronization with external services such as Google Calendar, Outlook, and Apple Calendar. The project follows a monorepo architecture built on a modern JavaScript stack: a React 18 frontend (Material UI v5, React Big Calendar) and a Node.js/Express backend handling proxying and parsing logic. Quality assurance is addressed through unit and integration testing with Vitest and React Testing Library, while CI/CD automation is implemented via GitHub Actions. Development was conducted using Windsurf Code Editor with coding assistance from Claude 3.5 Sonnet, under continuous supervision by the team. UniBo Smart Calendar was developed for the Software Engineering course by Alessandro De Faveri (Backend & Logic), Simone Mastria (DevOps & QA), and Giulia Rizzo (Frontend & UI/UX), and is distributed under the MIT License.
