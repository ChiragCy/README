# Golden Visit Report Template

> **User Story:** 1043380
>
> **Title:** Documentation – Creation of Golden Visit Report Template
>
> **Program:** Salesforce@AP
>
> **Solution Area:** Visit Management
>
> **Document Status:** Approved
>
> **Documentation Type:** Functional & Technical Solution Documentation
>
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
- Deployment Overview
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
- Unified Security Model
- Standardized Lightning User Experience
- Mobile Optimization

The objective is to provide a unified metadata structure, security model, Lightning architecture, and AI-enabled visit documentation process.

Supported personas:

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
      +-----------------+------------------+
      |                 |                  |
      v                 v                  v
   Details          Related            Crops
     Tab              Tab               Tab
                                           |
                                           v
                           Visit Report Crop Records
                                           |
                                           v
                               Create / Edit Crop Data

                        |
                        v
                 Meeting Notes Tab
                        |
                        v
              Visit Report Creation Flow
                        |
                        v
                  AI Components
                        |
    +-------------------+-------------------+
    |                   |                   |
    v                   v                   v
Einstein          Fetch Metadata      Process Visit
Transcribe             Flow             Summary
                        |
                        v
                 Save Visit Report
                        |
                        v
              Create Tasks & Events
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

The Golden Visit Report Record Type provides a globally standardized Visit Report experience while supporting AI-assisted visit planning, documentation, summaries, transcription and follow-up management.

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
| Reminder For Visit |
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

## SC_VisitReport_GLB_Layout

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

> **Note:** Visit Report Crops are additionally exposed through a dedicated **Crops Tab** on the Golden Visit Report Lightning Page to improve usability and allow direct crop management from the Visit Report experience.

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

Contains:

- General Information
- Pre-Call Plan
- Visit Preparation
- Visit Information
- Post-Call Analysis
- System Information

### Related Tab

Contains:

- Files
- Visit Products
- Visit Report Topics
- Visit Report Attendees
- Notification Histories

### Crops Tab

The Crops tab provides dedicated management of Visit Report Crop records associated with the Visit Report.

#### Purpose

Allows Sales users to capture crop-related information discussed during customer visits and maintain traceability between the Visit Report and Crop records.

#### Available Features

- View Visit Report Crops
- Create New Visit Report Crop
- Edit Existing Crop Records
- Review Crop Information
- Navigate between Visit Report and Crop records

#### Related List

| Related List |
|--------------|
| Visit Report Crops |

#### User Actions

| Action |
|---------|
| New Visit Report Crop |
| Open Existing Crop |
| Edit Crop |
| View Crop Details |

#### Supported Personas

- Sales Representative
- Sales Manager
- Commercial Excellence

#### Business Value

The Crops tab separates crop-specific discussions from the main Visit Report while maintaining a direct relationship to the customer visit, improving reporting accuracy and user experience.

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

## Dynamic Actions

- Edit Attendees
- File
- Delete
- Post
- Distribute Internally
- View PDF
- Clone with Related
- New Sales Event

---

# 3.6 Validation Rules

No new validation rules were introduced for the Golden Template implementation.

Validation occurs through:

- Standard Salesforce Validations
- Flow Validations
- AI Data Validation
- Save-Time Validation

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

- Sales Representative
- Sales Manager
- Commercial Excellence

---

# 3.9 Permission Sets

- SC_CORE
- SALESREP_BASE
- SALESMANAGER_BASE
- COMMERCEEXCELLENCE_BASE
- Visit Report Creation
- Visit Report Preparation

---

# 3.10 Permission Set Groups

- SalesRep_SC_GRP
- SalesManager_SC_GRP
- CommercialExcellence_SC_GRP

---

# 3.11 Profiles

- SC_LITE

---

# 3.12 Custom Permissions

- VisitReportCreation
- SALESREP_SC_CP
- SALESMANAGER_SC_CP
- COMMERCIALEXCELLENCE_SC_CP

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
| Create Visit Report Crop | ✅ | ✅ | ✅ |
| Edit Visit Report Crop | ✅ | ✅ | ✅ |
| View Visit Report Crop | ✅ | ✅ | ✅ |

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
+-- Crops Tab
|      |
|      +-- Visit Report Crops
|      +-- New Crop Creation
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

User navigates to the Crops Tab.

### Step 5

