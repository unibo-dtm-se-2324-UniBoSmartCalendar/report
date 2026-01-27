---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

# 07. Deployment

This section details the deployment architecture and operational procedures designed for **UniBo Smart Calendar**. The project adopts a modern web deployment strategy, utilizing a cloud-native approach for production to ensure high availability, while maintaining a flexible container-free environment for local development.

## 7.1. Deployment Strategy

The application is built on a JavaScript/Node.js stack. To maximize scalability and minimize infrastructure management overhead, the deployment strategy is bifurcated:

1.  **Production Environment (Cloud):** Hosted on **Vercel**, leveraging its global CDN for the frontend and Serverless Functions for the backend.
2.  **Development Environment (Local):** A local Node.js setup that allows developers to emulate the production environment, run tests, and debug logic in real-time.

## 7.2. Cloud Deployment: Vercel

The production artifact is deployed to [Vercel](https://vercel.com). This platform was chosen for its native integration with the Git workflow and its specialized support for the project's architecture, effectively treating the frontend and backend as a unified entity during deployment.

### 7.2.1. Serverless Architecture
Unlike traditional VPS deployment, the backend logic (specifically the calendar parsing and proxy services) is deployed as **Serverless Functions**.
-   **Routing:** All requests sent to the `/api/*` endpoint are intercepted by Vercel's Edge Network and routed to the corresponding Node.js functions located in the `api/` directory of the repository.
-   **Benefits:** This approach eliminates the need to manage server uptime or scaling. Resources are allocated dynamically based on traffic demand.

### 7.2.2. Configuration (`vercel.json`)
The repository includes a strict configuration file, `vercel.json`, which governs the build and runtime behavior:
-   **Rewrites:** It configures URL rewrites to map API calls to the serverless handlers.
-   **CORS Policy:** It explicitly handles Cross-Origin Resource Sharing headers to allow the frontend to securely communicate with the backend proxy.

**Production URL:** [https://unibosmartcalendar.vercel.app](https://unibosmartcalendar.vercel.app)

## 7.3. Local Deployment

For development and artifact verification, the project is designed to run locally using the **Node.js** runtime. The repository follows a structure where both the client (React) and the server (Express/Node) are managed via a single `package.json`.

### 7.3.1. Prerequisites
-   **Node.js:** Version 18.x or higher (LTS recommended).
-   **npm:** Version 9.x or higher.
-   **Git:** For version control operations.

### 7.3.2. Installation Procedure
To set up the artifact locally, follow these steps:

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/unibo-dtm-se-2324-UniBoSmartCalendar/artifact.git](https://github.com/unibo-dtm-se-2324-UniBoSmartCalendar/artifact.git)
    cd artifact
    ```

2.  **Install Dependencies:**
    ```bash
    npm install
    ```
    *This command reads the `package.json` file and installs all required libraries for both the frontend (e.g., React, Vite) and the backend (e.g., ical-generator, axios).*

3.  **Environment Configuration:**
    Create a `.env` file in the root directory by copying the provided template:
    ```bash
    cp .env.example .env
    ```
    *Edit the new `.env` file to configure any necessary API keys or port settings (default: 3000).*

### 7.3.3. Execution
To launch the application in development mode:
```bash
npm start
```

This command triggers a concurrent script that launches:

The Frontend: Accessible via http://localhost:3000 (served via Vite).

The Backend API: Accessible via http://localhost:3001 (or the configured API port).

The environment supports Hot Module Replacement (HMR), meaning changes to the source code are immediately reflected in the browser without a full page reload.