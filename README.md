<div align="center">

# Music Production and Management Platform

### A full-stack platform for a gospel music ministry — music and video streaming, event bookings, a choir, donations, paid music sheets, and administrative operations, unified in one system.
**Live :** [Visit the Platform](https://obiblomusic.com/)

![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/Relational_DB-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-3448C5?style=for-the-badge&logo=cloudinary&logoColor=white)
![Paystack](https://img.shields.io/badge/Paystack-00C3F7?style=for-the-badge&logo=paystack&logoColor=white)
![Google Drive](https://img.shields.io/badge/Google_Drive_Backup-4285F4?style=for-the-badge&logo=googledrive&logoColor=white)
![Mailjet](https://img.shields.io/badge/Mailjet-FF6B6B?style=for-the-badge&logo=mailjet&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![Composer](https://img.shields.io/badge/Composer-885630?style=for-the-badge&logo=composer&logoColor=white)

</div>

---
> [!NOTE]
> This repository is a public case study of my work on the platform. It does **not** contain the application's proprietary source code, credentials, private user data, or other confidential information belonging to Peterfleming Arts Limited.
---

## Table of Contents

1. [Project Overview](#project-overview)
2. [My Role](#my-role)
3. [Platform Architecture](#platform-architecture)
4. [Core Platform Areas](#core-platform-areas)
5. [Domain Model](#domain-model)
6. [Administrative Panel](#administrative-panel)
7. [Authentication, Authorization & Activity Tracking](#authentication-authorization--activity-tracking)
8. [Application Structure & Service Layer](#application-structure--service-layer)
9. [Background Jobs & Notifications](#background-jobs--notifications)
10. [Automated Console Commands](#automated-console-commands)
11. [Media & File Management](#media--file-management)
12. [Payments & Donations](#payments--donations)
13. [Automated Testing](#automated-testing)
14. [Deployment & CI/CD](#deployment--cicd)
15. [Security Considerations](#security-considerations)
16. [Third-Party Integrations](#third-party-integrations)
17. [Technology Stack](#technology-stack)
18. [Notable Laravel Architecture](#notable-laravel-architecture)
19. [Resource-Oriented Admin Architecture](#resource-oriented-admin-architecture)
20. [Engineering Highlights](#engineering-highlights)
21. [Project Screenshots](#project-screenshots)
22. [Recommended Technical Diagrams](#recommended-technical-diagrams)
23. [What This Project Demonstrates](#what-this-project-demonstrates)
24. [Confidentiality & Portfolio Disclaimer](#confidentiality--portfolio-disclaimer)
25. [Public Repository Safety Checklist](#public-repository-safety-checklist)
26. [Project Information](#project-information)

---

## Project Overview

**Obiblo Music** is a gospel music ministry built around production, recording, and live performance. Their operations span:

| Area | Description |
|---|---|
| Music Production & Recording | In-house production and recording services |
| Gospel Performance | The ministry performs gospel music themselves, including as a choir |
| Event Bookings (Performance) | Bookings to travel and perform/sing at an event |
| Event Bookings (Recording Only) | Bookings to attend and record an event without performing |
| Music & Video Streaming | Catalog of audio and video content shared via the platform |
| Music Sheets | Original compositions, some free and some paid |
| Donations | Online giving from supporters |

The platform centers on **music events** — bookings, releases, and ministry activity — supported by a full administrative back office.

Rather than a simple content site, the application is a **ministry operations platform**: it manages bookings, media, payments, donations, and audience engagement behind a public-facing experience.

---

## My Role

**Role:** Software Engineer / Lead Developer

I was responsible for the design, development, testing, deployment, and ongoing technical management of the platform.

| Category | Responsibilities |
|---|---|
| Architecture & Data | Application architecture, database design, migrations |
| Backend Development | Laravel backend development, service-layer design, request validation |
| Access Control | Authentication, authorization guards, admin role management |
| Feature Development | Booking system, media catalog, music sheet store, event management, donations |
| Payments | Paystack payment gateway integration |
| Communications | Booking and contact notifications, transactional email |
| Infrastructure | Cloud media storage, automated database backups, CI/CD deployment |
| Quality Assurance | Automated feature and unit test suite, CI-gated deployments |
| Operations | Scheduled jobs, sitemap generation, production maintenance |

---

## Platform Architecture

The platform combines a public-facing ministry website with an authenticated administrative back office.

<p align="center">
  <img src="images/architecture.png" alt="Architecture" width="60%">
</p>
---

## Core Platform Areas

### 1. Music & Video Library

The platform maintains a media library of the ministry's audio and video work.

- Audio content is linked to external streaming platforms — **Spotify** and **Audiomack** — rather than hosted directly, and can also be streamed on-site via embedded players (iframes)
- Video content is linked similarly to **YouTube**
- Audio and video entries can be associated with music sheets where applicable
<p align="center">
  <img src="images/media.png" alt="Architecture" width="45%">
  <img src="images/video.png" alt="Architecture" width="45%">
</p>

---

### 2. Music Sheets

The ministry composes original music sheets, which can be offered for free or sold individually.

- Each music sheet can include composer details and descriptive information
- Music sheets can be linked to an existing audio entry
- Paid music sheets are gated behind the Paystack payment flow

```text
Music Sheet Created
      ↓
Marked Free or Paid
      ↓
Linked to Audio (optional)
      ↓
Published
      ↓
User Requests Access
      ↓
Free? → Immediate Access
Paid? → Paystack Checkout → Access Granted
```
<p align="center">
  <img src="images/sheet.png" alt="Music Sheet" width="45%">
  <img src="images/sheet2.png" alt="Music Sheet" width="45%">
</p>

---

### 3. Event Bookings

Users can book the ministry for two distinct kinds of engagements:

| Booking Type | Description |
|---|---|
| **Performance Booking** | The ministry travels to perform/sing at the event |
| **Recording-Only Booking** | The ministry attends solely to record the event, without performing |

Booking submissions are recorded and trigger a notification workflow to the ministry.

<p align="center">
  <img src="images/book.png" alt="Booking" width="45%">
  <img src="images/book2.png" alt="Booking" width="45%">
</p>

---

### 4. Events

The ministry can publish its own events, such as tours, where the public can register — whether the event is free or requires registration to attend.

<p align="center">
  <img src="images/eventobi.png" alt="Event" width="60%">
</p>

---

### 5. Donations

Supporters can give directly to the ministry online through an integrated Paystack donation flow.

```text
Donor
  ↓
Donation Form
  ↓
Paystack Checkout
  ↓
Payment Verified
  ↓
Donation Record
  ↓
Payment Record
```

<p align="center">
  <img src="images/donation.png" alt="Donations" width="60%">
</p>

---

### 6. Visitor Tracking

The platform tracks anonymous visitors using browser fingerprinting rather than personal or demographic data.

This allows an anonymous visitor — for example, someone who donates or downloads content without creating an account — to later claim their activity record if they choose to register. Actions performed during an anonymous session are associated with the visitor's fingerprint and can be linked to a registered account afterward.

---

## Domain Model

| Domain Group | Models |
|---|---|
| Core | Admin, User, Visitor |
| Media | Audio, Video |
| Ministry Activity | Booking, Event |
| Commerce & Giving | Donation, Payment |

| Model | Purpose |
|---|---|
| **Admin** | Different administrative account types (Super Admin, Regular Admin, Moderator) |
| **Audio** | Music entries linked to Spotify/Audiomack, streamable on-site via embedded players |
| **Video** | Video entries linked to YouTube |
| **Booking** | Requests to book the ministry to perform or to record an event |
| **Event** | Ministry-published events (e.g. tours) with open or registration-based attendance |
| **Donation** | Records of donations made through the platform |
| **Payment** | Tracks payment transactions across donations and paid music sheets |
| **User** | Registered platform users |
| **Visitor** | Anonymous visitors tracked via browser fingerprint, with no demographic data collected |

<p align="center">
  <img src="images/erd.png" alt="Entity Relationship Diagram" width="60%">
</p>

---

## Administrative Panel

The administrative panel is the operational core of the platform.

| Section | Purpose |
|---|---|
| **Dashboard** | Summary and overview of the system |
| **Music Sheets** | Create/manage music sheets, set free or paid status and pricing, link to audio |
| **Audio** | Manage audio entries and streaming links |
| **Video** | Manage video entries and streaming links |
| **Bookings** | Manage incoming performance and recording booking requests |
| **Events** | Manage ministry-published events |
| **Donation Tracking** | View and track donations received |
| **Payment History** | Real-time view of payment transactions processed via Paystack |
| **Registered Users** | View users who created accounts on the platform |
| **Guest/Visitor Users** | View anonymous visitor activity (fingerprint-based, no demographic data) |
| **Staff/Admin Management** | Super Admin can add other administrators and assign them a role |

Most resources follow the same CRUD pattern — **Index**, **Create**, **Edit**, and **Show** pages.

<p align="center">
  <img src="images/dashboard.png" alt="Dashboard" width="60%">
</p>

---

## Authentication, Authorization & Activity Tracking

The platform separates normal users from administrative users through distinct authentication guards, consistent with the ministry's earlier institutional projects.

```text
                    Application
                         │
              ┌──────────┴──────────┐
              │                     │
         Web Guard             Admin Guard
              │                     │
        Normal Users          Administrators
```

### Role-Based Authorization

| Role | Access Level |
|---|---|
| **Super Admin** | Full administrative access; can add other administrators and assign their role |
| **Regular Admin** | Broad administrative access to permitted resources |
| **Moderator** | Restricted administrative access |

Authorization policies are used throughout the admin panel, and administrative actions are tracked so that activity within the system can be reviewed.

---

## Application Structure & Service Layer

The codebase follows a layered structure that keeps controllers thin:

| Layer | Responsibility |
|---|---|
| **Controllers** | Handle HTTP requests and coordinate workflows |
| **Requests** | Handle form validation separately from controllers |
| **Services** | Encapsulate business logic outside of controllers |
| **Middleware** | Custom middleware handled in its own dedicated layer |
| **Policies** | Enforce resource-level authorization |
| **Models** | Represent domain entities and relationships |
| **Migrations** | Version and manage database structure |

---

## Background Jobs & Notifications

| Component | Purpose |
|---|---|
| **Database Backup Listener** | A queued job that backs up the database and uploads it to Google Drive |
| **Booking Notification** | Notifies the ministry when a user submits a booking |
| **Message Notification** | Notifies the ministry when a user sends a message |

```text
Booking / Message Submitted
      ↓
Event Fired
      ↓
Notification Dispatched
      ↓
Ministry Notified
```

```text
Backup Triggered
      ↓
Queued Job
      ↓
Database Export
      ↓
Upload to Google Drive
```
---

## Automated Console Commands

| Command | Purpose |
|---|---|
| **Generate Sitemap** | Regenerates the site's sitemap and writes it to the public folder |

The sitemap command runs automatically as part of the CI/CD deployment pipeline whenever a new page or update is deployed, keeping the sitemap current so Google Search Console can index the site accurately.

```text
Deployment Triggered
      ↓
Generate Sitemap Command
      ↓
sitemap.xml Updated in Public Folder
      ↓
Google Search Console Indexing
```

---

## Media & File Management

The platform uses **Cloudinary** for image storage. Audio and video content are not hosted directly — they are linked to **Spotify** and **Audiomack** (audio) and **YouTube** (video), and can be streamed on-site through embedded players.

---

## Payments & Donations

**Paystack** is integrated as the platform's payment gateway, used for:

- Donations
- Paid music sheet purchases

The **Payment** model tracks transactions across both use cases, and the admin panel provides a real-time payment history view.

---

## Automated Testing

A dedicated CI workflow (`test.yaml`) runs the automated test suite before deployment, covering both feature and unit tests.

| Test Type | Coverage |
|---|---|
| Login | Simulated login flows |
| Registration | New user registration |
| Email Verification | Verification flow correctness |
| Forgot Password / Reset | Password reset flow |
| Protected Route Access | Confirms guests cannot access protected routes |

```text
Push / Pull Request
      ↓
test.yaml (CI)
      ↓
Feature & Unit Tests
      ↓
Pass → Proceed to Deployment
Fail → Deployment Blocked
```
---

## Deployment & CI/CD

Deployment follows the same automated shared-hosting pipeline used across the ministry's projects, with an added testing gate beforehand.

The deployment workflow handles:

- Running the automated test suite (`test.yaml`) before deployment proceeds
- Deploying application files via FTP
- Executing deployment commands through SSH
- Installing Composer dependencies
- Running database migrations
- Generating the sitemap

```text
Developer
    │
    ▼
Git Repository
    │
    ▼
GitHub Actions
    │
    ├── test.yaml → Run Test Suite
    │
    ├── FTP Deployment
    │
    └── SSH Commands
          │
          ├── Composer Dependencies
          ├── Database Migrations
          └── Generate Sitemap
                    │
                    ▼
             Shared Hosting
                    │
                    ▼
              Production App
```
---

## Third-Party Integrations

| Service / Technology | Purpose |
|---|---|
| Cloudinary | Image storage |
| Spotify / Audiomack | Audio streaming |
| YouTube | Video streaming |
| Paystack | Payment gateway for donations and music sheet purchases |
| Google / Laravel Socialite | Google authentication |
| Google Drive | Periodic automated database backups |
| Mailjet | Transactional email delivery |
| GitHub Actions | CI/CD automation and automated testing |
| Shared Hosting + SSH | Production hosting and server operations |

---

## Technology Stack

<div align="left">

![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat-square&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/Relational_DB-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-3448C5?style=flat-square&logo=cloudinary&logoColor=white)
![Paystack](https://img.shields.io/badge/Paystack-00C3F7?style=flat-square&logo=paystack&logoColor=white)
![Google Drive](https://img.shields.io/badge/Google_Drive-4285F4?style=flat-square&logo=googledrive&logoColor=white)
![Mailjet](https://img.shields.io/badge/Mailjet-FF6B6B?style=flat-square&logo=mailjet&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Composer](https://img.shields.io/badge/Composer-885630?style=flat-square&logo=composer&logoColor=white)
![SSH](https://img.shields.io/badge/SSH-000000?style=flat-square&logo=gnu-bash&logoColor=white)

</div>

| Layer | Technologies |
|---|---|
| **Backend** | PHP, Laravel, Eloquent ORM, Laravel Authentication & Authorization, Laravel Policies, Laravel Notifications, Queued Jobs |
| **Frontend** | Server-rendered Laravel views |
| **Database** | Relational database architecture, Laravel migrations |
| **Testing** | Automated feature and unit test suite, CI-gated via `test.yaml` |
| **Infrastructure & DevOps** | Shared hosting, SSH, FTP-based deployment, GitHub Actions, Composer |
| **External Services** | Cloudinary, Paystack, Spotify, Audiomack, YouTube, Google Drive, Mailjet |

---

## What This Project Demonstrates

| Category | Skills Demonstrated |
|---|---|
| Backend Engineering | Laravel application architecture, PHP backend development, service-layer architecture |
| Data | Relational database design, Eloquent ORM |
| Access Control | Authentication, authorization, Laravel policies, multiple authentication guards, role-based access control |
| Application Structure | Request-based validation, dedicated middleware layer, CRUD resource architecture |
| Quality Assurance | Automated feature and unit testing, CI-gated deployments |
| Payments | Third-party payment gateway integration (Paystack) for commerce and donations |
| Media Strategy | Integrating third-party streaming platforms (Spotify, Audiomack, YouTube) instead of self-hosting media |
| Privacy-Aware Design | Fingerprint-based anonymous visitor tracking without demographic data collection |
| DevOps | CI/CD, automated testing gates, shared-hosting deployment, SSH server operations, GitHub Actions |
| Automation | Scheduled database backups, automated sitemap generation for SEO |

---

## Project Information

| Category | Details |
|---|---|
| **Organization** | Obiblo Music |
| **Project Type** | Ministry Operations & Digital Experience Platform |
| **Backend** | Laravel / PHP |
| **Database** | Relational Database |
| **Media Storage** | Cloudinary (images); Spotify, Audiomack & YouTube (streaming) |
| **Payments** | Paystack |
| **Email** | Mailjet |
| **Backups** | Google Drive (automated, queued) |
| **Authentication** | Laravel Authentication / Google Social Login |
| **Testing** | Automated feature & unit test suite (CI-gated) |
| **Deployment** | Shared Hosting |
| **CI/CD** | GitHub Actions |
| **Server Access** | SSH |
| **Deployment Method** | FTP + SSH |
| **Source Code** | Private / Proprietary |

---

<div align="center">

**Built to connect ministry, music, and community through one digital platform.**

</div>
