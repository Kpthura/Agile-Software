# Project Charter: Finance Expense Tracking App

**Course:** Agile Software Development  
**Document Version:** 1.0  
**Date:** September 12, 2026  
**Status:** Approved / Active Baseline  

---

## 1. Project Overview & Objectives

### 1.1 Executive Summary
The **Finance Expense Tracking App** is a lightweight, intuitive personal finance management application designed to help individuals monitor, categorize, and control their personal expenditures. Developed within an Agile framework, the project delivers rapid increments, prioritizing core user needs around tracking money flow, budgeting, and financial habit awareness.

### 1.2 Problem Statement
Many individuals struggle with personal financial management and overspending due to a lack of clear visibility into their daily cash flow. Commercial solutions are frequently overloaded with intrusive advertisements, paid subscriptions, or overly complex investment modules. Users need an accessible, streamlined, and secure tool to log expenses quickly, establish baseline budgets, and review spending trends without friction.

### 1.3 Project Purpose & Strategic Goals
- **Empower Users:** Provide full transparency into daily spending patterns and habits.
- **Frictionless Entry:** Allow users to record an expense quickly with minimal inputs required.
- **Budget Discipline:** Enable users to set monthly income and budget baselines to prevent overspending.
- **Iterative Agile Delivery:** Deliver a dependable Minimum Viable Product (MVP) through iterative sprint releases.

---

## 2. Project Scope

### 2.1 In-Scope: Minimum Viable Product (MVP) Features

#### A. User Registration & Profile Management
- **Secure Authentication:**
  - Secure user sign-up with email and password.
  - Secure login/logout using industry-standard password encryption and session/token validation.
- **Financial Baseline Preferences:**
  - Configuration of basic financial parameters:
    - Expected Monthly Income
    - Target Monthly Budget limit
- **Personal Information Management:**
  - View personal account details.
  - Edit personal profile information (name, email address, password update).

#### B. Expense Tracking Core
- **Manual Expense Logging:**
  - Ability to record transactions with essential attributes:
    - **Amount:** Numerical transaction value with currency validation.
    - **Date:** Transaction date (defaults to current date with custom date picker option).
    - **Description:** Note or memo detailing the purchase.
    - **Category:** Classification tag (e.g., Food & Dining, Transportation, Housing/Utilities, Healthcare, Entertainment, Miscellaneous).
- **Transaction Management (CRUD Operations):**
  - **Edit:** Update amount, date, description, or category on existing records.
  - **Delete:** Remove transactions with confirmation safety prompt.
- **Transaction History & Feed:**
  - Display chronological list of recent transactions.
  - Summary views showing recent spending against total budget.

### 2.2 Out-of-Scope (Deferred to Future Sprints / Releases)
The following capabilities are recognized as future enhancements but excluded from the initial MVP:
- Automated bank feed integration (e.g., Open Banking / Plaid APIs).
- Receipt image capture and OCR parsing.
- Multi-currency support and live foreign exchange rate conversions.
- Recurring automated subscription detection.
- Shared / collaborative wallets and bill splitting.
- Export options to external formats (CSV, Excel, PDF).

---

## 3. Stakeholders & Agile Team Roles

| Role | Title / Persona | Responsibilities |
| :--- | :--- | :--- |
| **Product Owner (PO)** | Agile Course Instructor / Project Lead | Defines vision, maintains and prioritizes Product Backlog, accepts user stories upon completion. |
| **Scrum Master** | Agile Facilitator | Facilitates Agile ceremonies (Daily Standup, Sprint Planning, Review, Retrospective), removes blockers. |
| **Development Team** | Full-Stack Software Engineers | Designs system architecture, implements frontend UI, develops backend APIs, writes automated tests. |
| **Target End Users** | Students & Young Professionals | Provide feedback during sprint reviews and validate usability and functionality. |

---

## 4. Agile Roadmap & Sprint Milestones

