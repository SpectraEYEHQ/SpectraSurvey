# 📋 SpectraSurvey - Intensive Analysis (Technical + Business)

---

## 📑 Table of Contents

1. [🧭 Executive Summary](#-executive-summary)
2. [🎯 Application Purpose](#-application-purpose)
   - [Primary Purpose](#primary-purpose)
   - [Business Value](#business-value)
3. [🏢 Business Architecture](#-business-architecture)
   - [Main Actors](#main-actors)
   - [Capability Map](#capability-map-business)
   - [Business Map (Mermaid)](#business-map-mermaid)
4. [✨ Application Features](#-application-features)
   - [Authentication, Identity, Security](#41-authentication-identity-security)
   - [Full Survey Lifecycle](#42-full-survey-lifecycle)
   - [Response Collection (Public/Private)](#43-response-collection-publicprivate)
   - [Analytics and Reporting](#44-analytics-and-reporting)
   - [Groups, Invitations, Distribution](#45-groups-invitations-distribution)
   - [File Module (DAM)](#46-file-module-dam)
   - [Team and Organization Settings](#47-team-and-organization-settings)
   - [Platform Admin (Super Admin)](#48-platform-admin-super-admin)
   - [Audit and Compliance](#49-audit-and-compliance)
5. [🏗️ Technical Architecture](#️-technical-architecture)
   - [Technology Stack](#51-technology-stack)
   - [Backend Runtime Flag (QA/CI)](#511-backend-runtime-flag-qaci)
   - [Technical Map (System)](#52-technical-map-system)
   - [Frontend Component Architecture](#53-frontend-component-architecture)
   - [Express Backend (Functional Zones)](#54-express-backend-functional-zones)
   - [Hybrid Architecture (Current State)](#55-hybrid-architecture-current-state)
6. [🔄 Technical Flow Map](#-technical-flow-map)
   - [Login Flow](#61-login-flow-simplified)
   - [Public Survey Submit Flow](#62-public-survey-submit-flow)
   - [Secure File Sharing Flow](#63-secure-file-sharing-flow)
7. [🗃️ Data Architecture](#️-data-architecture)
   - [Data Domains](#71-data-domains)
   - [High-Level ER (Mermaid)](#72-high-level-er-mermaid)
   - [Multi-Tenancy](#73-multi-tenancy)
8. [🧩 Product Offering](#-product-offering)
9. [⚠️ Critical Observations (Risks and Gaps)](#️-critical-observations-risks-and-gaps)
   - [Integration Inconsistencies](#91-integration-inconsistencies)
   - [Operational Risks](#92-operational-risks)
   - [Branding and UX Consistency](#93-branding-and-ux-consistency)
10. [🛠️ Consolidation Recommendations](#️-consolidation-recommendations)
11. [📈 Recommended KPIs](#-recommended-kpis)
12. [✅ Conclusion](#-conclusion)

---

## 🧭 Executive Summary

**SpectraSurvey** is a multi-tenant platform designed for:

- creating, distributing, and analyzing surveys,
- managing organizational files through storage, sharing, and versioning,
- enabling team and organization administration with audit and compliance visibility,
- supporting centralized super-admin operations across tenants.

The product is already feature-rich and operationally valuable, but it still carries architectural complexity due to a mixed runtime model:
- **Express + MySQL** as the main backend foundation,
- **direct Supabase usage** still present in parts of the frontend and legacy flows.

This hybrid model increases maintenance cost, raises testing complexity, and introduces long-term consistency risks.

---

## 🎯 Application Purpose

### Primary Purpose

Provide organizations with a unified system for:

- survey operations,
- associated data and digital asset management,
- controlled collaboration,
- compliance visibility and governance.

### Business Value

- 📬 Improve response rates through multi-channel distribution and optimized public UX.
- 🧾 Provide traceability through audit and compliance visibility for enterprise and regulated use cases.
- 🗂️ Centralize survey data and digital assets in one operational workspace.
- 🏢 Support multi-tenant organizational administration with role-based control.
- 📊 Enable insight generation through survey analytics and response exploration.

---

## 🏢 Business Architecture

### Main Actors

- **Organization Member**: creates surveys, analyzes results, manages files.
- **Organization Admin**: manages members, policies, settings, and access.
- **Platform Super Admin**: governs tenants, users, and global configurations.
- **Respondent (External/Public)**: completes surveys through public or private access flows.

### Capability Map (Business)

- **Research Operations**: survey design, publishing, response collection.
- **Analytics & Insight**: dashboards, exports, response-level analysis.
- **Digital Asset Management**: folders, files, versions, sharing, trash.
- **Tenant Administration**: members, roles, organization settings.
- **Platform Governance**: global admin, monitoring, compliance controls.

### Business Map (Mermaid)

```mermaid
flowchart LR
  A["Respondent"] --> B["Public Survey Access"];
  B --> C["Survey Engine"];
  C --> D["Analytics"];
  C --> E["Audit Trail"];

  F["Organization Member"] --> C;
  F --> G["File Governance"];

  H["Organization Admin"] --> I["Tenant Settings"];
  H --> J["Team Management"];

  K["Super Admin"] --> L["Platform Control Plane"];
  L --> M["Organizations"];
  L --> N["Users"];
  L --> O["Compliance / Monitoring"];
