# Hospital Management System - Research & Feasibility Document

**Date:** February 24, 2026
**Prepared by:** Imperial Networks Development Team
**Status:** Draft - Pending Client Meeting Review
**Approach:** Build from Scratch (AI-Assisted with Claude Code)
**Inspiration:** OpenEMR (open-source EHR)

---

## Table of Contents

1. [Problem Statement](#1-problem-statement)
2. [Philippine Hospital Pain Points](#2-philippine-hospital-pain-points)
3. [Regulatory Requirements](#3-regulatory-requirements)
4. [Inspiration: OpenEMR](#4-inspiration-openemr)
5. [Feature Set](#5-feature-set)
6. [Tech Stack & Architecture](#6-tech-stack--architecture)
7. [Pricing Model & Strategy](#7-pricing-model--strategy)
8. [Development Timeline & Cost (AI-Assisted)](#8-development-timeline--cost-ai-assisted)
9. [Competitive Landscape](#9-competitive-landscape)
10. [Next Steps](#10-next-steps)

---

## 1. Problem Statement

Philippine hospitals, especially Level 1-2 facilities, face significant operational inefficiencies due to manual processes, paper-based records, and lack of integrated systems. Key statistics:

- Average triage waiting time: **41.99 minutes**
- Average clinic consultation waiting time: **69.53 minutes**
- **21.5% of patients get lost** during the registration process
- Physician-to-population ratio: **1:25,300** (WHO standard is 1:1,000)
- Only **29% of Filipinos** expressed satisfaction with public healthcare (2021)
- PhilHealth owes hospitals approximately **PHP 27 billion** in unpaid/delayed claims
- There are **~1,351 hospitals** in the Philippines - 64% are Level 1 (basic) and underserved by IT

**Critical deadline: April 1, 2026 - PhilHealth eClaims 3.0 becomes mandatory.** All admissions after this date must include electronic SOA in XML format. This creates immediate demand.

---

## 2. Philippine Hospital Pain Points

### 2.1 Long Queues & Manual Registration
- Walk-in culture with no standardized appointment system
- Manual paperwork at every step (registration, vitals, consultation, billing, pharmacy)
- ER overcapacity (some hospitals at 193% occupancy)
- No real-time queue visibility for patients

### 2.2 Paper-Based Records
- Most hospitals maintain paper records with ambivalent digital transition
- Lost or illegible records cause treatment delays
- Records must be retained for 15 years (in-patient) and 10 years (out-patient) per law
- Missing documents are a leading cause of PhilHealth claim denials

### 2.3 Billing & PhilHealth Claims
- Manual eligibility checking, case rate matching, and documentation
- Claims reprocessing described as "costly and time-consuming"
- Delayed reimbursements, denials, and preventable write-offs
- eClaims 3.0 requires XML-format claims with DTD validation

### 2.4 Interdepartmental Communication
- Delays and loss of request slips and charge slips between departments
- Lab, pharmacy, and radiology operate as information silos
- No real-time visibility into orders or results

### 2.5 Appointment Scheduling
- Most hospitals still use walk-in systems
- No patient self-service for appointments
- No automated reminders or follow-up scheduling

---

## 3. Regulatory Requirements

### 3.1 PhilHealth eClaims 3.0 (Mandatory April 1, 2026)
- Electronic SOA in XML format required
- Claims with scanned PDF SOAs will be **rejected**
- Must use PhilHealth-certified HITP software
- XML generation, DTD validation, and secure transmission required

### 3.2 Data Privacy Act (RA 10173)
- Health records = **Sensitive Personal Information** (heightened security)
- Must appoint a Data Protection Officer (DPO)
- Privacy Impact Assessments required
- Encryption, access controls, and audit trails mandatory
- Breach notification to NPC within 72 hours
- Penalties: PHP 500,000 to PHP 5,000,000 + imprisonment up to 6 years

### 3.3 DOH Requirements
- EMR systems must follow DOH data standards for interoperability
- Automated mandated statistical report generation
- Must pass DOH-PhilHealth joint validation testing

### 3.4 Universal Health Care Act (RA 11223)
- Mandates a national eHealth framework
- Requires: e-scheduling, e-consulting, e-appointment, e-prescription, telehealth
- All health facilities required to maintain a HIS consistent with DOH standards

---

## 4. Inspiration: OpenEMR

We are **not forking** OpenEMR. We are building from scratch using a modern stack, but we take inspiration from OpenEMR's proven feature set and workflows. OpenEMR has been battle-tested for over a decade with 4,000+ monthly downloads.

### What we're borrowing (concepts, not code):

| OpenEMR Feature | What We'll Build (Localized for PH) |
|-----------------|--------------------------------------|
| **Scheduling** | Appointment booking with calendar view, recurring appointments, patient self-booking, SMS reminders. Adapted for PH walk-in + appointment hybrid culture |
| **e-Prescribing** | Digital prescriptions with drug database, dosage templates, print-ready Rx format. Using Philippine FDA drug list instead of US NDC codes |
| **Medical Billing** | Charge capture, invoice generation, payment tracking. Built around **PhilHealth case rates** and Senior/PWD discount laws instead of US insurance |
| **CMS Reporting** | Automated report generation. Replaced with **DOH statistical reports** and PhilHealth eClaims 3.0 XML generation |
| **Lab Integration** | Lab order entry, result tracking, normal range flagging. Adapted for common PH lab equipment brands |
| **Clinical Decision Rules** | Alerts for drug interactions, abnormal vitals, overdue follow-ups. Simplified for PH hospital workflows |
| **Advanced Security** | Role-based access, audit trails, encryption. Built to comply with **RA 10173 (Data Privacy Act)** |
| **Multilingual** | **English and Tagalog** support across the entire UI (OpenEMR supports 30+ but we only need 2) |

### What OpenEMR DOESN'T have that we will build:

| Feature | Why It's Critical for PH |
|---------|--------------------------|
| **Queue Management System** | Solves the #1 pain point - long waiting times with no visibility |
| **PhilHealth eClaims 3.0** | Mandatory by April 2026 - XML SOA generation, DTD validation |
| **PhilHealth Member Verification** | Real-time eligibility check against PhilHealth database |
| **Senior/PWD Discount Engine** | Automatic 20% discount computation per RA 9994 and RA 7277 |
| **Queue Display Board** | TV/monitor display for waiting areas showing real-time queue |
| **SMS Notifications** | Queue alerts, appointment reminders, result notifications |
| **Patient Portal (Tagalog)** | Self-service in Filipino language for patients |

---

## 5. Feature Set

### Phase 1 - MVP (Core Modules) — Target: 8-10 weeks

These solve the most critical pain points (queuing, registration, billing, PhilHealth):

#### 5.1 Patient Registration & Records
- Quick registration form (name, birthday, address, contact, PhilHealth ID)
- Patient search (by name, ID, PhilHealth number, contact number)
- Auto-generated patient ID with QR code
- Photo capture (webcam)
- PhilHealth member verification (eligibility check)
- Family/dependent linking
- Patient demographic history
- Document upload (IDs, PhilHealth MDR, etc.)
- **Language: English + Tagalog toggle**

#### 5.2 Queue Management System
- Digital queue number issuance (per department)
- Real-time queue display board (for TV/monitor in waiting area)
- Priority queue: PWD, Senior Citizen, Pregnant (per Philippine law)
- Department-based queuing (Registration → Vitals → Doctor → Billing → Pharmacy)
- Estimated wait time display
- SMS notification when queue number is approaching
- Queue analytics (average wait time, peak hours)
- "Now Serving" display with audio announcement

#### 5.3 OPD (Outpatient Department)
- Doctor's dashboard (today's patients, pending consultations)
- Patient vitals recording (BP, temp, weight, height, pulse, O2 sat)
- SOAP notes (Subjective, Objective, Assessment, Plan)
- Diagnosis entry with ICD-10 code search
- Digital prescription writing with drug search
- Dosage templates (common prescriptions saved)
- Referral generation (to specialist, to lab, to imaging)
- Consultation history timeline
- Print-ready medical certificate, prescription, referral forms

#### 5.4 Billing & Cashier
- Auto-generated charges from consultation, lab, pharmacy orders
- PhilHealth case rate lookup and computation
- Senior Citizen discount (20% per RA 9994) — auto-applied
- PWD discount (20% per RA 7277) — auto-applied
- Payment processing (cash, GCash, card — payment method tracking)
- Official receipt generation (BIR-compliant format)
- Statement of Account (SOA) generation
- Outstanding balance tracking
- Daily cashier summary / shift reports
- Refund and adjustment handling

#### 5.5 PhilHealth eClaims Integration
- eClaims 3.0 XML generation (mandatory April 2026)
- DTD validation before submission
- Electronic SOA with required fields
- Claim status tracking (submitted, approved, denied, reprocessed)
- PhilHealth case rate database (auto-matched to diagnosis)
- Claim form auto-population (CF1, CF2, CF3, CF4)
- Batch claim submission
- Denial reason tracking and resubmission workflow

#### 5.6 User & Access Management
- Role-based access control (Admin, Doctor, Nurse, Cashier, Pharmacist, Lab Tech, Registration Staff)
- Department assignment
- Audit trail (who did what, when — required by Data Privacy Act)
- Session management and auto-logout
- Password policy enforcement
- Activity logs per user

### Phase 2 - V1.0 (Extended Modules) — Target: 6-8 weeks after MVP

#### 5.7 Scheduling & Appointments
- Doctor schedule management (available days, time slots, max patients)
- Patient self-booking (via patient portal or front desk)
- Calendar view (daily, weekly, monthly)
- Recurring appointments (follow-ups)
- SMS/email appointment reminders (1 day before)
- Walk-in vs. appointment tracking
- No-show tracking
- Rescheduling and cancellation

#### 5.8 IPD (Inpatient Department)
- Admission workflow (from ER or OPD)
- Bed/ward management with visual floor map
- Bed availability dashboard
- Daily charges auto-computation (room rate, meds, procedures)
- Nurse notes and vital signs charting (per shift)
- Doctor's orders (medications, labs, diet, activity)
- Discharge summary generation
- Transfer between wards/rooms
- Length of stay tracking

#### 5.9 Pharmacy
- Medicine inventory with batch and expiry tracking
- Prescription fulfillment from doctor's digital Rx
- Stock alerts (low stock, near-expiry)
- Dispensing log with patient receipt
- Drug interaction warnings
- Generic vs. branded tracking (per Generics Act RA 9502)
- Purchase order management
- Supplier directory

#### 5.10 Laboratory
- Lab test ordering (from doctor's consultation)
- Sample collection tracking (with barcode)
- Result entry with normal range flagging
- Auto-alert for critical/abnormal values
- Result templates for common tests (CBC, urinalysis, blood chem)
- Print-ready lab result forms
- Lab workload dashboard
- Test catalog management (prices, turn-around times)

#### 5.11 Inventory Management
- Medical supplies tracking (gauze, syringes, gloves, etc.)
- Reorder level alerts
- Stock in/stock out logging
- Supplier management
- Purchase order generation
- Expiry date tracking
- Department-level consumption tracking

#### 5.12 DOH Reporting
- Automated generation of DOH-mandated statistical reports
- Notifiable disease reporting
- Hospital statistical report (bed occupancy, patient census, morbidity/mortality)
- Data export in DOH-required formats

### Phase 3 - V2.0 (Advanced) — Target: 8-12 weeks after V1.0

#### 5.13 Patient Portal (Web)
- Patient login (phone number + OTP)
- View upcoming appointments and queue status
- View lab results and billing history
- Online payment (GCash, Maya, bank transfer)
- Download medical records / certificates
- Book or reschedule appointments
- **Full Tagalog interface option**

#### 5.14 Analytics Dashboard
- Real-time KPIs: patient volume, revenue, wait times, bed occupancy
- Daily/weekly/monthly trend charts
- Top diagnoses, top procedures, top medications
- PhilHealth claims summary (submitted vs approved vs denied)
- Revenue breakdown (by department, by payment method)
- Staff productivity metrics
- Exportable reports (PDF, Excel)

#### 5.15 Telehealth (Basic)
- Video consultation integration (via Jitsi or similar open-source)
- E-prescription from teleconsult
- Teleconsult billing
- Follow-up scheduling from video call

#### 5.16 HMO Integration
- LOA (Letter of Authorization) processing
- HMO accreditation verification
- HMO-specific billing and claims
- Supported HMOs: Maxicare, Intellicare, Medicard, PhilCare, etc.

#### 5.17 Mobile App (Future)
- Doctor mobile app: patient list, rounds, quick orders
- Patient mobile app: queue status, results, appointments
- React Native or Flutter (cross-platform)

---

## 6. Tech Stack & Architecture

### 6.1 Chosen Stack

| Layer | Technology | Why |
|-------|------------|-----|
| **Frontend** | Next.js 15+ (React) with TypeScript | Modern, fast, SSR for SEO (patient portal), large talent pool |
| **Backend** | Node.js with NestJS (TypeScript) | Same language as frontend, excellent for REST APIs, strong typing |
| **Database** | PostgreSQL 16 | Reliable, handles complex queries, JSON support, free |
| **Cache/Queue** | Redis | Queue management, session caching, real-time updates |
| **Real-time** | WebSocket (Socket.io) | Live queue board updates, real-time notifications |
| **SMS** | Semaphore or Globe Labs API | Philippine SMS providers, affordable bulk SMS |
| **File Storage** | S3-compatible (MinIO or AWS S3) | Patient documents, lab results, receipts |
| **PDF Generation** | Puppeteer or React-PDF | Prescriptions, receipts, lab results, SOA |
| **Deployment** | Docker + Docker Compose | Easy deployment, same setup for dev/prod |
| **Hosting** | VPS (Hetzner/DigitalOcean) or local PH cloud | Cost-effective, data residency option |
| **CI/CD** | GitHub Actions | Automated testing and deployment |
| **Language** | i18next | English + Tagalog translation framework |

### 6.2 Architecture

```
Internet → Nginx (SSL/Reverse Proxy)
  │
  ├── Frontend (Next.js) ─── Port 3000
  │     ├── Staff Portal (hospital employees)
  │     ├── Patient Portal (patients)
  │     └── Queue Display Board (TV/monitors)
  │
  ├── Backend API (NestJS) ─── Port 4000
  │     ├── REST API endpoints
  │     ├── WebSocket server (real-time queue)
  │     ├── PhilHealth eClaims XML engine
  │     └── Report generation engine
  │
  ├── PostgreSQL ─── Port 5432
  │
  ├── Redis ─── Port 6379
  │     ├── Queue state management
  │     ├── Session store
  │     └── Real-time pub/sub
  │
  └── MinIO (S3) ─── Port 9000
        └── File storage (documents, images)
```

### 6.3 Why Build from Scratch

| Factor | Our Custom Build | Forking OpenEMR / ERPNext |
|--------|-----------------|---------------------------|
| **Philippine workflows** | Built for PH from day 1 | Retrofitting US/global system |
| **Tech stack** | Modern TypeScript end-to-end | PHP (OpenEMR) or Python/Frappe (ERPNext) |
| **PhilHealth** | Native integration | Bolted on as afterthought |
| **Queue management** | Core feature | Does not exist |
| **IP ownership** | 100% ours to sell | GPL license restrictions |
| **UX/UI** | Modern, clean, Tagalog-ready | Dated interfaces |
| **Maintenance** | We know every line of code | Fighting someone else's codebase |
| **AI-assisted dev** | Claude Code accelerates everything | Same benefit but with unfamiliar codebase |

---

## 7. Pricing Model & Strategy

### 7.1 Subscription Tiers

#### Tier 1: Klinika (Clinic / Small Practice)
| Item | Details |
|------|---------|
| Target | Clinics, small practices, RHUs, birthing facilities |
| Bed Capacity | 0-25 beds |
| Modules | Patient Registration, OPD, Queue Management, Billing, PhilHealth eClaims, Basic Reports |
| Users | Up to 10 staff accounts |
| Monthly Price | **PHP 8,000/month** |
| Setup Fee | PHP 30,000 (one-time, includes training + data migration) |

#### Tier 2: Ospital (Level 1 Hospital)
| Item | Details |
|------|---------|
| Target | Level 1 hospitals |
| Bed Capacity | 25-75 beds |
| Modules | All Tier 1 + IPD, Pharmacy, Laboratory, Inventory, Appointments, Nurse Notes |
| Users | Up to 30 staff accounts |
| Monthly Price | **PHP 25,000/month** |
| Setup Fee | PHP 80,000 (one-time) |

#### Tier 3: Sentro (Level 2 Hospital)
| Item | Details |
|------|---------|
| Target | Level 2 hospitals |
| Bed Capacity | 75-200 beds |
| Modules | All Tier 2 + Analytics Dashboard, DOH Reporting, Patient Portal, HMO Integration, Multi-department |
| Users | Up to 80 staff accounts |
| Monthly Price | **PHP 75,000/month** |
| Setup Fee | PHP 200,000 (one-time) |

#### Tier 4: Enterprise (Level 3 / Hospital Chain)
| Item | Details |
|------|---------|
| Target | Level 3 tertiary hospitals, hospital networks |
| Bed Capacity | 200+ beds |
| Modules | Full suite + API access, multi-branch, custom integrations, SLA-backed support, telehealth |
| Users | Unlimited staff accounts |
| Monthly Price | **Custom pricing, starting PHP 150,000/month** |
| Setup Fee | Negotiated |

### 7.2 Additional Revenue Streams

| Revenue Stream | Price |
|----------------|-------|
| Extra users (beyond tier limit) | PHP 500/user/month |
| SMS credits (queue + appointment reminders) | PHP 0.50/SMS |
| Custom module development | PHP 50,000 - 300,000/module |
| Integration services (lab equipment, HMO, etc.) | PHP 30,000 - 150,000/integration |
| Data migration from legacy system | PHP 30,000 - 200,000 |
| On-site training (additional sessions) | PHP 8,000/day |
| Priority support SLA | +25% of monthly subscription |

### 7.3 Go-to-Market

1. **30-day free trial** with full Tier 2 features
2. **PhilHealth eClaims 3.0 compliance** as the #1 sales hook (deadline is April 2026)
3. **Transparent published pricing** (competitors are all quote-only)
4. **Target Level 1 hospitals first** (500+ facilities, underserved, shorter sales cycle)
5. **First client = pilot hospital** (discounted or free in exchange for feedback + case study)

---

## 8. Development Timeline & Cost (AI-Assisted)

### 8.1 Development Approach

We are building this with **2 developers + Claude Code (AI-assisted agentic coding)**. This dramatically reduces timeline and cost compared to a traditional 6-7 person team.

**Team:**
- 2 Full-Stack Developers — **PHP 120,000/month total**
- Claude Code (AI coding assistant) — ~PHP 10,000/month

**How Claude Code accelerates development:**
- Generates boilerplate, CRUD operations, API endpoints, database schemas in minutes
- Handles repetitive tasks: form validations, table components, filters, pagination
- Writes tests alongside feature code
- Generates database migrations, seed data, and TypeScript types
- Assists with complex logic: PhilHealth XML generation, billing computations, queue algorithms
- Handles i18n translation structure (English + Tagalog)
- Debugging and refactoring at speed

**What still requires human effort:**
- Architecture decisions and system design
- PhilHealth eClaims specification research and compliance testing
- UI/UX design decisions and user flow mapping
- Hospital workflow observation and requirements validation
- Deployment, server setup, and security hardening
- Client communication, training, and support
- Testing with real hospital staff

### 8.2 Timeline

| Phase | Duration | What Gets Built |
|-------|----------|----------------|
| **Week 1-2** | 2 weeks | Project setup, database schema, auth system, user management, role-based access |
| **Week 3-4** | 2 weeks | Patient registration & records, patient search, QR code generation |
| **Week 5-6** | 2 weeks | Queue management system, real-time queue board (WebSocket), SMS integration |
| **Week 7-8** | 2 weeks | OPD module: doctor's dashboard, vitals, SOAP notes, ICD-10, prescriptions |
| **Week 9-10** | 2 weeks | Billing & cashier: charges, PhilHealth case rates, Senior/PWD discounts, receipts |
| **Week 11-12** | 2 weeks | PhilHealth eClaims 3.0: XML generation, DTD validation, claim forms (CF1-CF4) |
| **Week 13-14** | 2 weeks | Testing, bug fixes, UI polish, Tagalog translations, deployment |
| | | |
| **MVP LAUNCH** | **~3.5 months** | **Registration, Queue, OPD, Billing, PhilHealth, Users** |
| | | |
| **Week 15-16** | 2 weeks | Scheduling & appointments, SMS reminders |
| **Week 17-18** | 2 weeks | IPD: admissions, bed management, nurse notes, discharge |
| **Week 19-20** | 2 weeks | Pharmacy: inventory, dispensing, drug database |
| **Week 21-22** | 2 weeks | Laboratory: test ordering, results, templates |
| **Week 23-24** | 2 weeks | Inventory management, DOH reporting |
| | | |
| **V1.0 LAUNCH** | **~6 months** | **All Phase 1 + Phase 2 modules** |
| | | |
| **Week 25-28** | 4 weeks | Patient portal, analytics dashboard |
| **Week 29-32** | 4 weeks | HMO integration, telehealth (basic) |
| | | |
| **V2.0 LAUNCH** | **~8 months** | **Full platform** |

### 8.3 Cost Breakdown

| Item | Cost (PHP) | Notes |
|------|-----------|-------|
| **2 Developers** | PHP 120,000/month | Full-stack TypeScript devs |
| **Claude Code subscription** | ~PHP 10,000/month | Claude Pro/Team plan |
| **UI/UX design (contract)** | PHP 50,000 - 80,000 | One-time, Figma mockups for key screens |
| **Domain + SSL** | PHP 3,000/year | |
| **Hosting (dev/staging)** | PHP 3,000 - 5,000/month | VPS for development |
| **SMS API credits (testing)** | PHP 5,000 | Semaphore test credits |
| **PhilHealth eClaims testing** | PHP 0 | Free testing environment from PhilHealth |
| **Miscellaneous** | PHP 20,000 | Tools, licenses, contingency |

**Monthly burn rate: ~PHP 135,000** (2 devs + Claude Code + hosting)

#### Total Cost to MVP (~3.5 months)

| Item | PHP |
|------|-----|
| 2 Developers (3.5 months) | 420,000 |
| Claude Code (3.5 months) | 35,000 |
| UI/UX design | 50,000 - 80,000 |
| Hosting & infra | 15,000 - 20,000 |
| Misc | 25,000 |
| **Total MVP** | **PHP 545,000 - 580,000** |

#### Total Cost to V1.0 (~6 months)

| Item | PHP |
|------|-----|
| 2 Developers (6 months) | 720,000 |
| Claude Code (6 months) | 60,000 |
| Hosting & infra | 25,000 - 35,000 |
| Misc | 15,000 |
| **Total V1.0** | **PHP 820,000 - 830,000** |

#### Total Cost to V2.0 (~8 months)

| Item | PHP |
|------|-----|
| 2 Developers (8 months) | 960,000 |
| Claude Code (8 months) | 80,000 |
| Hosting & infra | 35,000 - 50,000 |
| Misc | 15,000 |
| **Total V2.0** | **PHP 1,090,000 - 1,105,000** |

### 8.4 Traditional Team vs AI-Assisted Comparison

| Metric | Traditional (6-7 person team) | AI-Assisted (2 devs + Claude Code) |
|--------|-------------------------------|----------------------------------|
| MVP timeline | 7-11 months | **~3.5 months** |
| MVP cost | PHP 2.75M - 6.8M | **~PHP 560K** |
| V2.0 timeline | 14-21 months | **~8 months** |
| V2.0 cost | PHP 5.5M - 13.5M | **~PHP 1.1M** |
| Monthly burn | PHP 350K - 650K | **~PHP 135K** |
| Risk | High (team coordination) | Lower (small team, consistent codebase) |

### 8.5 Post-Launch Operating Costs

| Item | Monthly (PHP) |
|------|---------------|
| Production hosting (1-10 hospitals) | 5,000 - 15,000 |
| SMS credits | 2,000 - 10,000 |
| Claude Code (ongoing maintenance) | 10,000 |
| 2 Developers (maintenance + support + new features) | 120,000 |
| **Total monthly operating** | **PHP 137,000 - 155,000** |

### 8.6 Break-Even Projection

With monthly operating costs of ~PHP 145,000 and average revenue of PHP 25,000/hospital/month:

| Hospitals | Monthly Revenue | Monthly Profit | Months to Recover MVP Cost (~560K) |
|-----------|----------------|----------------|-------------------------------------|
| 5 hospitals | PHP 125,000 | -PHP 20,000 | Not yet profitable |
| 6 hospitals | PHP 150,000 | PHP 5,000 | ~112 months (break-even point) |
| 8 hospitals | PHP 200,000 | PHP 55,000 | ~10 months |
| 10 hospitals | PHP 250,000 | PHP 105,000 | ~5 months |
| 15 hospitals | PHP 375,000 | PHP 230,000 | ~2.5 months |
| 20 hospitals | PHP 500,000 | PHP 355,000 | ~1.5 months |

**Break-even: ~6 paying hospitals** (achievable within 6-12 months of launch).
**Comfortable profit starts at 8-10 hospitals.**

---

## 9. Competitive Landscape

### 9.1 Existing Philippine HIS Providers

| Provider | Type | Target | Strengths | Weaknesses |
|----------|------|--------|-----------|------------|
| **Bizbox** | On-premise | All levels, 3,000+ customers | Market leader, PhilHealth certified, 25+ years | Legacy UI, expensive (PHP 800K+ setup), quote-only |
| **COMLOGIK** | On-premise | Hospitals, 200+ since 1999 | Established, comprehensive | Legacy tech, long implementation |
| **KCCI Medsys** | On-premise | Hospitals, clinics | Integrated solution | Dated interface, on-premise only |
| **Agimat Health** | Cloud | Level 1-3 | Cloud-native, modern, fast deploy | New entrant, unproven at scale |
| **SeriousMD** | Cloud/SaaS | Doctors, small clinics | Modern, affordable, telemedicine | Not for full hospital management |
| **iHOMIS** | On-premise | Government hospitals | Free (DOH-provided), 56% gov adoption | Dated, limited features, government-only |

### 9.2 Our Competitive Advantages

1. **Cloud-native** - no server hardware needed at hospital
2. **Modern UX** - clean web UI, mobile-responsive, Tagalog support
3. **Transparent pricing** - published tiers starting at PHP 8,000/month
4. **Low entry cost** - PHP 30K setup vs. PHP 800K-2M from competitors
5. **Queue management** - built-in, solves the #1 patient complaint
6. **PhilHealth eClaims 3.0** - compliant from day one
7. **Fast deployment** - days, not months
8. **Patient portal** - self-service appointments, results, payments in Tagalog

---

## 10. Next Steps

### Immediate Actions
- [ ] Review this document with client
- [ ] Identify the target hospital (first potential client) and their exact workflow
- [ ] Visit the hospital to observe registration, billing, and queue flow
- [ ] Begin UI/UX design for MVP screens
- [ ] Set up project repository and development environment

### Questions for Client Meeting
1. What type of hospital is the first target? (Level 1, 2, or 3? Government or private?)
2. How many beds? How many daily patients (OPD + ER)?
3. What system do they currently use? (Paper? iHOMIS? Bizbox? Custom?)
4. Are they PhilHealth-accredited? Do they currently submit eClaims?
5. What is their #1 pain point? (Queue? Billing? Records? PhilHealth?)
6. What is their budget range?
7. Do they have existing IT infrastructure? (Computers at stations? Network? Internet?)
8. How many staff would use the system?
9. Are they open to cloud-based, or do they require on-premise?
10. When do they need the system operational?

### After Client Feedback
- [ ] Lock MVP feature scope based on client priorities
- [ ] Finalize pricing for first client (pilot deal)
- [ ] Start development sprint 1

---

## Appendix: Market Opportunity

- Philippine eHealth market: **USD 3.1 billion (2025)**, growing at **15.9% CAGR** to **USD 8.7 billion by 2032**
- Total hospitals: ~1,351 (65% private, 35% government)
- Level 1 hospitals (primary target): **~500+ facilities** mostly without modern IT systems
- PhilHealth eClaims 3.0 deadline (April 2026) creates **urgent demand wave**

---

*This document is a living document. Updated after client meetings and as requirements are clarified.*
