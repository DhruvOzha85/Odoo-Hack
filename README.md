# 💼 Expense Approval System — CE Hackathon

> A **role-based corporate expense management system** with smart approval workflows, sequential & parallel routing, and multi-tier access control — built entirely in pure **HTML · CSS · Vanilla JS**.

[![Live Demo](https://img.shields.io/badge/🚀_Live_Demo-ce--hackathon.netlify.app-00ffe7?style=for-the-badge)](https://ce-hackathon.netlify.app/)
[![GitHub](https://img.shields.io/badge/GitHub-DhruvOzha85%2FOdoo--Hack-181717?style=for-the-badge&logo=github)](https://github.com/DhruvOzha85/Odoo-Hack)
[![Netlify](https://img.shields.io/badge/Deployed_on-Netlify-00C7B7?style=for-the-badge&logo=netlify)](https://netlify.com)
![HTML](https://img.shields.io/badge/HTML5-100%25-E34F26?style=for-the-badge&logo=html5&logoColor=white)

---

## 📌 Overview

**CE Hackathon Expense Approval System** is a fully client-side web application that simulates a real-world corporate expense management workflow. It allows employees to submit expense claims, routes them through a configurable approval chain managed by an admin, and generates audit-ready receipts upon final approval.

No backend. No framework. No build step. Just open `index.html` and go.

---

## ✨ Key Features

- 🔐 **Role-Based Access** — Four distinct user roles with dedicated views
- 🔀 **Sequential & Parallel Routing** — Admin-configurable approval flow
- ✅ **Required Approver Enforcement** — Auto-reject if a required approver declines
- 📊 **Approval Threshold** — Configurable minimum approval percentage (e.g. 60%)
- 👔 **Manager-First Escalation** — Route to direct manager before other approvers
- 🧾 **Auto-Generated Receipts** — Full audit trail on final approval
- 📱 **Responsive UI** — Works across desktop and mobile

---

## 👥 User Roles

### 🛡️ Admin
Configures the entire approval framework for the organisation.
- Define approval rules per user
- Assign required approvers
- Toggle sequential vs. parallel flow
- Set manager-first escalation
- Configure minimum approval percentage

### 👔 Manager
Reviews and acts on pending expense requests from team members.
- View all pending requests
- Approve or reject expenses
- Add comments & remarks
- Track full approval history
- Receive first-pass escalations

### 👤 Employee
Submits expense claims and monitors their status in real time.
- Submit new expense requests
- Track request status live
- View approval chain progress
- Receive auto-rejection notifications
- Access history of past submissions

### 🧾 Receipt
Auto-generated upon final approval — a structured audit-ready record.
- Auto-generated on approval
- Full approval chain record
- Expense summary breakdown
- Ready for accounting & audit

---

## 🔄 Approval Workflow

```
Employee submits expense
        ↓
Manager review (if Manager-First is enabled)
        ↓
Sequential OR Parallel routing to assigned approvers
        ↓
Required approvers must sign off
  → If any required approver rejects → Auto-rejected ✗
        ↓
Minimum approval threshold check (e.g. 60%)
        ↓
Final Approval ✓ → Receipt Auto-Generated 🧾
```

---

## 📁 Project Structure

```
Odoo-Hack/
│
├── index.html              # Entry point / Login
├── AdminView.html          # Admin dashboard — configure rules & approvers
├── managerview.html        # Manager dashboard — review & act on requests
├── employeView.html        # Employee dashboard — submit & track expenses
├── UserRoleManager.html    # Role assignment & user management
├── receipt.html            # Auto-generated receipt view
└── README.md               # Project documentation
```

---

## 🛠️ Tech Stack

| Technology | Usage |
|---|---|
| HTML5 | Page structure & markup |
| CSS3 | Styling, animations, layout |
| Vanilla JavaScript | Logic, DOM manipulation, workflow |
| CSS Variables | Consistent theming across pages |
| Flexbox & Grid | Responsive layouts |
| Font Awesome | Icons |
| Netlify | Deployment & CDN hosting |

---

## 🚀 Getting Started

### Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/DhruvOzha85/Odoo-Hack.git

# 2. Navigate into the project
cd Odoo-Hack

# 3. Open in your browser
open index.html
# or just double-click index.html in your file explorer
```

> No dependencies. No `npm install`. No build step required.

### Live Demo

The project is deployed and publicly accessible at:

**🌐 [https://ce-hackathon.netlify.app/](https://ce-hackathon.netlify.app/)**

---

## 📸 Pages at a Glance

| Page | Role | Purpose |
|---|---|---|
| `index.html` | All | Login / entry point |
| `AdminView.html` | Admin | Configure approval rules |
| `managerview.html` | Manager | Review pending requests |
| `employeView.html` | Employee | Submit & track expenses |
| `UserRoleManager.html` | Admin | Manage user roles |
| `receipt.html` | All | View approved receipt |

---

## 🏆 Built For

This project was built as part of the **CE Hackathon** — a challenge to design and implement a functional corporate expense approval system with real-world workflow logic, entirely on the frontend.

---

## 👤 Author

**DhruvOzha85**
- GitHub: [@DhruvOzha85](https://github.com/DhruvOzha85)
- Project: [github.com/DhruvOzha85/Odoo-Hack](https://github.com/DhruvOzha85/Odoo-Hack)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">Built with ♥ for the CE Hackathon &nbsp;·&nbsp; Deployed on Netlify &nbsp;·&nbsp; 100% HTML · CSS · JS</p>
