# Golden Visit Report Template

> **User Story:** 1043380  
> **Title:** Documentation – Creation of Golden Visit Report Template  
> **Program:** Salesforce@AP  
> **Solution Area:** Visit Management  
> **Document Status:** Approved  
> **Documentation Type:** Functional & Technical Solution Documentation  
> **Reference Stories:** 1032101, 1034337

---

# Table of Contents

- Executive Summary
- Solution Architecture
- Metadata
  - Object Overview
  - Fields
  - Record Types
  - Page Layouts
  - Lightning Pages
  - Validation Rules
  - Flows
  - Personas
  - Permission Sets
  - Permission Set Groups
  - Profiles
  - Custom Permissions
- Access Model
- UI / UX
- Business Logic
- Traceability Matrix
- Approval Summary

---

# 1. Executive Summary

The Golden Visit Report Template establishes a standardized global Visit Report process across Salesforce@AP.

The solution consolidates:

- AP Global Visit Report Template
- APN Visit Report Template
- AI Visit Preparation Capabilities
- Voice-to-Text Transcription
- AI Summary Generation

The objective is to provide a unified user experience, consistent metadata model, standardized Lightning layout, and AI-enabled Visit Report creation process.

The solution supports the following personas:

- Sales Representative
- Sales Manager
- Commercial Excellence

---

# 2. Solution Architecture

## High-Level Solution Architecture

```text
+----------------------------------------------------+
|                    Salesforce User                 |
+----------------------------------------------------+
                        |
                        v
+----------------------------------------------------+
|         SC_VisitReport_GLB_FlexiPage               |
+----------------------------------------------------+
                        |
        +---------------+----------------+
        |               |                |
        v               v                v
     Details         Related       Meeting Notes
       Tab             Tab              Tab
                                           |
                                           v
                           Visit Report Creation Flow
                                           |
                                           v
                              AI Service Components
                                           |
               +---------------------------+--------------------------+
               |                           |                          |
               v                           v                          v
    EinsteinTranscribeWCmp   Fetch Metadata Flow    Process Summary Flow
               |                           |                          |
               +---------------------------+--------------------------+
                                           |
                                           v
                                  Save Visit Report
                                           |
                                           v
                              Create Tasks and Events
```

---

# 3. Metadata

# 3.1 Object Overview

| Attribute | Value |
|------------|---------|
| Object Name | Visit Report |
| Record Type | SC_VisitReport_GLB |
| Layout | SC_VisitReport_GLB_Layout |
| FlexiPage | SC_VisitReport_GLB_FlexiPage |
| Global Template | Yes |
| Mobile Compatible | Yes |
| AI Enabled | Yes |

## Purpose

The Golden Visit Report Record Type provides a globally standardized Visit Report experience while supporting AI-assisted visit preparation and post-visit documentation.

---

# 3.2 Fields

## General Information

| Field |
|---------|
| Visit ID |
| Visit Report Name |
| Account |
| Events |
| OD Campaign |
| Status |
| Reason of Visit |
| Contact Type |
| Visit Start Date |
| Visit End Date |
| Business Segment |
| Account Plan |
| Account Plan Objective |

---

## Pre-Call Plan

| Field |
|---------|
| Call Objective |
| Statement of Intent |
| Behavior Style |
| Resources / Collateral Needed |
| GAP Model Questions |
| Differentiated Features & Benefits |
| Possible Objections |

---

## Visit Preparation

| Field |
|---------|
| Visit Preparation |

---

## Visit Information

| Field |
|---------|
| General Summary |

---

## Post-Call Analysis

| Field |
|---------|
| What Went Well |
| What Could Improve |
| Next Call Objective |
| Follow Up Actions |
| Last Visit Summary |
| Market Feedback |
| Reminder for the Visit |
| Net Promoter Score |
| Campaign History |
| AP Survey |

---

## System Information

| Field |
|---------|
| Created By |
| Last Modified By |
| Record Type |

---

# 3.3 Record Types

| Object | Record Type |
|----------|-------------|
| Visit Report | SC_VisitReport_GLB |
| Task | SC_SalesTask_GBL |
| Event | SC_SalesEvent_GBL |

---

# 3.4 Page Layouts

## Layout

### SC_VisitReport_GLB_Layout

### Layout Sections

