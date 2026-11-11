# QlockTap Core Engine — Enterprise Multi-Tenant EWA Architecture Specification

Welcome to the primary architectural specification repository for the **QlockTap Core Engine**. This public repository serves as an open-access blueprint mapping out the structural innovations, multi-tenant isolation loops, and advanced cybersecurity defensive controls engineered into the platform's decoupled backend mainframe.

---

## System Core Architecture & Design Patterns

The platform is designed following the **Hexagonal Architecture (Ports and Adapters) Pattern**. This architectural separation guarantees that core domain business calculations (such as dynamic earned wage cap pooling and financial clearing logic) remain completely isolated from volatile third-party network APIs, consumer client variations, and database ingestion channels.

```mermaid
graph TD
    A[Public Web & Mobile Traffic] --> B[AWS Route 53 Master DNS Steering Wheel]
    subgraph Elastic Cloud Computing Layer AWS
        B -->|dashboard.qlocktap.io| C[AWS Amplify CDN Edges — Nuxt 3 UI]
        B -->|api.qlocktap.io| D[AWS App Runner Auto-Scaling — NestJS API]
    end
    subgraph Hardened Data Partition Layer Supabase
        D -->|Pooled Sockets Port 6543| E[Supabase Enterprise Cluster Proxy]
        E --> F[Node A: Primary PostGIS Mainframe]
        E --> G[Node B: Streaming Read-Replica Failover Backup]
    end
```

### 1. Zero-Knowledge Spatial Ingestion & Presence Verification
To enforce strict worker tracking data anonymity and eliminate legal data-logging liabilities under the **Nigeria Data Protection Act (NDPA)** and global **GDPR** frameworks, raw telemetry vectors are never committed to permanent storage disk. Instead, incoming coordinates are instantly projected onto a discrete global hexagonal grid using **Uber's H3 Spatial Index Engine at Resolution 9**, resolving tracking boundaries down to an un-alterable binary `true/false` pass token inside the ledger.

```mermaid
graph TD
    A[Worker Triggers Clock-In Request] --> B[NestJS Attendance Ingress Gateway]
    subgraph Zero-Knowledge Processing Matrix
        B --> C[Extract Raw Geolocation Inputs: Longitude / Latitude]
        C --> D[Project Coordinates onto Uber H3 Resolution 9 Hex Cell Index]
        D --> E[Query Firm Geofence Table using H3 String Index Match]
        E --> F{Does Driver H3 Index == Firm Hub H3 Index?}
    end
    F -- NO --> G[Drop Request: 403 Forbidden Out of Perimeter]
    F -- YES --> H[Commit Shift Record: is_geofence_verified = TRUE]
    H --> I[Execute Cryptographic SHA-256 Anti-Tamper Row Signing]
```

### 2. Symmetrical B2B Onboarding Handshake Flow
SME enterprises register natively via authenticated credentials pools, spawning a unique, permanent 6-digit corporate token string reference. Workers use this single code block to self-onboard on their independent mobile devices. The backend intercepts the ingestion packet, captures mobile hardware configuration properties, and hashes them into an uncopyable SHA-256 fingerprint baseline rule to neutralize proxy clock-in and identity theft fraud loops.

```mermaid
sequenceDiagram
    participant SME as Corporate Dashboard Portal
    participant QT as QlockTap Decoupled API Core
    participant App as Driver Mobile Device Client

    SME->>QT: Initialize Corporate Identity (CAC & TIN Submission)
    QT->>QT: Provision Isolated Tenant Schema Row + Generate 6-Digit Company Token
    QT-->>SME: Render Active Workspace Interface
    Note over SME: Token shared with distributed staff pool via secure channels
    App->>QT: Fire Self-Onboarding Payload (Pass Name, Email, Base Pay & Company Token)
    QT->>QT: Execute Dynamic Token-Firm Database Cross-Lookup
    QT->>QT: Extract Device Motherboard, OS Build, and Display Canvas Vectors
    QT->>QT: Compute Irreversible SHA-256 Client-Hardware Signature Hash
    QT-->>App: Core Handshake Complete — Device Fingerprint Hard-Locked
```

### 3. Asymmetric Monthly Payroll Reconciliation & Clearing
At the close of an active billing cycle, the core analytics engine triggers high-performance relational left-joins across the schema partitions to compute dynamic salary deductions, platform administrative processing fees, and output bank-ready batch settlement manifests. This converts complex double-entry financial clearing math into clean, actionable, enterprise-standard data manifests.

```mermaid
graph TD
    A[Corporate HR Accountant Requests End-of-Cycle Reconciliation] --> B[Reconciliation Engine Service Core]
    subgraph Multi-Tenant Clearing Matrix
        B --> C[Pull Worker Profile Monthly Base Salary Baseline Records]
        B --> D[Left Join: Aggregate Verified Gross Shift Earnings from Ledger]
        B --> E[Left Join: Sum Successful Early Payout Vault Advances Disbursed]
        E --> F[Compute Total Platform Fees: ₦500 per transaction success]
    end
    F --> G[Execute Clearing Formula: Base Salary - Advances - Fees]
    G --> H[Compile Standardized Bank-Ready Payroll Manifest Sheet]
    H --> I[Transmit Disbursal File to FairMoney Open Banking Core Core]
```

---

## Applied Cybersecurity & Hardening Controls

Drawing directly from international enterprise information security methodologies, the core platform codebase is hardened against advanced security threat vectors:
* **Authenticated Column-Level Encryption:** Sensitive banking strings and routing fields are fully scrambled prior to storage using an authenticated **AES-256-GCM cipher pattern** holding automated Initialization Vectors (IV) and Galois authentication tags to completely neutralize direct database injection or internal breaching threats.
* **Perimeter Access Checkpoints:** API endpoints are protected via an asymmetric **JWT Bearer Token Guard** tracking custom metadata decorators to enforce strict Role-Based Access Control (**RBAC**), completely firewalling corporate data layers from field worker tokens.
* **Database Connection Pooling:** Backend container nodes map asynchronous transactions natively using **PgBouncer protocols over encrypted Port 6543** to completely eliminate connection socket starvation anomalies under massive spikes in concurrent traffic.

---
