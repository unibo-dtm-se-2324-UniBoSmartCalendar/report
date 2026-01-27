---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

This section describes the strategy and operational procedures adopted to make the **UniBo Smart Calendar** application accessible to both end-users and developers. The project utilizes a dual-deployment strategy to support both a robust cloud-native production environment and a flexible local development workflow.

## Deployment Strategy

The application follows a modern web architecture based on a JavaScript/Node.js stack. To ensure scalability and ease of management, the deployment is structured into two main approaches:

1.  **Cloud Deployment (Production):** Utilization of the **Vercel** platform for automatic provisioning of the frontend and serverless APIs.
2.  **Local Deployment (Development/Testing):** Configuration of a local Node.js environment for testing, debugging, and feature development.

## Cloud Deployment: Vercel

The production version of UniBo Smart Calendar is hosted on [Vercel](https://vercel.com). This platform was selected for its seamless integration with the GitHub workflow and its native support for **Serverless Functions**, which are critical for handling the backend proxy logic and calendar parsing without requiring a dedicated server infrastructure.

### Configuration
The repository includes a `vercel.json` configuration file that instructs the platform on how to handle routing and build outputs:
-   **Frontend:** The React application is compiled via `npm run build` and served as optimized static content.
-   **Backend API:** Requests targeting `/api/*` are routed to the Node.js functions located in the `api/` directory. This serverless architecture effectively resolves CORS issues when fetching data from external university calendar endpoints.

The production application is accessible at: [https://unibosmartcalendar.vercel.app](https://unibosmartcalendar.vercel.app)

## Local Deployment

To run the artifact locally, developers must have **Node.js (v18+)** and **npm (v9+)** installed. The project's structure allows for the management of both client and server logic with a unified set of commands.

### Installation Procedure
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/unibo-dtm-se-2324-UniBoSmartCalendar/artifact.git](https://github.com/unibo-dtm-se-2324-UniBoSmartCalendar/artifact.git)
    cd artifact
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```
    *This command recursively installs all necessary packages for both the React frontend and the Express backend/serverless handlers.*

### Execution
The application can be launched in development mode using the following command:
```bash
npm start
