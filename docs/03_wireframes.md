# UI/UX Wireframes & Interface Specifications
**Project:** Internal IT Helpdesk Ticketing System

This document outlines the low-fidelity layout and functional UI components for the core screens of the Phase 1 MVP.

## 1. Requester Dashboard (My Tickets View)
**Purpose:** Allow employees to view their active and past requests at a glance.

### Layout Specification
* **Top Navigation Bar:** `[ Company Logo ]` | `Home` | `Create New Ticket` | `[ Profile Dropdown (SSO User) ]`
* **Main Content Area:**
  * **Summary Metrics:** `[ Open Tickets: 2 ]`  `[ Resolved: 5 ]`
  * **Data Grid / Ticket List:**

| Ticket ID | Title | Category | Status | Priority | Last Updated | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| IT-1042 | Mouse not working | Hardware | In Progress | Low (P4) | 2 hours ago | [ View ] |
| IT-1041 | VPN Access Denied | Access | Resolved | High (P2) | 1 day ago | [ Verify Fix ] |

## 2. Ticket Creation Form
**Purpose:** Standardized input for capturing necessary information to properly route and resolve issues.

### Form Elements & Validation
* **Requester Name:** `[ Auto-filled via SSO ]` *(State: Read-only)*
* **Issue Title:** `[ Single-line Text Input ]` *(Validation: Mandatory, Max 100 characters)*
* **Category:** `[ Dropdown Menu ]` *(Options: Hardware, Software, Network, Access)*
* **Urgency:** `[ Radio Buttons ]` *(Options: Low, Medium, High, Critical)*
* **Description:** `[ Rich Text Area ]` *(Placeholder: Please describe the issue, steps to reproduce, and any error codes).*
* **Attachments:** `[ Drag & Drop File Zone ]` *(Validation: PNG, JPG, PDF only. Max 5MB per file).*
* **Action Buttons:** `[ Cancel ]` (Routes back to Dashboard) | `[ Submit Ticket ]` (Triggers validation and backend creation).

## 3. Ticket Detail Page (Agent View)
**Purpose:** The workspace for IT Agents to resolve issues and update statuses.

### Layout Specification
* **Left Column (Ticket Info):**
  * Ticket Title & ID
  * Original Description
  * Attachment links
* **Right Column (Metadata & Actions):**
  * Assignee: `[ Dropdown (List of IT Agents) ]`
  * Status: `[ Dropdown (Follows State Machine Rules) ]`
  * Priority: `[ Dropdown ]`
* **Bottom Section (Communication Thread):**
  * Tab 1: `Public Replies` (Visible to requester)
  * Tab 2: `Internal Notes` (Highlighted in yellow, visible only to IT)
  * `[ Text Area for Reply ]`
  * `[ Send Button ]`