1. General Information
2. Pre-Call Plan
3. Visit Preparation
4. Visit Information
5. Post-Call Analysis
6. System Information

### Related Lists

| Related List |
|--------------|
| My Insights |
| Visit Products |
| Visit Report Crops |
| Files |
| Visit Report Attendees |
| Notification Histories |
| Visit Report Topics |

### Actions

| Action |
|---------|
| Edit Attendees |
| File |
| Delete |
| Post |
| Distribute Internally |
| View PDF |
| Clone with Related |
| New Sales Event |

---

# 3.5 Lightning Pages

## Lightning Record Page

### SC_VisitReport_GLB_FlexiPage

| Feature | Value |
|----------|---------|
| Dynamic Forms | Enabled |
| Dynamic Actions | Enabled |
| Mobile Optimized | Yes |
| App Assignment | Sales |
| Assigned Profile | SC_LITE |

---

## Lightning Tabs

### Details Tab

Contains all business sections:

- General Information
- Pre-Call Plan
- Visit Preparation
- Visit Information
- Post-Call Analysis
- System Information

### Related Tab

Contains:

- Files
- Products
- Crops
- Topics
- Attendees
- Notifications

### Meeting Notes Tab

Contains:

- Visit Report Creation Flow
- AI Components
- Meeting Notes Functionality

### Chatter Tab

Contains standard Chatter functionality.

### Activity Tab

Contains:

- Tasks
- Events
- Activity Timeline

---

# 3.6 Validation Rules

No new validation rules were introduced as part of the Golden Template implementation.

Validation occurs through:

- Existing Salesforce Validation Rules
- Screen Flow Validation
- AI Data Validation
- Save-Time Record Validation

---

# 3.7 Flows

| Flow Name | Purpose |
|------------|----------|
| Fetch Metadata for Objects | Retrieves metadata used by AI engine |
| Process Visit Summary | Generates Visit Summary |
| Check Users Profile | Determines Golden Record Type access |
| Suggested Records To Create Or Update | Creates recommendations |
| Visit Report Creation | Guided Visit Report process |

---

## Flow Execution

```text
User Creates Visit Report
          |
          v
Check Users Profile
          |
          v
Assign SC_VisitReport_GLB
          |
          v
Open Meeting Notes
          |
          v
Visit Report Creation Flow
          |
          v
Fetch Metadata For Objects
          |
          +-------------------------+
          |                         |
          v                         v
AI Suggestions      Voice Transcription
          |                         |
          +------------+------------+
                       |
                       v
             Process Visit Summary
                       |
                       v
      Suggested Records To Create Or Update
                       |
                       v
             Save Visit Report
```

---

# 3.8 Personas

| Persona |
|----------|
| Sales Representative |
| Sales Manager |
| Commercial Excellence |

---

# 3.9 Permission Sets

| Permission Set |
|----------------|
| SC_CORE |
| SALESREP_BASE |
| SALESMANAGER_BASE |
| COMMERCEEXCELLENCE_BASE |
| Visit Report Creation |
| Visit Report Preparation |

---

# 3.10 Permission Set Groups

| Permission Set Group |
|-----------------------|
| SalesRep_SC_GRP |
| SalesManager_SC_GRP |
| CommercialExcellence_SC_GRP |

---

# 3.11 Profiles

| Profile |
|----------|
| SC_LITE |

---

# 3.12 Custom Permissions

| Custom Permission |
|-------------------|
| VisitReportCreation |
| SALESREP_SC_CP |
| SALESMANAGER_SC_CP |
| COMMERCIALEXCELLENCE_SC_CP |

---

# 4. Access Model

## Security Architecture

```text
Profiles
   |
   +-- SC_LITE
           |
           v
Permission Set Groups
           |
           +-- SalesRep_SC_GRP
           +-- SalesManager_SC_GRP
           +-- CommercialExcellence_SC_GRP
                       |
                       v
Permission Sets
                       |
      +----------------+----------------+
      |                |                |
      v                v                v
 SALESREP_BASE   SALESMANAGER_BASE  COMMERCEEXCELLENCE_BASE
                       |
                       v
Custom Permissions
                       |
      +----------------+----------------+
      |                |                |
      v                v                v
SALESREP_CP  SALESMANAGER_CP  COMMERCIALEXCELLENCE_CP
```

---

## OWD & Sharing

