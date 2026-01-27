---
title: CI/CD
has_children: false
nav_order: 9
---

# CI/CD

# 08. Continuous Integration & Continuous Delivery (CI/CD)

This section provides a conceptual and technical detailed description of the CI/CD workflow adopted for **UniBo Smart Calendar**. The pipeline is designed to automate the verification and delivery processes, ensuring that the software remains in a deployable state at all times.

## 8.1. Conceptual Workflow

The CI/CD pipeline serves as the backbone of our quality assurance strategy. It bridges the gap between development (writing code) and operations (running the application).

### What is Automated?
The automation covers four distinct stages of the software lifecycle:
1.  **Dependency Resolution:** Ensuring the project runs with the exact library versions specified.
2.  **Static Analysis:** Checking code style and syntax without executing the program.
3.  **Dynamic Verification:** executing the test suite to validate logic and behavior.
4.  **Deployment:** Promoting the validated code to the production environment.

### Why Automation?
We implemented this rigorous automation for several strategic reasons:
* **Consistency:** It eliminates the "it works on my machine" problem by running verification in a neutral, clean environment every time.
* **Speed & Feedback:** Developers receive immediate feedback on their commits. If a test fails, they know within minutes, preventing bugs from compounding.
* **Confidence:** The `main` branch is protected. We can deploy to production at any moment knowing that the codebase has passed all quality gates.

## 8.2. CI Implementation: GitHub Actions Exploitation

The Continuous Integration logic is implemented using **GitHub Actions**. The workflow is defined in the `.github/workflows/main.yml` file, leveraging the platform's ability to spin up ephemeral virtual machines (runners).

### 8.2.1. Workflow Triggers
To balance resource usage with code safety, the pipeline is triggered on:
* **Push Events:** Specifically to the `main` branch.
* **Pull Requests:** Opened against the `main` branch. This ensures that no code enters the stable codebase without passing inspection.

### 8.2.2. Implementation Details
The workflow exploits several specific GitHub Actions capabilities to optimize performance and reliability:

1.  **Deterministic Environment (`npm ci`):**
    Instead of the standard `npm install`, the pipeline uses `npm ci` (Clean Install). This command relies strictly on the `package-lock.json` file, ensuring that the CI runner uses the exact same dependency tree as the local developer environment, preventing version mismatch errors.

2.  **Parallel Execution & Caching:**
    The workflow is designed to minimize wait times. Although the current setup runs sequentially to fail fast, we exploit **dependency caching**. The `actions/setup-node` action is configured to cache the `~/.npm` directory. This significantly reduces build time on subsequent runs by avoiding the need to re-download unchanged packages.

3.  **The "Test & Build" Job Matrix:**
    The core job executes the following sequence:
    * **Linting:** Runs `npm run lint` (ESLint) and `npm run format:check` (Prettier) to enforce code style.
    * **Testing:** Runs `npm run test` (Vitest). If any assertion fails, the process exits with a non-zero status code, halting the pipeline.
    * **Build Dry-Run:** Runs `npm run build` (Vite). This is crucial for verifying that the application builds successfully without memory errors or missing assets, even if the tests pass.



graph TD
    %% Nodes
    User([Developer])
    Repo[GitHub Repository]
    
    subgraph CI [CI: GitHub Actions]
        direction TB
        Install[📦 npm ci]
        Lint[🎨 Lint & Format]
        Test[🧪 Unit Tests]
        Build[🏗️ Build Verification]
    end
    
    subgraph CD [CD: Vercel]
        direction TB
        Preview[🚀 Preview Deployment]
        Prod[🌍 Production Deployment]
    end

    %% Flow
    User -->|Push / PR| Repo
    Repo --> Install
    Install --> Lint
    Lint --> Test
    Test --> Build
    
    %% Logic Split
    Build -->|Pull Request| Preview
    Build -->|Merge to Main| Prod

    %% Styling (Optional - for standard rendering)
    classDef ci fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef cd fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px;
    class Install,Lint,Test,Build ci;
    class Preview,Prod cd;


## 8.3. CD Implementation: Vercel Integration

While GitHub Actions handles the *Integration* (verification), **Vercel** handles the *Delivery* (deployment).

* **Preview Deployments:** Upon opening a Pull Request, Vercel automatically builds the branch and assigns it a unique URL. This provides a tangible "preview" of the feature for manual validation.
* **Production Deployment:** When the CI pipeline passes and code is merged into `main`, Vercel detects the change and triggers a production build. This updates the public-facing application with zero downtime, completing the automated lifecycle.