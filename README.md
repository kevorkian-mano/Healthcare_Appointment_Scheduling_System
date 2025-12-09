# Healthcare Appointment Scheduling System - Architecture Design Documentation

## 📋 Executive Summary

The **Healthcare Appointment Scheduling System** is a comprehensive software architecture project documenting the complete design of a scalable healthcare platform. This project spans three major milestones, progressively analyzing requirements, designing system architectures, and developing UML diagrams and final architecture specifications.

**System Purpose:** A digital platform that enables patients to search for doctors, book/manage appointments, and receive automated reminders while allowing doctors to manage schedules and availability, with built-in security and support for 10,000+ concurrent users.

---

## 📑 Table of Contents

1. [Milestone 1: Requirements Analysis & System Decomposition](#milestone-1-requirements-analysis--system-decomposition)
2. [Milestone 2: UML Diagrams & Process Modeling](#milestone-2-uml-diagrams--process-modeling)
3. [Milestone 3: Architecture Design & Implementation](#milestone-3-architecture-design--implementation)

---

# Milestone 1: Requirements Analysis & System Decomposition

## 📝 Overview

Milestone 1 focuses on comprehensive requirements gathering through stakeholder interviews. An analyst conducts detailed client interviews to extract functional and non-functional requirements, establish system decomposition strategies, and identify architectural constraints.

## 🎯 Requirements Extraction Process

The requirements were gathered through **12 detailed interview sessions** with the client, following a systematic analysis approach:



### **Functional Requirements (10 Features)**

| # | Feature | Description |
|---|---------|-------------|
| 1 | Patient Registration | Patients create accounts with credentials |
| 2 | Doctor Search | Search doctors by specialty, location, availability |
| 3 | Appointment Booking | Book appointments with selected doctor and time |
| 4 | Appointment Management | Reschedule and cancel appointments |
| 5 | Schedule Management | Doctors manage working hours and schedules |
| 6 | Availability Updates | Doctors adjust availability in real-time |
| 7 | Appointment Viewing | Doctors and patients view appointment details |
| 8 | Email Reminders | Automated email reminders before appointments |
| 9 | SMS Reminders | Automated SMS reminders before appointments |
| 10 | EHR Integration | Future capability to connect with hospital records |

### **Non-Functional Requirements (11 Constraints)**

| Category | Requirement | Specification |
|----------|-------------|----------------|
| **Performance** | Response Time | <2 seconds for all operations |
| **Performance** | Concurrency | Support 10,000+ concurrent users |
| **Usability** | User-Friendly | Simple, intuitive interface |
| **Usability** | Mobile-First | Primary access via mobile devices |
| **Usability** | Accessibility | WCAG compliance for all users |
| **Scalability** | Architecture Evolution | Supports scaling to microservices |
| **Scalability** | Growth Capacity | Scale from thousands to millions of users |
| **Reliability** | Double-Booking Prevention | Prevent conflicting appointment bookings |
| **Reliability** | Reminder Delivery | Timely, reliable notification delivery |
| **Availability** | Uptime | 24/7 availability (99.9%+ SLA) |
| **Security** | Data Protection | Encryption of credentials and patient data |
| **Security** | Access Control | Role-based access control (RBAC) |
| **Maintainability** | Modularity | Independent modules for easy maintenance |
| **Maintainability** | Flexibility | Easy to accommodate changes |

### **System Decomposition**

**Module-Based Decomposition:**
```
Healthcare Appointment System
├── Patient Module
│   ├── Registration
│   ├── Profile Management
│   └── Appointment History
├── Doctor Module
│   ├── Profile Management
│   ├── Schedule Management
│   └── Availability Management
├── Scheduling Module
│   ├── Appointment Booking
│   ├── Conflict Prevention
│   ├── Time Slot Management
│   └── Rescheduling/Cancellation
└── Notification Module
    ├── Email Delivery
    ├── SMS Delivery
    └── Reminder Scheduling
```


---

# Milestone 2: UML Diagrams & Process Modeling

## 📊 Overview

Milestone 2 provides detailed visual representations of system behavior through **Sequence Diagrams** and **Business Process Model and Notation (BPMN)** diagrams. These diagrams show exactly how users interact with the system and how components communicate.

---

## 🔄 Sequence Diagrams

Sequence Diagrams show the **flow of messages and interactions** between system components and actors.

### **Sequence 1: Patient Register / Login / Search Doctor / View Doctor Profile / View History**
**Key Points:**
- Patient registration stores credentials securely
- Login verification checks username/password with error handling
- Doctor search retrieves full list from database
- Doctor profile retrieves detailed information
- Appointment history shows all past/future appointments

---

### **Sequence 2: Patient Book and Confirm Appointments**
**Key Points:**
- Availability check prevents double-booking
- Appointment saved atomically to database
- Notifications sent to both patient and doctor
- Confirmation displayed to patient

---

### **Sequence 3: Patient Cancel / Reschedule Appointments**
**Key Points:**
- Reschedule checks new availability before confirming
- Cancel removes appointment and frees time slot
- Both operations trigger notifications to patient and doctor
- Confirmation shown to initiating party

---

### **Sequence 4: Doctor Login / Add and Modify Working Hours / View Schedule**
**Key Points:**
- Doctor login validates credentials
- Schedule view retrieves all appointments for doctor
- Add hours creates new availability slots
- Modify hours updates existing availability
- Updates confirmed immediately to doctor

---

### **Sequence 5: Admin Login / User Management / Password Reset**
**Key Points:**
- Admin login verifies administrative credentials
- Add user checks for duplicates before creating
- Deactivate user removes user from system
- Reset password updates credentials and notifies user
- All changes logged for audit trail

---

## 🔄 Business Process Model and Notation (BPMN)

BPMN diagrams show the **complete workflow** of how patients interact with the system from start to finish.



---

# Milestone 3: Architecture Design & Implementation

## 📐 Overview

Milestone 3 provides the final, production-ready architecture design with comprehensive justification for all architectural choices, detailed component specifications, and complete system interaction patterns.

---

## 🎯 System Description

**Healthcare Appointment Scheduling System** allows patients to book, manage, and cancel medical appointments while enabling doctors to control availability and schedules. The system provides real-time updates, automated notifications, and secure communication between patients and healthcare providers.

**Key Characteristics:**
- **Scalability:** Handles 10,000+ concurrent users
- **Performance:** <2 second response time for all operations
- **Availability:** 24/7 uptime with fault tolerance
- **Security:** Encrypted data, role-based access control
- **Mobile-First:** Responsive design for mobile devices

---

## 🏗️ Architecture Evolution Strategy
### **Phase 1: Monolithic Architecture (Initial MVP)**
---
### **Phase 2: Microservices Architecture (As System Grows)**
---

## 💡 Architecture Choice Justifications

### **Backend Architecture: Microservices**

**Why Microservices Over Monolithic?**

| Aspect | Benefit | Impact |
|--------|---------|--------|
| **Scalability** | Each service scales independently | Handle 10,000+ users efficiently |
| **Modularity** | Aligns with 4-module requirement | Direct mapping to business domains |
| **Fault Isolation** | Service failure doesn't crash system | Improved 24/7 availability |
| **Technology Flexibility** | Use best tech per service | Optimize each microservice |
| **Deployment** | Independent release cycles | Faster feature deployment |
| **Team Structure** | Teams own services end-to-end | Improved productivity |
| **Performance** | Services optimized individually | Meet <2 second requirement |
| **Future Growth** | Easy to add new services | Support EHR integration |

---

### **Frontend Architecture: SPA + PWA**

**Why SPA with PWA Features?**

#### **SPA (Single Page Application) Benefits:**
- ✅ **Fast Navigation:** Client-side routing, no full page reloads
- ✅ **Better UX:** Smooth transitions between views
- ✅ **Reduced Server Load:** Only API requests, not page rendering
- ✅ **Mobile-Friendly:** Perfect for mobile-first design
- ✅ **Meets Performance:** <2 second response via optimized data transfer

#### **PWA (Progressive Web App) Enhancements:**

```
Feature              SPA    PWA
─────────────────────────────────
Offline Support      ❌     ✅
Installable          ❌     ✅
Push Notifications   ❌     ✅
App-like Feel        ✓      ✅✅
Initial Load Speed   Slower Better (with caching)
Mobile Experience    Good   Excellent
```
---

## 📊 System Statistics

```
MICROSERVICES:                    7 Services
├── User Management Service       (3 instances)
├── Scheduling Service            (3 instances)
├── Notification Service          (3 instances)
├── Authentication Service        (2 instances)
├── Analytics & Reporting Service (2 instances)
├── Admin Service                 (2 instances)
├── Email Service                 (2 instances)
└── SMS Service                   (2 instances)

TOTAL INSTANCES:                  ~20 service instances

DATABASES:                        8 dedicated databases
├── User Store                    (1 Source + 3 Replicas)
├── Scheduling Store              (1 Source + 3 Replicas)
├── Notification Store            (1 Source + 3 Replicas)
├── Auth Store                    (1 Source + 3 Replicas)
├── Analytics Store               (1 Source + 3 Replicas)
├── Admin Store                   (1 Source + 3 Replicas)
├── Email Service DB              (Dedicated)
└── SMS Service DB                (Dedicated)

TOTAL DB INSTANCES:               ~27 database instances

CAPACITY:                         
├── Concurrent Users:             10,000+
├── Requests/Second:              50,000+
├── Response Time:                <2 seconds (p99)
├── Uptime SLA:                   99.9%
└── Availability Zones:           Multi-region ready

EXTERNAL INTEGRATIONS:
├── Email Provider                (SendGrid/AWS SES/Mailgun)
├── SMS Provider                  (Twilio/AWS SNS/Vonage)
└── Cloud Platform                (AWS/Google Cloud/Azure)
```

---


## 📈 Project Completion Status

### **Milestone 1: ✅ COMPLETED**
- [x] Requirements gathering (12 interviews)
- [x] Functional requirements extraction (11 features)
- [x] Non-functional requirements (12 constraints)
- [x] Module decomposition (4 modules)
- [x] Object-oriented decomposition (5 entities)
- [x] System analysis and documentation

### **Milestone 2: ✅ COMPLETED**
- [x] Sequence diagrams (5 detailed flows)
  - Patient register/login/search/view
  - Patient book appointments
  - Patient cancel/reschedule
  - Doctor login/schedule management
  - Admin user management
- [x] BPMN diagrams (Process flow)
  - Patient registration and login process
  - Complete patient workflow
- [x] UML documentation

### **Milestone 3: ✅ COMPLETED**
- [x] Monolithic architecture design
- [x] Microservices architecture design
- [x] Architecture evolution strategy
- [x] Frontend architecture justification (SPA + PWA)
- [x] Backend architecture justification (Microservices)
- [x] Component descriptions (7 services)
- [x] System interaction flows (3 detailed scenarios)
- [x] Database strategy (Source-Replica model)
- [x] Horizontal scaling strategy
- [x] Requirements coverage matrix
- [x] Technology recommendations
- [x] Complete system documentation

---


**Project Status: ✅ ALL MILESTONES COMPLETED SUCCESSFULLY**

**Architecture Ready for: Enterprise Implementation, Scalability Planning, Team Development, Future Enhancement**