| Setting | Value |
|----------|---------|
| OWD | AS-IS |
| Sharing Model | Existing Sharing Model |
| Additional Sharing Logic | None |

---

## Persona Capability Matrix

| Capability | Sales Rep | Sales Manager | Commercial Excellence |
|------------|-----------|---------------|----------------------|
| Create Visit Report | ✅ | ✅ | ✅ |
| Read Visit Report | ✅ | ✅ | ✅ |
| Edit Visit Report | ✅ | ✅ | ✅ |
| AI Preparation | ✅ | ✅ | ✅ |
| Voice Transcription | ✅ | ✅ | ✅ |
| Create Task | ✅ | ✅ | ✅ |
| Create Event | ✅ | ✅ | ✅ |
| View PDF | ✅ | ✅ | ✅ |
| Clone with Related | ✅ | ✅ | ✅ |

---

# 5. UI / UX

## Lightning Page Structure

```text
SC_VisitReport_GLB_FlexiPage
|
+-- Highlights Panel
|      |
|      +-- Dynamic Actions
|
+-- Details Tab
|
+-- Related Tab
|
+-- Meeting Notes Tab
|      |
|      +-- AI Components
|      +-- Visit Report Creation Flow
|
+-- Chatter Tab
|
+-- Activity Tab
```

---

## End-to-End User Journey

### Step 1

User clicks **New Visit Report**.

### Step 2

Golden Visit Report Record Type is assigned.

### Step 3

User completes:

- General Information
- Pre-Call Planning

### Step 4

User opens Meeting Notes.

### Step 5

User launches AI preparation.

### Step 6

AI provides:

- Suggested Visit Content
- Recommendations
- Summary Assistance

### Step 7

User records voice notes.

### Step 8

EinsteinTranscribeWCmp converts speech to text.

### Step 9

Flow processes data and updates Visit Report.

### Step 10

User reviews Post-Call Analysis.

### Step 11

User saves Visit Report.

### Step 12

System creates follow-up Tasks and Events when applicable.

---

## Screenshot Placeholders

### Create Visit Report

> Add Screenshot

### Golden Layout

> Add Screenshot

### Meeting Notes & AI Experience

> Add Screenshot

### Dynamic Actions

> Add Screenshot

### Mobile Experience

> Add Screenshot

---

# 6. Business Logic

## Automation Components Inventory

| Component | Type | Purpose |
|------------|------|----------|
| EinsteinTranscribeWCmp | AI Component | Voice-to-text transcription |
| customTextareaWCmp | AI Component | Text processing |
| Fetch Metadata For Objects | Flow | Metadata retrieval |
| Process Visit Summary | Flow | Summary generation |
| Check Users Profile | Flow Decision | Profile evaluation |
| Visit Report Creation | Flow | Guided report process |
| Suggested Records To Create Or Update | Flow | Follow-up record creation |

---

## Technical Execution Flow

```text
User
 |
 v
FlexiPage
 |
 v
Meeting Notes
 |
 v
Visit Report Creation Flow
 |
 v
Fetch Metadata Flow
 |
 v
AI Components
 |
 +-------- EinsteinTranscribeWCmp
 |
 +-------- customTextareaWCmp
 |
 v
Process Visit Summary
 |
 v
Suggested Records
 |
 +-------- Tasks
 |
 +-------- Events
 |
 v
Save Visit Report
```

---

# 7. Traceability Matrix

| Requirement | Source Story |
|-------------|--------------|
| Golden Record Type | 1032101 |
| Golden Layout | 1032101 |
| Golden FlexiPage | 1032101 |
| Dynamic Actions | 1032101 |
| Mobile Optimization | 1032101 |
| AI Enablement | 1034337 |
| Voice-to-Text | 1034337 |
| Visit Summary AI | 1034337 |
| Permission Updates | 1034337 |
| Documentation Consolidation | 1043380 |

---

# 8. Deployment Overview

## Metadata Deployed

- Record Types
- Page Layouts
- Lightning Pages
- Flows
- Permission Sets
- Permission Set Groups
- Custom Permissions

---

## Impacted Personas

- Sales Representative
- Sales Manager
- Commercial Excellence

---

## Impacted Processes

- Visit Planning
- Visit Execution
- Post-Visit Documentation
- AI Assisted Visit Reporting
- Follow-up Management
