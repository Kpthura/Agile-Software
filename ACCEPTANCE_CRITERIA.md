# Acceptance Criteria Document
## Finance Expense Tracking App

**Course:** Agile Software Development  
**Document Version:** 1.0  
**Date:** September 12, 2026  
**Status:** Approved Baseline  

---

## 1. Overview & Framework

### 1.1 Purpose
This document defines the formal **Acceptance Criteria (AC)** for all Minimum Viable Product (MVP) features of the **Finance Expense Tracking App**. It serves as the single source of truth for developers, quality assurance (QA) testers, and the Product Owner to determine when a user story meets its Definition of Done (DoD).

### 1.2 Format & Syntax
Acceptance criteria are formatted using both:
- **Given-When-Then (Gherkin BDD)** scenarios for functional behavior and automated test execution.
- **Verification Checklists** for input boundaries, security policies, and UI/UX requirements.

---

## 2. Epic 1: User Registration & Authentication

### User Story US-01: User Registration (Sign Up)
> *As a new user, I want to create an account with my email and password so that I can securely access my personal expense tracking dashboard.*

#### Acceptance Criteria

##### Scenario 1.1: Successful Registration (Happy Path)
- **Given** an unauthenticated visitor is on the Registration page (`/register`),
- **When** they enter an unregistered, valid email address (e.g., `user@example.com`),
- **And** they enter a password satisfying security rules (>= 8 characters with numbers/symbols),
- **And** they enter matching password confirmations and their full name,
- **And** click the "Sign Up" button,
- **Then** a new user record is created in the database with a salted, hashed password,
- **And** an authentication token/session is established,
- **And** the user is redirected to the Dashboard or Onboarding screen with a welcome message.

##### Scenario 1.2: Duplicate Email Rejection
- **Given** a visitor attempts to register,
- **When** they submit an email address already registered in the system,
- **Then** registration is prevented,
- **And** the form remains populated (excluding password fields),
- **And** an error message is displayed: *"An account with this email already exists."*

##### Scenario 1.3: Invalid Email Format
- **Given** a visitor enters an invalid email string (e.g., `user@domain`, `user.com`, or empty),
- **When** they click "Sign Up" or unfocus the input,
- **Then** client-side validation prevents form submission,
- **And** an inline error appears: *"Please enter a valid email address."*

##### Scenario 1.4: Password Complexity Failure
- **Given** a visitor enters a password shorter than 8 characters (e.g., `12345`),
- **When** they submit the form,
- **Then** the form is blocked from submitting,
- **And** an error message states: *"Password must be at least 8 characters long and contain at least one number or special character."*

##### Scenario 1.5: Password Mismatch
- **Given** the password and confirm password inputs do not match,
- **When** the user clicks "Sign Up",
- **Then** an error states: *"Passwords do not match."*, and no network submission is made.

---

### User Story US-02: User Login & Session Management
> *As a registered user, I want to log in securely with my credentials so that I can access my private financial data.*

#### Acceptance Criteria

##### Scenario 2.1: Successful Login (Happy Path)
- **Given** a registered user is on the Login page (`/login`),
- **When** they enter their registered email and correct password,
- **And** click the "Log In" button,
- **Then** their credentials are authenticated against the database hash,
- **And** a secure session (JWT / HTTP-only cookie) is established,
- **And** the user is redirected to the main Dashboard (`/dashboard`).

##### Scenario 2.2: Failed Login (Incorrect Credentials)
- **Given** a user is on the Login page,
- **When** they enter an incorrect password or an email not present in the system,
- **And** click "Log In",
- **Then** authentication fails,
- **And** a generic error is shown: *"Invalid email or password."* (Preventing username enumeration),
- **And** the password field is cleared.

##### Scenario 2.3: Unauthenticated Route Protection
- **Given** an unauthenticated visitor,
- **When** they attempt to navigate directly to protected routes (e.g., `/dashboard`, `/profile`),
- **Then** the application redirects them immediately to `/login`,
- **And** displays an informative notice: *"Please log in to continue."*