| Sprint / Phase | Focus Area | Deliverables & Outcomes |
| :--- | :--- | :--- |
| **Sprint 0: Initiation & Setup** | Project Foundation | Project charter, tech stack selection, environment setup, repository initialization, and backlog preparation. |
| **Sprint 1: Auth & Profile** | User Registration & Profile (MVP 1) | Sign up, secure login/logout, user profile view/edit, monthly income and budget configuration. |
| **Sprint 2: Expense Tracking** | Transaction Engine (MVP 2) | Expense entry form (Amount, Date, Description, Category), edit/delete functionality, recent transactions feed. |
| **Sprint 3: Testing & Integration** | Quality Assurance & Hardening | Cross-feature integration, input validation, automated unit and integration tests, usability testing. |
| **Sprint 4: Deployment & Review** | Release & Retrospective | Production/demo deployment, final documentation, sprint review, and project demonstration. |

---

## 5. Success Criteria & Key Performance Indicators (KPIs)

- **Functional MVP Completion:** 100% of defined MVP features implemented and verified against Acceptance Criteria.
- **Usability & Efficiency:** A new user can complete registration and record their first transaction within 2 minutes.
- **Reliability & Responsiveness:** UI response times under 1 second for creating, updating, and viewing transactions.
- **Data Integrity & Security:** Protected user passwords (salted/hashed), authenticated API routes, and accurate arithmetic balance calculations.
- **Agile Adherence:** Sprints executed with documented sprint plans, review sessions, and retrospectives.

---

## 6. Assumptions, Constraints & Dependencies

### 6.1 Assumptions
- Users have access to standard web browsers or modern mobile devices.
- Transactions are entered in a single base currency for the MVP.
- Users perform manual entry consistently.

### 6.2 Constraints
- **Schedule:** Bound by the academic course semester timeline and sprint cadences.
- **Budget:** Relying on open-source software, free tiers for database, and cloud hosting.
- **Scope Discipline:** Strict adherence to MVP boundaries to prevent scope creep.

### 6.3 Technical Dependencies
- Frontend framework (e.g., React, Vue, or mobile counterpart).
- Backend service runtime & RESTful API framework (e.g., Node.js/Express, Python/FastAPI, etc.).
- Relational or document database (e.g., PostgreSQL, SQLite, MongoDB).
- Version control system (Git & GitHub).

---

## 7. Risk Assessment & Mitigation Matrix

| Risk | Severity / Likelihood | Mitigation Strategy |
| :--- | :--- | :--- |
| **Scope Creep** (Adding analytics, charts, or bank sync early) | High / Medium | Use MoSCoW prioritization; strictly decline non-MVP user stories until MVP is accepted. |
| **User Drop-off from Tedious Logging** | Medium / High | Design concise, low-click input forms with sensible category defaults and instant confirmation. |
| **Security / Auth Vulnerabilities** | High / Low | Rely on tested, standard authentication libraries (e.g., bcrypt, JWT, OAuth) rather than custom crypto logic. |
| **Sprint Delays / Schedule Slippage** | Medium / Medium | Maintain short daily standups, track sprint velocity, and adjust sprint backlog early if blockers occur. |

---

## 8. Definition of Done (DoD) for MVP User Stories
A user story in the MVP is deemed **Done** when:
1. Acceptance criteria outlined in the user story are fully satisfied.
2. Code is formatted, clean, peer-reviewed, and merged into the main branch.
3. Form validation is active for all input fields (preventing negative values, missing categories, invalid emails).
4. Unit/component tests pass without errors.
5. The feature operates cleanly in both desktop and mobile viewports.
6. Product Owner reviews and formally accepts the increment.

---

## 9. Approvals & Sign-off

| Role | Name | Status | Date |
| :--- | :--- | :--- | :--- |
| **Product Owner** | Project Stakeholder | Approved | September 12, 2026 |
| **Scrum Master** | Agile Facilitator | Approved | September 12, 2026 |
| **Lead Developer** | Technical Lead | Approved | September 12, 2026 |
