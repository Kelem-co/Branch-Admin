<div align="center">
  <img src="./public/logo.svg" alt="Kelem Branch Admin" width="160" height="160">
  <br><br>
  <h1>Kelem Branch-Admin Dashboard</h1>
  <p><em>Branch administration dashboard for the Kelem platform</em></p>
  <br>
  <p>
    <strong>Course:</strong> Software Engineering Final Year Project<br>
    <strong>Institution:</strong> Addis Ababa Science and Technology University
  </p>
  <br>
  <p>
    <strong>Collaborators:</strong><br>
    <a href="https://github.com/fitiha">fitiha</a> ·
    <a href="https://github.com/NahomTesM">NahomTesM</a> ·
    <a href="https://github.com/oddegen">oddegen</a> ·
    <a href="https://github.com/RobelD420">RobelD420</a> ·
    <a href="https://github.com/Tonetor777">Tonetor777</a>
  </p>
</div>

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Technology Stack](#technology-stack)
4. [Architecture](#architecture)
5. [Project Structure](#project-structure)
6. [Getting Started](#getting-started)
7. [Development](#development)
8. [Backend Integration](#backend-integration)

---

## Project Overview

Kelem Branch Admin is a Next.js administrative dashboard for branch-level school operations. It gives branch administrators one place to manage students, parents, teachers, academic setup, attendance, announcements, calendar events, and bulk record imports.

The app uses the Next.js App Router as a lightweight shell, then mounts a client-side dashboard experience that switches between modules without full page reloads. It is designed to work against a Django/DRF backend using JWT authentication.

---

## Features

| Module | Description |
|---|---|
| **Dashboard** | Operational summary cards, attendance and performance visuals, upcoming events, and quick visibility into branch health. |
| **Parents** | Parent directory, profile editing, linked-student visibility, invite flows, and parent relationship management. |
| **Students** | Student directory, add/edit flows, section assignment, parent linkage, media upload support, and batch import helpers. |
| **Teachers** | Teacher listing, assignment visibility, homeroom mapping, invitation flow, status-aware filtering, and bulk invite/import actions. |
| **Academia** | Grade, section, subject, and role management tied to branch and academic-year context. |
| **Attendance** | Attendance dashboards and branch-wide attendance monitoring by academic year. |
| **Announcements** | Draft, schedule, send, search, filter, and target branch announcements with optional media attachments. |
| **Academic Calendar** | Branch calendar management for school events and academic planning. |
| **Batch Import** | Bulk upload workflow for student, parent, and teacher records with progress polling and validation feedback. |
| **Invitation Activation** | Dedicated account activation pages for branch admins and teachers using secure tokenized invitation links. |

---

## Technology Stack

| Layer | Technology |
|---|---|
| Framework | Next.js |
| UI Library | React 19 |
| Language | TypeScript 5 |
| Styling | Tailwind CSS 4 |
| Animation | Motion |
| Charts | Recharts |
| Icons | Lucide React |
| API Layer | Native Fetch wrapper in `src/lib/api.ts` |
| Auth | JWT access/refresh flow |
| File Uploads | Browser media client with queued upload helpers |
| Formatting | Prettier |

---

## Architecture

### Application Flow

The application is split into a thin App Router shell and a client-rendered admin dashboard:

```text
app/page.tsx
└── app/client-app.tsx
    └── src/App.tsx
        ├── Authentication bootstrap
        ├── Branch + academic year context loading
        ├── Sidebar / header layout
        └── Module rendering
            ├── Dashboard
            ├── Parents
            ├── Students
            ├── Teachers
            ├── Academia
            ├── Attendance
            ├── Announcements
            ├── Academic Calendar
            └── Batch Import
```

### Key Design Choices

- The App Router is used for shell routes and invitation flows, while the main admin experience is a client-side SPA mounted from `src/App.tsx`.
- JWT tokens are managed in the frontend and used for authenticated requests to the backend.
- Branch, organization, and academic-year context are loaded once after login and passed down to feature modules.
- Shared API utilities centralize error formatting, pagination types, auth refresh behavior, and media upload support.

---

## Project Structure

```text
app/
├── layout.tsx
├── page.tsx
├── client-app.tsx
├── complete-invitation/[uid]/[token]/page.tsx
└── complete-teacher-invitation/[uid]/[token]/page.tsx

src/
├── App.tsx
├── components/
│   ├── Dashboard.tsx
│   ├── Parents.tsx
│   ├── Students.tsx
│   ├── Teachers.tsx
│   ├── Academia.tsx
│   ├── AttendanceDashboard.tsx
│   ├── Announcements.tsx
│   ├── AcademicCalendar.tsx
│   ├── BatchImport.tsx
│   └── shared layout and upload components
├── hooks/
│   ├── data-fetching hooks for students, parents, teachers, grades, sections, and attendance
├── lib/
│   ├── api.ts
│   └── media/
├── constants/
│   └── mockData.ts
├── types.ts
└── index.css
```

---

## Getting Started

### Prerequisites

- Node.js 20 or later
- npm

### Installation

```bash
git clone git@github.com:Kelem-co/Branch-Admin.git
cd Branch-Admin
npm install
```

### Environment Setup

Create a local environment file:

```bash
cp .env.example .env.local
```

Required variable:

```env
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000
```

---

## Development

### Run Locally

```bash
npm run dev
```

The app runs on [http://localhost:3000](http://localhost:3000).

### Build for Production

```bash
npm run build
```

### Start Production Build

```bash
npm run start
```

### Type Check

```bash
npm run typecheck
```

### Lint Workflow

```bash
npm run lint
```

This runs `next typegen` and `tsc --noEmit --incremental false`.

---

## Backend Integration

The frontend is built to communicate with a Django/DRF backend through [`src/lib/api.ts`](./src/lib/api.ts).

### Expected Auth Flow

- Users sign in with JWT credentials.
- Access and refresh tokens are stored client-side and refreshed when needed.
- The current branch-admin profile is resolved after authentication.
- Branch, organization, and academic-year context are then used across modules.

### Backend-Driven Areas

- User authentication and session refresh
- Branch admin profile lookup
- Students, parents, teachers, grades, sections, and assignments
- Attendance and academic-year data
- Announcements and targeting criteria
- Bulk import jobs and import status polling
- Media upload and attachment lifecycle

### Important Note

Without a valid backend base URL and compatible API responses, the authenticated modules will not function correctly.
