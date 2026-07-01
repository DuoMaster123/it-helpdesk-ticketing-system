# Product Requirements Document (PRD)
**Project:** Internal IT Helpdesk Ticketing System  
**Document Version:** 1.0  
**Date:** July 2026  

## 1. Business Rules & Logic

### 1.1 Priority & SLA (Service Level Agreement) Matrix
Ticket priority is determined by a combination of **Urgency** (how quickly the business needs a fix) and **Impact** (how many users or critical systems are affected). 

| Priority Level | Response Time SLA | Resolution Time SLA | Example Scenario |
| :--- | :--- | :--- | :--- |
| **Critical (P1)** | 15 Minutes | 2 Hours | Entire office network down; Server crash. |
| **High (P2)** | 1 Hour | 8 Hours | VIP user locked out; Key financial software glitch. |
| **Medium (P3)** | 4 Hours | 24 Hours | Printer malfunction; Single user software bug. |
| **Low (P4)** | 8 Hours | 48 Hours | Request for a new mouse; Non-urgent software installation. |

### 1.2 Ticket Status Workflow (State Machine)
Every ticket must follow a strict lifecycle. The allowed status transitions are:
1. **New:** Ticket is created by the requester. Unassigned.
2. **Assigned:** IT Manager or automatic routing assigns the ticket to a specific IT Agent.
3. **In Progress:** The IT Agent has started investigating or working on the issue.
4. **Pending Requester:** Agent needs more information from the requester (SLA timer pauses).
5. **Resolved:** Agent has fixed the issue. Requester must verify.
6. **Closed:** Requester confirms the fix, or the system auto-closes after 3 days of being 'Resolved'.

---

## 2. Product Backlog (Epics & User Stories)

### Epic 1: Ticket Creation and Tracking (Requester)

**User Story 1.1: Submit a new ticket**
> **As an** Employee,  
> **I want to** submit a support ticket via a web form,  
> **So that** I can formally request IT assistance.

* **Acceptance Criteria:**
  * The form must include mandatory fields: Title, Category (Hardware, Software, Network, Access), Urgency, and Description.
  * Users can upload attachments (PNG, JPG, PDF up to 5MB).
  * Upon successful submission, the system generates a unique Ticket ID (e.g., `IT-1042`).

**User Story 1.2: View ticket status**
> **As an** Employee,  
> **I want to** view a list of my submitted tickets and their current statuses,  
> **So that** I know if my issue is being worked on.

* **Acceptance Criteria:**
  * The "My Tickets" dashboard displays columns: Ticket ID, Title, Date Created, Status, and Priority.
  * The default view sorts tickets by Date Created (newest first).

### Epic 2: Ticket Management and Resolution (IT Agent)

**User Story 2.1: Update ticket status**
> **As an** IT Agent,  
> **I want to** change the status of a ticket,  
> **So that** the requester and my manager know the current progress.

* **Acceptance Criteria:**
  * An Agent can only transition statuses according to the defined Workflow (e.g., cannot jump from 'New' directly to 'Closed').
  * When changing status to 'Resolved', the Agent must input a mandatory "Resolution Note".

**User Story 2.2: Internal comments**
> **As an** IT Agent,  
> **I want to** add internal, private notes to a ticket,  
> **So that** I can collaborate with other IT staff without notifying the requester.

* **Acceptance Criteria:**
  * Comments have a toggle: "Public Reply" (visible to requester) or "Internal Note" (visible only to IT roles).
  * Internal notes are highlighted with a distinct background color (e.g., light yellow).

### Epic 3: System Administration & Reporting (IT Manager)

**User Story 3.1: SLA Breach Dashboard**
> **As an** IT Manager,  
> **I want to** view a dashboard highlighting tickets that have breached their SLAs,  
> **So that** I can intervene and reallocate resources immediately.

* **Acceptance Criteria:**
  * The dashboard includes a specific widget showing "Breached Tickets" marked in red.
  * Hovering over a breached ticket displays the overdue time (e.g., "-2 Hours").

---

## 3. Non-Functional Requirements (NFRs)
* **Performance:** The web pages must load within 2 seconds under normal conditions (up to 500 concurrent users).
* **Security:** Role-Based Access Control (RBAC) must be strictly enforced. Requesters cannot view tickets created by other employees.
* **Auditability:** Every action on a ticket (status change, assignment, comment) must be logged in a read-only "Ticket History" trail with a timestamp and user ID.