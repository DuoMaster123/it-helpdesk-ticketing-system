# System Architecture & Diagrams
**Project:** Internal IT Helpdesk Ticketing System  

This document visualizes the system's interactions and workflows using Mermaid.js. GitHub natively supports Mermaid, allowing these diagrams to be rendered directly from code.

## 1. Use Case Diagram
This diagram outlines the primary actors in the system and their respective interactions (Use Cases) with the Helpdesk application.

```mermaid
flowchart LR
    %% Define Actors
    Requester([Employee / Requester])
    Agent([IT Support Agent])
    Manager([IT Manager])

    %% Define Use Cases
    subgraph Helpdesk System
        UC1(Submit a Ticket)
        UC2(View My Tickets)
        UC3(Update Ticket Status)
        UC4(Add Internal Notes)
        UC5(Reassign Ticket)
        UC6(View SLA Dashboard)
        UC7(Manage Categories)
    end

    %% Map Interactions
    Requester --- UC1
    Requester --- UC2
    
    Agent --- UC2
    Agent --- UC3
    Agent --- UC4
    
    Manager --- UC3
    Manager --- UC5
    Manager --- UC6
    Manager --- UC7
```

## 2. Ticket Status Workflow (State Diagram)
This state machine diagram illustrates the strict lifecycle a ticket follows from creation to closure. It reflects the business rules defined in the PRD.

```mermaid
stateDiagram-v2
    direction TB
    [*] --> New : Ticket Created by Employee

    New --> Assigned : Manual or Auto-routing
    Assigned --> InProgress : Agent starts investigation
    
    InProgress --> PendingRequester : Agent requests more info
    PendingRequester --> InProgress : Requester provides info
    
    InProgress --> Resolved : Agent applies fix
    
    Resolved --> Closed : Requester verifies fix
    Resolved --> InProgress : Requester rejects fix
    Resolved --> Closed : Auto-close after 72 hours
    
    Closed --> [*]
```

## 3. Basic Entity-Relationship Diagram (ERD)
This diagram defines the foundational data structure required for the Phase 1 (MVP) release.

```mermaid
erDiagram
    USER {
        string user_id PK
        string email
        string full_name
        string role "Employee, Agent, Manager"
        string department
    }
    
    TICKET {
        string ticket_id PK
        string title
        string description
        string status "New, Assigned, In Progress, etc."
        string priority "P1, P2, P3, P4"
        datetime created_at
        datetime resolved_at
        string requester_id FK
        string assignee_id FK
    }
    
    COMMENT {
        string comment_id PK
        string ticket_id FK
        string author_id FK
        text content
        boolean is_internal
        datetime created_at
    }

    USER ||--o{ TICKET : "creates (as requester)"
    USER ||--o{ TICKET : "works on (as assignee)"
    TICKET ||--o{ COMMENT : "has"
    USER ||--o{ COMMENT : "writes"
```