User reviews Crop information associated with the Visit Report.

### Step 6

User opens Meeting Notes.

### Step 7

User launches AI preparation.

### Step 8

AI provides:

- Suggested Visit Content
- Recommendations
- Summary Assistance

### Step 9

User records voice notes.

### Step 10

EinsteinTranscribeWCmp converts speech to text.

### Step 11

Flow processes data and updates Visit Report.

### Step 12

User reviews Post-Call Analysis.

### Step 13

User saves Visit Report.

### Step 14

System creates follow-up Tasks and Events when applicable.

---

## Screenshot Placeholders

### Create Visit Report

<img width="1136" height="727" alt="image" src="https://github.com/user-attachments/assets/ffba9b0d-be92-4865-b5aa-91aafc48a413" />

### Golden Layout

<img width="1858" height="792" alt="image" src="https://github.com/user-attachments/assets/c44a1bdd-f5ba-4722-b26b-ce3f942ab050" />

### Tabs
<img width="499" height="76" alt="image" src="https://github.com/user-attachments/assets/afff7168-a877-4f27-995c-17b33b0e94ca" />

### Meeting Notes & AI Experience
<img width="1233" height="625" alt="image" src="https://github.com/user-attachments/assets/39f98ac2-5a39-4404-af35-1544074c8a39" />

### Dynamic Actions

<img width="1281" height="106" alt="image" src="https://github.com/user-attachments/assets/d0cd0051-a73b-44b1-8f39-c08ebd39624c" />


### Mobile Experience

> Insert Screenshot

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

## Visit Report Crops Management

### Component Type

Lightning Page Configuration

### Purpose

Provides dedicated access to Visit Report Crop records directly from the Visit Report.

### Trigger

User navigates to the Crops Tab.

### Actions Supported

- Create Visit Report Crop
- Edit Visit Report Crop
- View Visit Report Crop
- Navigate between child crop records and parent Visit Report

### Expected Behaviour

All Crop records remain associated with the current Visit Report and inherit the same security model and access permissions defined for Golden Visit Report users.

---


# Business Context

As part of the global Farm2Cloud transformation initiative, BASF is standardizing the Visit Management process through the implementation of a single Golden Visit Report template.

Historically, multiple Visit Report templates existed across regions, resulting in inconsistent user experiences, fragmented reporting capabilities, varying business processes, and differences in data quality.

The Golden Visit Report Template addresses these challenges by introducing:

- A globally standardized Visit Report record type
- Consistent Lightning Experience layouts
- Standardized metadata structure
- Unified security and access model
- AI-powered visit preparation capabilities
- Voice-to-text visit documentation
- Mobile-ready user experience

The objective is to ensure that all Sales users operate using a common process while maintaining regional scalability and supporting future global enhancements.

---

# Solution Overview

The Golden Visit Report solution consists of four primary functional areas:

1. Visit Planning
2. Visit Execution
3. Visit Documentation
4. Follow-Up Management

Users can prepare customer visits, capture visit outcomes, generate AI-powered summaries, manage crop-related information, and create follow-up activities within a single consolidated user experience.

The solution leverages Salesforce Lightning Experience, Flow Automation, AI Components, Dynamic Forms, Dynamic Actions, and Standard Salesforce Security features.

---

# Key Features

## Golden Visit Report Experience

Provides a consistent Visit Report structure across all supported business units.

Capabilities include:

- Standardized page layouts
- Standardized Lightning Pages
- Unified record type structure
- Consistent field organization
- Global reporting support

---

## AI Visit Preparation

Users can leverage AI functionality to prepare customer visits.

Capabilities include:

- AI-generated visit preparation recommendations
- Suggested talking points
- AI-generated visit summaries
- Intelligent field population

Benefits include:

- Reduced manual effort
- Increased productivity
- Improved visit quality
- More consistent customer engagement

---

## Voice-to-Text Documentation

Sales users can dictate visit notes directly within the Visit Report.

Capabilities include:

- Audio recording
- Speech recognition
- Automatic transcription
- Direct population of Visit Report fields

Benefits include:

- Faster documentation
- Better field adoption
- Reduced administrative effort
 ---

## Technical Execution Flow

```text
User
 |
 v
FlexiPage
 |
 +---- Crops Tab
 |         |
 |         +---- Create/Edit Crop Records
 |
 +---- Meeting Notes
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
