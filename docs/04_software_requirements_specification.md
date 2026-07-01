# Software Requirements Specification (SRS)
**Project:** Internal IT Helpdesk Ticketing System  

## 1. Introduction
While the Product Requirements Document (PRD) outlines user stories and business logic, this SRS details the technical constraints, system interfaces, and data structures required for the engineering team to build the MVP.

## 2. Data Dictionary
Detailed specification of the core `TICKET` entity stored in the database.

| Field Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `ticket_id` | VARCHAR(20) | Primary Key, Auto-generate | Format: `IT-XXXX` (e.g., IT-1042). |
| `title` | VARCHAR(100)| Not Null | Short summary of the reported issue. |
| `description` | TEXT | Not Null | Detailed explanation of the issue. |
| `status` | VARCHAR(20) | Not Null, Default: 'New' | Enum: `New`, `Assigned`, `InProgress`, `Pending`, `Resolved`, `Closed`. |
| `priority` | VARCHAR(10) | Not Null, Default: 'P4' | Enum: `P1`, `P2`, `P3`, `P4`. |
| `requester_id`| VARCHAR(50) | Foreign Key, Not Null | Links to `USER.user_id`. |
| `assignee_id` | VARCHAR(50) | Foreign Key, Nullable | Links to `USER.user_id` (IT Agent). Null if status is 'New'. |
| `created_at` | TIMESTAMP | Not Null | System-generated timestamp (UTC). |

## 3. System Interfaces & API Specifications
The system will expose internal RESTful APIs for frontend communication. Below are the core endpoints.

### 3.1. Create a New Ticket
* **Endpoint:** `POST /api/v1/tickets`
* **Authorization:** Bearer Token (JWT - Any logged-in user)
* **Request Payload (JSON):**
  ```json
  {
    "title": "Cannot access VPN",
    "category": "Access",
    "priority": "P2",
    "description": "Getting error code 403 when connecting to SG server."
  }
  ```
* **Response (201 Created):** Returns the generated `ticket_id` and timestamp.

### 3.2. Update Ticket Status
* **Endpoint:** `PATCH /api/v1/tickets/{ticket_id}/status`
* **Authorization:** Bearer Token (IT Agent or Admin Role Required)
* **Request Payload (JSON):**
  ```json
  {
    "status": "Resolved",
    "resolution_note": "Reset user password in Active Directory."
  }
  ```
* **Response (200 OK):** Updates the database and triggers a notification to the requester.

## 4. Technical & Security Requirements
* **Environment:** Web-based, optimized for desktop browsers (Chrome, Edge, Firefox).
* **Database:** PostgreSQL 15.x.
* **Authentication:** Single Sign-On (SSO) integration with corporate Azure Active Directory (OAuth 2.0).
* **Data Security:** All data at rest must be encrypted using AES-256. API payloads must transmit over HTTPS (TLS 1.2+).