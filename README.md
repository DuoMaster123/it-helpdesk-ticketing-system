# Internal IT Helpdesk Ticketing System

## Project Overview
This repository contains the complete Product Management (BA/PM) artifacts for the **Internal IT Helpdesk Ticketing System**. The solution is designed to centralize, track, and streamline internal IT support requests within an organization, replacing inefficient and fragmented communication channels like instant messaging and emails.

## Problem Statement
Employees currently report technical issues (hardware failures, software access, network downtime) via ad-hoc channels (Slack, email, or direct calls). This workflow results in:
* **High Ticket Drop Rate:** Requests are frequently missed or forgotten.
* **Lack of Transparency:** Requesters cannot track the status or progress of their issues.
* **No Performance Metrics:** IT Management lacks data on resolution times, common system bottlenecks, or team workload.

## Proposed Solution
A web-based internal portal where employees can log tickets, track their progress in real-time, and IT agents can systematically manage, prioritize, and resolve issues based on defined Service Level Agreements (SLAs).

## Target Users & Roles
* **Employee (Requester):** Submits tickets, tracks status, and provides feedback upon resolution.
* **IT Support Agent (Assignee):** Reviews, prioritizes, updates, and resolves assigned tickets.
* **IT Manager (Admin):** Monitors team performance via dashboards, manages system configurations, and handles escalation.

## Product Scope (Phase 1 - MVP)
### In-Scope
* **User Authentication:** Single Sign-On (SSO) using corporate email accounts.
* **Ticket Lifecycle Management:** Create, edit, assign, view, and close tickets.
* **Categorization & Prioritization:** Matrix-based priority assignment (Low, Medium, High, Critical) linked to SLAs.
* **Status Workflow:** Standard transition flow: `New` -> `Assigned` -> `In Progress` -> `Resolved` -> `Closed`.
* **Basic Reporting Dashboard:** High-level metrics showing open vs. closed tickets and average resolution time.

### Out-of-Scope (Future Phases)
* Native Mobile Applications (iOS/Android).
* AI-powered Chatbot for automated first-level troubleshooting.
* Third-party integrations (Asset Management software, Jira API).

---

## Repository Structure & Artifacts
* **[Product Requirements Document (PRD)](./docs/01_product_requirements.md):** Detailed functional and non-functional requirements, business rules, and user stories. *(Coming Soon)*
* **System Architecture & Diagrams:** Use Case, Activity, and Entity-Relationship Diagrams (ERD). *(Coming Soon)*
* **UI/UX Wireframes:** Low-fidelity mockups of key user dashboards. *(Coming Soon)*