##### Scenario 2.4: Session Persistence
- **Given** an authenticated user is on any protected page,
- **When** they refresh the browser window or close and reopen the tab within token validity period,
- **Then** the authenticated session remains active without requesting re-login.

##### Scenario 2.5: User Logout
- **Given** an authenticated user,
- **When** they click the "Log Out" button in the navigation header,
- **Then** the active session token is cleared from the client storage/cookie,
- **And** the user is redirected to `/login`,
- **And** clicking browser "Back" does not reveal private financial records or permit authenticated actions.

---

## 3. Epic 2: User Profile & Financial Preferences

### User Story US-03: Set Financial Preferences (Income & Budget)
> *As a user, I want to configure my monthly income and target monthly budget so that I have clear benchmark limits for my spending.*

#### Acceptance Criteria

##### Scenario 3.1: Configure Monthly Income and Budget
- **Given** an authenticated user is on the Profile / Preferences settings view,
- **When** they input valid numerical values for:
  - Monthly Expected Income (e.g., `3500.00`)
  - Target Monthly Budget (e.g., `2000.00`),
- **And** click "Save Preferences",
- **Then** the values are saved to the user's account profile in the database,
- **And** a success notification appears: *"Financial preferences updated successfully."*,
- **And** the Dashboard budget indicators reflect the updated budget limit immediately.

##### Scenario 3.2: Negative or Non-Numeric Value Rejection
- **Given** a user enters negative numbers (e.g., `-500`) or non-numeric characters (e.g., `abc`),
- **When** they attempt to save preferences,
- **Then** form validation blocks submission,
- **And** an error message is displayed: *"Value must be a positive number."*

##### Scenario 3.3: Decimal Precision Handling
- **Given** a user enters values with decimals,
- **When** the values have more than 2 decimal places (e.g., `1200.559`),
- **Then** the input automatically rounds or limits to two decimal places (`1200.56`).

---

### User Story US-04: View & Edit Personal Information
> *As a user, I want to view and edit my personal profile details so that my account remains accurate and my password can be updated.*

#### Acceptance Criteria

##### Scenario 4.1: View Profile Details
- **Given** an authenticated user navigates to `/profile`,
- **Then** the page displays:
  - User's Full Name
  - Email Address
  - Current Monthly Income
  - Current Monthly Budget
  - Account Creation Date

##### Scenario 4.2: Edit Profile Details
- **Given** a user modifies their Full Name or Email on the profile screen,
- **When** they click "Update Profile",
- **Then** the updated values are persisted,
- **And** a confirmation message is displayed: *"Profile details updated."*

##### Scenario 4.3: Password Change Flow (Happy Path)
- **Given** a user is on the Security / Change Password section of their profile,
- **When** they input their current password correctly,
- **And** enter a new compliant password and matching confirmation,
- **And** click "Change Password",
- **Then** the password hash is updated in the database,
- **And** a success toast appears: *"Password changed successfully."*

##### Scenario 4.4: Password Change with Incorrect Current Password
- **Given** a user enters an incorrect current password,
- **When** they submit the change request,
- **Then** the change is rejected,
- **And** an error displays: *"Current password is incorrect."*

---

## 4. Epic 3: Expense Tracking Engine

### User Story US-05: Manual Expense Entry
> *As a user, I want to add an expense manually with amount, date, description, and category so that I keep an accurate log of my spending.*

#### Acceptance Criteria

##### Scenario 5.1: Successful Expense Creation (Happy Path)
- **Given** an authenticated user opens the "Add Expense" form/modal,
- **When** they provide:
  - **Amount:** A positive number (e.g., `45.50`)
  - **Date:** A valid date (defaults to current date `YYYY-MM-DD`)
  - **Category:** Selected from standard options (e.g., `Food & Dining`, `Transport`, `Groceries`, `Utilities`, `Entertainment`, `Healthcare`, `Miscellaneous`)
  - **Description:** Text memo (e.g., `Lunch with team`)
