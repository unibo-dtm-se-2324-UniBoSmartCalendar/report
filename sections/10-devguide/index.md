---
title: Developer guide
has_children: false
nav_order: 11
---

# Developer Guide


This section describes the procedures and conventions required for a new team member to quickly integrate into the project and start contributing consistently.

## **10.1 Organizational Information**

Collaboration is based on transparency and systematic use of tracking tools.

**Contacts**:

The reference team consists of Alessandro De Faveri (Backend), Simone Mastria (DevOps), and Giulia Rizzo (Frontend).

**Issue Reporting**:

For every identified bug or proposed new feature, opening a GitHub Issue is mandatory. The project uses issues to track progress and to link commits to specific requests (e.g., #1, #2, #4).

**Communication**:

Architectural decisions are documented in the `README.md` and `CHANGELOG.md` to maintain a history of changes.

## **10.2 Internal Conventions**

The team follows strict standards to ensure code readability and maintainability.

**Coding Style**:

JavaScript/React: CamelCase is used for functions and variables, while PascalCase is used for React components (e.g., `ScheduleContainer.jsx`).

Naming: File names reflect their purpose (e.g., `conflictUtils.js` for computation logic, `api.js` for network services).

**Commit Conventions**:

The use of Conventional Commits (e.g., `feat`:, `fix`:, `chore`:) is mandatory. This practice is essential for automatic changelog generation and semantic versioning.

## **10.3 Development Environment**

The environment is configured to be ready to use within a few minutes.

**Prerequisites**:

`Node.js` is required (version 18.x or more is strongly recommended as specified in `package.json`) along with npm (v9+).

**Initial Setup**:

Clone the repository.

Run `npm install` in the root directory to install frontend, backend, and development tool dependencies (such as `concurrently` and `vitest`).

**Execution**:

The `npm start` command simultaneously launches the React client (port 3000) and the Express server (port 3001) using the concurrently package.

**Testing**:

To validate changes, run `npm test`. The system uses Vitest to execute unit and integration tests (e.g., `conflictUtils.test.js`).

## **10.4 Workflow**

The project follows a workflow based on feature branches and continuous integration.

**Branching Strategy**:

Direct work on the main branch is not allowed. For each task, a dedicated branch is created (e.g., `feature/feature-name` or `fix/bug-name`).

**Pull Request (PR)**:

Once the work is completed, a PR is opened against main.

**Continuous Integration**:

Every push or PR automatically triggers a GitHub Actions pipeline (defined in `ci.yml`). The pipeline runs tests and verifies that the build bundle is generated correctly before allowing the merge.

## **10.5 Development Tools**

**IDE**:

The use of Visual Studio Code is recommended.

**Command Line**:

Most operations (build, test, deploy) are centralized in npm scripts defined in `package.json` to minimize human error.

**Browser DevTools**:

The use of React Developer Tools is essential for debugging React components.
