---
title: Release
has_children: false
nav_order: 7
---

# Release

---

### 6.1 Artifact Production and Distribution

The UniBo Smart Calendar project produces artifacts ready for the production environment through a structured pipeline.

**Produced Artifacts:**
The main artifact is the application Build Bundle. It includes the frontend static files (optimized through the React build process) and the Node.js server configured for execution.

**Release Repositories:**

* **GitHub:** Acts as the central repository for the source code and for the formal distribution of versions through Git tags and GitHub Releases.
* **Vercel:** Chosen for hosting and Continuous Deployment. Every update on the main branch is automatically transformed into a deployed online artifact.

**Release Mode:**
Releases occur automatically. The CI pipeline (GitHub Actions) validates the code and, upon success, Vercel builds and publishes the final artifact.

**Build Commands:**
Local generation of the artifact is performed using the `npm run build` command, as defined in the main configuration file.

---

### 6.2 License Selection

Following the course guidelines on intellectual property and open-source software management, the legal strategy of the project was defined.

**Chosen License:**
The code and artifacts are distributed under the MIT License.

**Technical and Legal Rationale:**

* **Permissive Nature:** Unlike copyleft licenses (such as the GPL), the MIT license is permissive. This option was chosen to ensure maximum freedom for code reuse in academic contexts, requiring only the preservation of the original copyright notice.
* **Compatibility:** The MIT license is compatible with almost all third-party libraries used in the project (such as React and MUI), facilitating integration without legal conflicts.
* **Simplicity:** Being a short and clear license, it is well suited to a university project managed by a small team, reducing administrative overhead in contribution management.

---

### 6.3 Versioning Scheme

The project adopts a rigorous versioning methodology to ensure change traceability.

**Adopted Scheme:**
Semantic Versioning (SemVer) using the MAJOR.MINOR.PATCH format.

**Increment Logic:**

* **PATCH:** For backward-compatible bug fixes (e.g., fixes in UniBo data parsing).
* **MINOR:** For new features (e.g., addition of the statistics dashboard or the test suite).
* **MAJOR:** For structural changes that break compatibility (e.g., radical migration of the server architecture).

**Artifact Alignment:**
Frontend and backend share the same version number in the `package.json`. This ensures that the entire system is treated as a single atomic artifact, simplifying deployment and debugging.

**New Version Creation:**

* **Changelog:** Update of the `CHANGELOG.md` file with the implemented changes.
* **Tagging:** Creation of a Git tag (e.g., v1.0.0) that uniquely identifies the source code state.
* **GitHub Release:** Formal publication on GitHub, which automatically triggers the distribution process to Vercel.



