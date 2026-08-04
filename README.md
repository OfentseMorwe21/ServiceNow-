# 🚀 IT Onboarding Hub — Scoped ServiceNow Application

An end-to-end, custom-built **ServiceNow Scoped Application (`x_onboard`)** designed to streamline and automate corporate employee onboarding. Built on a Personal Developer Instance (PDI), this project implements full-stack ServiceNow configurations including Service Portals, Service Catalog, Knowledge Management, server-side scripting, custom security policies (ACLs), and automated workflows.

---

## 🛠️ Tech Stack & Key ServiceNow Capabilities

* **Platform Utilities:** Application Studio, Service Portal, Service Catalog, Knowledge Management, Automated Test Framework (ATF).
* **Scripting & APIs:** JavaScript (ES5/ES6), `GlideRecord`, `GlideSystem` (`gs`), `GlideDateTime`, `g_form`, AngularJS (Portal Widgets), Script Includes.
* **Security & Automation:** Access Control Lists (ACLs), Business Rules (Before/After), UI Actions, UI Policies, Flow Designer.

---

## 🏗️ Application Architecture

The application is built within a self-contained scope (`x_onboard`) across five core layers:

```text
 ┌─────────────────────────────────────────────────────────────┐
 │                      SERVICE PORTAL LAYER                   │
 │      Branded /onboarding Portal, Custom Widgets, Mobile      │
 └──────────────────────────────┬──────────────────────────────┘
                                │
 ┌──────────────────────────────┴──────────────────────────────┐
 │                      SELF-SERVICE LAYER                     │
 │  4x Catalog Items, 1x Order Guide, 8-10 KB Articles (User Criteria) │
 └──────────────────────────────┬──────────────────────────────┘
                                │
 ┌──────────────────────────────┴──────────────────────────────┐
 │                   BUSINESS LOGIC & SECURITY                 │
 │   Business Rules, Script Includes (OnboardingUtils), ACLs   │
 └──────────────────────────────┬──────────────────────────────┘
                                │
 ┌──────────────────────────────┴──────────────────────────────┐
 │                       DATA SCHEMA LAYER                     │
 │   x_onboard_request (extends Task) | x_onboard_checklist_item│
 └─────────────────────────────────────────────────────────────┘

```

### Role-Based Access Control (RBAC)

* **`x_onboard.employee`**: End-user access. Can submit requests, track progress, and read self-service KB articles. Restrictive row-level security prevents viewing other users' data.
* **`x_onboard.fulfiller`**: IT Support team access. Can process, fulfill, approve, or reject incoming onboarding tasks.
* **`x_onboard.manager`**: Elevated administrative access. Can publish/retire KB articles, view performance analytics dashboards, and manage workflows.

---

## 📋 Core Modules & Feature Highlights

### 1. Branded Service Portal (`/onboarding`)

* **Custom UI/UX:** Built with a clean, responsive layout utilizing custom CSS/SASS, dynamic greeting widgets with data binding, quick-action catalog tiles, and featured announcements.
* **Progress Tracker Widget:** AngularJS widget that reads live checklist data from `x_onboard_checklist_item` to display a real-time onboarding completion percentage bar for new starters.

### 2. Service Catalog & Order Guides

* **Catalog Items:** Custom items for *Equipment Requests*, *System Access Requests*, *IT Help Requests*, and *Facilities Requests* with dynamic UI Policies (e.g., conditional field visibility for monitor sizes).
* **New Starter Bundle (Order Guide):** Bundles hardware and system access into a single seamless submission workflow.

### 3. Server-Side Automation & Scripting

* **`OnboardingUtils` Script Include:** Encapsulates reusable helper functions (`validateRequest`, `getAssignmentGroup`, `logAction`) to ensure modular code structure.
* **Business Rules:**
* **Auto-Assign by Category (`Before Insert`):** Dynamically assigns requests to target groups (*IT Hardware*, *IT Security*, or *General IT*) based on catalog selections.
* **Dynamic SLA Calculation (`After Insert`):** Uses `GlideDateTime` logic to automatically calculate target resolution dates (e.g., 5 business days for hardware, 2 days for access).
* **Automated Notifications (`After Update`):** Sends personalized email notifications to requestors upon ticket state changes.



### 4. Advanced Security & Data Integrity

* **Granular ACL Enforcement:** Enforces strict field-level and row-level access control. Restricts `fulfiller_notes` visibility to support staff and applies row-level query filtering (`opened_by = gs.getUserID()`) for end-users.
* **Scripted UI Actions:** Features interactive form buttons including **Approve & Fulfil** (server-validated through Script Include) and **Reject with Reason** (client-side modal prompt driving server updates).

### 5. Quality Assurance & Reporting

* **ATF Test Suite:** End-to-end automated test suites validating catalog submissions, SLA calculations, role impersonation, and security boundaries.
* **Manager Dashboard Page:** Dedicated portal dashboard for managers featuring category breakdowns, 30-day submission volumes, average resolution metrics, and overdue ticket tracking.

---

## 📅 Implementation Roadmap (5-Week Build)

* **Week 1 (Portal & Catalog):** Scoped app creation, portal branding, 4 catalog items, UI policies, and "New Starter Bundle" Order Guide.
* **Week 2 (Knowledge Base):** User Criteria setup, authoring 8 KB articles, related catalog links, and Flow Designer feedback workflows.
* **Week 3 (Backend Logic & Security):** `OnboardingUtils` Script Include, Business Rules, UI Actions, and table/field-level ACL policies.
* **Week 4 (Extensions):** AngularJS Checklist Tracker, Manager Dashboard, mobile optimizations, and full ATF test suites.
* **Week 5 (Documentation & Handover):** Technical documentation, user guides, and architecture mapping.
