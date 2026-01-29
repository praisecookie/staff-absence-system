# Staff Absence & Cover Management System

You need to understand TypeScript/JavaScript to reuse this system.  
**Status:** To be updated by whoever wants to use it.  
**Version:** 0.0.1

## 📖 Overview

This is a multi-tenant SaaS platform designed for Schools and Multi-Academy Trusts (MATs) to manage staff attendance, sickness, and cover requirements.

The system features a **Hierarchical Architecture**:

1.  **Trust Level (MAT):** Oversees multiple schools, monitors risk, and manages high-level interventions.
2.  **School Level:** Principals and HR manage daily staff absences and operational health.
3.  **Staff Level:** Individual teachers report absences, view wellbeing, and manage their return-to-work flow.

## 🛠 Technical Stack

### Frontend & Application Logic

- **Framework:** [Next.js 14+](https://nextjs.org/) (App Router)
- **Language:** TypeScript, JavaScript
- **Styling:** Tailwind CSS
- **Icons:** Lucide React
- **State Management:** React Hooks (`useState`, `useEffect`)

### Backend & Database

- **BaaS (Backend as a Service):** [Supabase](https://supabase.com/)
- **Database:** PostgreSQL
- **Authentication:** Supabase Auth (Email/Password)
- **Storage:** Supabase Storage (for document evidence)

## ✨ Key Features

### 🏢 For Multi-Academy Trusts (MATs)

- **Trust Dashboard:** Aggregate view of all schools, total staff, and absence rates.
- **Risk Watchlist:** Automated flagging of schools with critical absence levels (>10%).
- **Intervention Management:** Schedule physical or virtual reviews with struggling schools.
- **School Directory:** CRUD operations to add, edit, or remove schools from the trust.
- **Trust Profile:** Manage trust HQ details and contact info.

### 🏫 For Schools (Principals, HR, Cover Managers)

- **Operational Dashboard:** Real-time view of "Who's off today" and "Cover Needed".
- **Staff Directory:** Manage school employees and assign roles.
- **Cover Management:** Assign cover supervisors to absent classes.
- **Absence Reporting:** Log sickness or leave on behalf of staff (Proxy).
- **Return to Work:** Process RTW interviews and close absence records.

### 👩‍🏫 For Staff

- **Self-Service Portal:** Report absence (Sickness/Leave).
- **Wellbeing Pulse:** Weekly mood and stress check-ins.
- **My History:** View past absences and remaining leave balance.

## 🚀 How to Run (Developer Instructions)

### 1. Prerequisites

- Node.js (v18.0.0 or later)
- npm or yarn
- A Supabase project (for the database URL and Anon Key)

### 2. Installation

Clone the repository and install dependencies:

```bash
git clone [https://github.com/your-repo/staffabsence.git](https://github.com/your-repo/staffabsence.git)
cd braydenhq
npm install
```

### 3. Environment Variables

Create a .env.local file in the root directory and add your Supabase credentials:

```Bash
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### 4. Database Setup

Ensure your Supabase PostgreSQL database has the following core tables:

- `mats`: Stores Trust entities.
- `schools`: Stores School entities (linked to `mat_id`).
- `staff`: Stores Users (linked to `school_id` OR `mat_id`).
- `absence_records`: Stores sickness/leave data.
- `wellbeing_entries`: Stores weekly pulse check data.

### 5. Start the Development Server

```Bash
npm run dev
```

Open http://localhost:3000 with your browser to see the result.

## 📂 Project Structure

        /app
        /cover       # Cover Manager Dashboard & Logic
        /request     # Absence Request Logic (Princewill Protocol)
        /schools     # MAT School Directory (CRUD)
        /settings    # Traffic Controller for Profile/Settings
        /tasks       # Traffic Controller for School/MAT Tasks
        page.tsx     # Main Dashboard Traffic Controller
        layout.tsx   # Global Layout (Sidebar + Shell)

        /components
        /dashboard   # MatDashboard.tsx, SchoolDashboard.tsx
        /layout      # Sidebar.tsx, AppShell.tsx
        /settings    # MatProfile.tsx, SchoolSettings.tsx
        /tasks       # MatTasks.tsx, SchoolTasks.tsx

        /lib
        supabase.ts  # Supabase Client Initialization

## 📝 Notes

**Role Logic:** The system uses a "Traffic Controller" pattern in page.tsx and the Sidebar to dynamically serve content based on the system_role ('MAT_Admin', 'Principal', 'HR', 'Staff').

**Attendance Calculation:** Absence rates are currently calculated based on active absence records vs total staff count.

**Authentication:** The system relies on Supabase Auth. Ensure RLS (Row Level Security) policies are enabled in Supabase for production to prevent cross-school data leaks.

**Permissions:** Row Level Security (RLS) policies should be enabled in Supabase for production to prevent cross-school or cross-trust data access.

#

_You can reuse this system structure if you are building something similar._