- **And** click "Save Expense",
- **Then** the transaction is stored with `user_id` bound to the authenticated user,
- **And** the modal closes,
- **And** a toast notification displays: *"Expense added successfully."*,
- **And** the transaction immediately appears at the top of the Recent Transactions list,
- **And** the Total Spent and Remaining Budget counters recalculate instantly.

##### Scenario 5.2: Invalid Amount Validation
- **Given** the user attempts to save an expense,
- **When** the amount is empty, `0.00`, or a negative number,
- **Then** submission is prevented,
- **And** an error states: *"Please enter an amount greater than 0."*

##### Scenario 5.3: Missing Required Fields
- **Given** the user leaves either `Description`, `Category`, or `Date` empty,
- **When** they click "Save Expense",
- **Then** submission is blocked,
- **And** visual highlights flag the missing fields with appropriate guidance (e.g., *"Please select a category."*).

##### Scenario 5.4: Description Length Constraint
- **Given** a user enters a description exceeding 255 characters,
- **When** inputting or submitting,
- **Then** input is truncated or flagged with: *"Description cannot exceed 255 characters."*

---

### User Story US-06: Edit Existing Transaction
> *As a user, I want to edit an existing expense record so that I can correct mistakes or update details.*

#### Acceptance Criteria

##### Scenario 6.1: Pre-populated Edit Form
- **Given** an authenticated user views their Recent Transactions list,
- **When** they click the "Edit" button/icon on a specific transaction row,
- **Then** the Edit Expense modal opens,
- **And** all inputs (`Amount`, `Date`, `Category`, `Description`) are pre-populated with that transaction's current data.

##### Scenario 6.2: Successful Update & Recalculation
- **Given** an open edit form with existing transaction values,
- **When** the user changes the Amount from `$20.00` to `$35.00` and modifies the description,
- **And** clicks "Update Expense",
- **Then** the record updates in the database,
- **And** the updated details appear in the transaction row,
- **And** the Total Spent card increases by `$15.00`, and Remaining Budget decreases accordingly,
- **And** a confirmation message displays: *"Expense updated successfully."*

##### Scenario 6.3: Edit Cancellation
- **Given** an open edit form,
- **When** the user clicks "Cancel" or closes the modal without submitting,
- **Then** no changes are saved,
- **And** the transaction values in the list remain unaltered.

##### Scenario 6.4: Data Isolation Security Check
- **Given** an authenticated User A,
- **When** an API request is made to update an expense belonging to User B (`PUT /api/expenses/{userB_expenseId}`),
- **Then** the server responds with HTTP `403 Forbidden` or `404 Not Found`,
- **And** the record is not modified.

---

### User Story US-07: Delete Existing Transaction
> *As a user, I want to delete an expense record with a confirmation prompt so that I can remove errors without accidental data loss.*

#### Acceptance Criteria

##### Scenario 7.1: Deletion Confirmation Prompt
- **Given** an authenticated user on the transaction list,
- **When** they click the "Delete" icon on an expense,
- **Then** a confirmation dialog appears with the message:
  *"Are you sure you want to delete this expense? This action cannot be undone."*,
- **And** displays two options: "Cancel" and "Confirm Delete".

##### Scenario 7.2: Confirmed Deletion
- **Given** the confirmation dialog is displayed,
- **When** the user clicks "Confirm Delete",
- **Then** the transaction is removed from the database,
- **And** the transaction row disappears from the Recent Transactions list,
- **And** the Total Spent and Remaining Budget counters recalculate immediately,
- **And** a confirmation toast appears: *"Expense deleted."*

##### Scenario 7.3: Cancel Deletion
- **Given** the confirmation dialog is displayed,
- **When** the user clicks "Cancel" or clicks outside the modal,
- **Then** the dialog closes,
- **And** the transaction remains intact in the list and database.

