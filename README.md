# AtomQuest — Goal Setting & Tracking Portal

> Built for **AtomQuest Hackathon 1.0** · A fully functional, role-based employee goal management portal shipped as a single HTML file — no backend, no framework, no build step.

🔗 **Live Demo:** [atomquestt-pi.vercel.app](atomquestt-pi.vercel.app)

---

## Problem Statement

Organizations relying on manual or fragmented goal-tracking methods struggle with alignment, visibility, and accountability. Spreadsheets and offline review cycles create blind spots — managers can't monitor team progress in real time, employees lack clarity on how their work connects to organizational priorities, and HR teams are left piecing together data at appraisal time.

**AtomQuest** solves this by providing a structured, digital Goal Setting & Tracking Portal that supports the full lifecycle of employee goals — from creation and alignment to quarterly check-ins and performance visibility — while being intuitive, reliable, and audit-ready.

---

## Demo Credentials

| Role | Email | Password |
|---|---|---|
| Employee | alice@company.com | demo1234 |
| Manager | bob@company.com | demo1234 |
| Admin | carol@company.com | demo1234 |

> You can also use the **Microsoft Entra ID (SSO)** button on the login screen.

---

## Features

### ✅ Phase 1 — Goal Creation & Approval

- Employee interface to create and submit a Goal Sheet
- Select **Thrust Area** and define goal title, description, and UoM type (Numeric Min/Max, Percentage, Timeline, Zero)
- Set targets and weightage per goal with system-enforced validation:
  - Total weightage across all goals must equal **100%**
  - Minimum weightage per goal: **10%**
  - Maximum goals per employee: **8**
- **Manager (L1) Approval Workflow** — review, inline edit targets/weightages, return for rework, or approve and lock
- **Shared Goals** — admin/manager can push a departmental KPI to multiple employees; recipients adjust weightage only; achievement by the primary owner syncs across all linked sheets

### ✅ Phase 2 — Achievement Tracking & Quarterly Check-ins

- Quarterly update interface for employees to log actual achievement vs. planned targets
- Status selection per goal: **Not Started / On Track / Completed**
- **Manager Check-in module** — view planned vs. actual for each team member; add structured check-in comments
- System-computed progress scores by UoM type:

| UoM Type | Description | Formula |
|---|---|---|
| Min (Numeric / %) | Higher is better (e.g. Sales Revenue) | Achievement ÷ Target |
| Max (Numeric / %) | Lower is better (e.g. TAT, Cost) | Target ÷ Achievement |
| Timeline | Date-based completion | Completion date vs. Deadline |
| Zero | Zero = Success (e.g. Safety incidents) | If 0 → 100%, else 0% |

### ✅ Check-in Schedule

| Period | Window Opens | Action |
|---|---|---|
| Goal Setting | 1st May | Goal creation, submission & approval |
| Q1 Check-in | July | Progress update — Planned vs. Actual |
| Q2 Check-in | October | Progress update — Planned vs. Actual |
| Q3 Check-in | January | Progress update — Planned vs. Actual |
| Q4 / Annual | March / April | Final achievement capture |

### ✅ Reporting & Governance

- **Achievement Report** — exportable CSV/Excel showing planned target vs. actual achievement for all employees
- **Completion Dashboard** — real-time view of which employees and managers have completed quarterly check-ins
- **Audit Trail** — logs all changes made after goal lock date, capturing who changed what and when, with post-lock change highlighting

---

## Bonus Features Implemented

### 🌟 Microsoft Entra ID (Azure AD) Integration
SSO simulation via Microsoft Entra ID with role-based access mapped from user profiles.

### 🌟 Microsoft Teams Integration
Notification panel with Teams adaptive card format, automated reminders for key events (submission, approval, check-in), and deep-link support to navigate directly from a notification to the relevant goal sheet.

### 🌟 Escalation Module
Configurable rule-based escalation engine:
- Employee has not submitted goals within N days of cycle open
- Manager has not approved goals within N days of submission
- Quarterly check-in not completed within the active window
- Escalation chain: Employee → Manager → Skip-level / HR
- Escalation log visible to Admin/HR for tracking

### 🌟 Analytics Module
- Quarter-on-Quarter (QoQ) achievement trend indicators
- Heatmaps and progress bar charts for completion rates
- Goal distribution by Thrust Area, UoM type, and status
- Manager effectiveness view with check-in completion comparisons

---

## Role Access Matrix

| Feature | Employee | Manager | Admin |
|---|---|---|---|
| Dashboard | ✅ | ✅ | ✅ |
| My Goals | ✅ | — | — |
| Check-ins | ✅ | ✅ | — |
| Team Goals | — | ✅ | — |
| Reports & Export | — | ✅ | ✅ |
| Analytics | ✅ | ✅ | ✅ |
| Escalation Module | — | — | ✅ |
| Audit Trail | — | — | ✅ |
| Admin Configuration | — | — | ✅ |

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| Frontend | Vanilla HTML/CSS/JS | Zero dependencies, instant load, zero infra cost |
| Data persistence | `localStorage` | No backend required; state survives page refresh |
| Excel export | SheetJS (xlsx.js) | Client-side CSV/Excel generation |
| Fonts | Google Fonts (Bebas Neue, DM Sans, JetBrains Mono) | Professional typography |
| Hosting | Vercel (static) | Free tier, instant global CDN |

---

## Project Structure

```
atomquest-portal/
├── atomquest_portal_v2.html   # Entire application (HTML + CSS + JS)
└── vercel.json                # Vercel routing config
```

**vercel.json:**
```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/atomquest_portal_v2.html" }]
}
```

---

## Running Locally

No installation needed. Open directly in any modern browser:

```bash
# Option 1: Just double-click the HTML file

# Option 2: Serve with a local static server
npx serve .

# Option 3:
python -m http.server 8080
```

---

## Architecture

```
Browser (Single HTML File)
│
├── Auth Layer         — Role-based login (Employee / Manager / Admin)
├── State Management   — In-memory JS state + localStorage persistence
├── Navigation         — SPA-style page routing (no URL changes)
├── Feature Modules    — Goals, Check-ins, Team, Reports, Analytics,
│                        Escalation, Audit Trail, Admin Config
└── Export Engine      — Client-side CSV / Excel via SheetJS
```

All computation, validation, and rendering happens in the browser. There is no server, no API, and no database — making the solution effectively zero-cost to host and operate.

---

## Submission Checklist

- [x] Live hosted demo URL
- [x] All Phase 1 & Phase 2 requirements implemented
- [x] Three complete user journeys (Employee, Manager, Admin)
- [x] Validation rules enforced (100% weightage, max 8 goals, min 10% per goal)
- [x] Audit trail with post-lock change logging
- [x] Bonus: SSO (Entra ID simulation), Teams integration, Escalation module, Analytics
- [x] Demo credentials provided for all 3 roles

---

*AtomQuest v1.0 — Hackathon 1.0*