---

### User Story US-08: Recent Transactions Feed & Dashboard Summary
> *As a user, I want to view a chronological feed of recent expenses and summary cards so that I have an immediate pulse on my financial status.*

#### Acceptance Criteria

##### Scenario 8.1: Chronological Ordering
- **Given** an authenticated user with logged transactions,
- **When** they view the Dashboard,
- **Then** transactions are listed in descending chronological order (most recent transaction date at top),
- **And** transactions on the same date are ordered by `created_at` timestamp descending.

##### Scenario 8.2: Transaction Display Content
- **Given** transactions exist in the list,
- **Then** each item displays:
  - **Category Badge:** Category name with distinct icon or color badge.
  - **Description:** Memo text clearly readable.
  - **Date:** Formatted user-friendly string (e.g., `Sep 12, 2026`).
  - **Amount:** Formatted with currency symbol (e.g., `$45.00`).
  - **Actions:** Visible and clickable `Edit` and `Delete` action triggers.

##### Scenario 8.3: Empty State Handling
- **Given** a new user or a user with zero recorded expenses,
- **When** they view the Dashboard transaction section,
- **Then** an empty-state illustration/message is displayed:
  *"No transactions recorded yet. Click 'Add Expense' above to log your first expenditure."*,
- **And** the Total Spent indicator reads `$0.00`.

##### Scenario 8.4: Budget Status Indicators
- **Given** a user with a Monthly Budget of `$1,000.00`,
- **When** their total expenses for the month equal `$800.00`,
- **Then** the Summary Card displays:
  - **Total Spent:** `$800.00`
  - **Remaining Budget:** `$200.00` (highlighted in neutral/positive styling, e.g., green or blue).
- **When** their total expenses exceed `$1,000.00` (e.g., `$1,150.00`),
- **Then** the Remaining Budget displays negative (e.g., `-$150.00`),
- **And** a visual warning alert / badge (e.g., red highlight) indicates the budget has been exceeded.

---

## 5. Cross-Cutting & Non-Functional Acceptance Criteria

| ID | Category | Acceptance Criteria Rule |
| :--- | :--- | :--- |
| **AC-NFR-01** | **Security** | Passwords must be hashed with bcrypt (cost >= 10); no plain text secrets stored in database or logs. |
| **AC-NFR-02** | **Authorization** | Every expense query/mutation must strictly enforce tenant isolation (`user_id == session.user_id`). |
| **AC-NFR-03** | **Input Sanitization** | All inputs (descriptions, names, emails) must be sanitized against XSS attacks before rendering in DOM. |
| **AC-NFR-04** | **Responsiveness** | Forms, buttons, and transaction feeds must adapt cleanly without horizontal scrolling on mobile viewports down to 360px width. |
| **AC-NFR-05** | **Performance** | Expense creation and listing must respond within 300ms under standard local network conditions. |

---

## 6. Verification & Quality Sign-Off

| User Story | Verification Method | Status | Sign-off Date |
| :--- | :--- | :--- | :--- |
| **US-01 (Sign Up)** | Automated E2E & Form Unit Tests | Pending QA | — |
| **US-02 (Login/Logout)** | Security Tests & Auth Token Checks | Pending QA | — |
| **US-03 (Budget Settings)** | Unit Calculation & Persistence Tests | Pending QA | — |
| **US-04 (Profile Edit)** | Profile Form Validation Tests | Pending QA | — |
| **US-05 (Add Expense)** | Functional E2E & Boundary Tests | Pending QA | — |
| **US-06 (Edit Expense)** | State & Recalculation Verification | Pending QA | — |
| **US-07 (Delete Expense)** | Modal Confirmation & Deletion Verification | Pending QA | — |
| **US-08 (Recent Feed)** | Sorting, Rendering & Empty State Tests | Pending QA | — |
