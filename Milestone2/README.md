1. Project Overview
   
System Purpose: FranchiseOps AI Copilot is an AI-powered Franchise Management System designed to help franchise businesses monitor daily operations, analyze store performance, and make data-driven decisions.

Core Functionality: Features an interactive management dashboard alongside an AI-powered SQL Copilot that retrieves real-time answers directly from the franchise database.

Milestone 2 Focus: Extends the Milestone 1 application by integrating complete authentication, role-based security, modular page navigation, and administrative user controls.

2. Objectives

Authentication Integration: Seamlessly connect signup, login, and password recovery workflows from Milestone 1 into FastAPI endpoints.

Role-Based Access Control: Implement strict server-side authorization (RBAC) across 5 distinct user roles.

Administrative Control Hub: Build a dedicated Admin Dashboard to manage user accounts, change roles, lock accounts, and view activity audit logs.

Interactive Dashboard: Provide responsive navigation across all six operational agent modules.

AI Copilot Enhancement: Expand natural language understanding to support 15+ business query intents using whitelisted SQL commands.

Profile Management: Allow users to view account details and update credentials securely.

3. Technology Stack

Backend Framework: FastAPI (Python)

Database: SQLite3

Security & Auth: JWT (PyJWT), Password Hashing (bcrypt / PBKDF2)

Frontend: HTML5, CSS3 (Custom Responsive Layout with Dark Mode), JavaScript

Deployment & Tunneling: Google Colab, ngrok

4. Features and Modules

Authentication & Profile

API Endpoints: /api/auth/signup, /api/auth/login, and /api/auth/forgot.

Security Rules: Account locks automatically after 5 consecutive failed login attempts.

User Profile Page: Displays username, email, assigned role, joined date, and enables secure password updates.

Role-Based Access Control (RBAC)

Server-Side Enforcement: Calls need(ctx, capability) on every route to return HTTP 403 Forbidden for unauthorized requests.

Privilege Matrix:

Admin: Full system access (all pages, agent runs, user management, and audit logs).

Franchise Owner: Access to all agent pages, Copilot, and agent execution; no user management.

Store Manager: Access to Copilot, Workforce, Outlets, Inventory, Sentiment, and Audit (scoped to their specific outlet ID).

Staff: Access strictly limited to Copilot (outlet-scoped) and Profile page.

Auditor: Read-only access to all operational pages and compliance audit records.

Admin Dashboard

User Management: Overview table displaying email, username, role, status (Active/Locked), and creation date.

Account Actions: Capabilities to add users, delete users (with confirmation), promote/demote roles, and lock/unlock accounts.

System Safeguards: Prevents self-deletion, self-locking, and removal of the last remaining Admin.

Audit Trail: Displays a real-time log of the latest 50 administrative actions.

Operational Agents

Workforce Agent: Monitors staffing levels, shift cover, and employee attrition trends.

Outlets Agent: Evaluates outlet health scores and ranks store performance.

Inventory Agent: Tracks stock cover metrics and generates reorder tickets.

Marketing Agent: Measures campaign performance metrics and marketing ROI.

Sentiment Agent: Analyzes customer feedback ratings and sentiment trends.

Audit Agent: Conducts automated compliance checks and logs operational findings.

5. Copilot

Execution Engine: Translates user questions directly into whitelisted SQL database queries.

No.	Sample Question	Expected Answer
1	Which is the healthiest outlet?
Displays the outlet with the highest health score, along with its location and score.
2	Which outlet has the highest risk?	
Displays the outlet with the lowest health score and its weakest performance area.
3	Why is OUT-010 flagged?
Explains the outlet's health status, weakest agent scores, and open action tickets, if available.
4	What is the current inventory status?	
Displays the number of SKU records, items at or below reorder level, items with less than seven days of stock cover, and stock-out risk.
5	Which items need urgent restocking?	
Displays the most urgent SKUs, quantities to order, and outlets requiring stock replenishment.
6	Show the sales trend for the last seven days.
Displays recorded sales for the last seven days, including the best and weakest sales days.
7	How many employees work in Bengaluru?
Displays the employee count for Bengaluru and the location with the highest employee count, where available.
8	Which city has the most employees?
Displays the city with the highest employee count and the employee count for each listed city.
9	Which state has the most outlets?	
Displays the state with the highest number of outlets.
10	Show all outlets in Karnataka.
Displays the outlets matching the selected state, where supported by the city-to-state mapping.
11	What is the workforce status?	
Displays total staff, employees with high attrition risk, and average overtime hours.
12	Show details of OUT-010.	
Retrieves matching outlet records and related available action-ticket information.

Additional Example Business Questions
Other examples of natural-language questions include:

Show me the overall franchise performance.
What is the current workforce status?
Show the available franchise information.
Give me the relevant business performance details.
Retrieve the records matching my question.
Show the database results for this query.

Copilot Response Details
When a supported question is submitted:

The Copilot identifies the question pattern.
It retrieves the relevant information from the database.
It executes the corresponding SQL query.
It displays the generated SQL query.
It presents the query results and row count, where applicable.

Unsupported questions receive a helpful response with suggestions for supported queries.

Note: Answers are generated dynamically from the database. The examples above describe expected response content, not fixed database values. Actual results depend on the available records, implemented SQL patterns, and user permissions. The exact questions supported depend on the implementation in analyst.py and qa.py.

6. Application Screenshots
Login Page
<img width="1440" height="810" alt="Login" src="https://github.com/user-attachments/assets/a94c0e63-1310-4e1e-a8a4-6b37f7966b06" />
 Main Dashboard
<img width="1440" height="815" alt="Dashboard" src="https://github.com/user-attachments/assets/b79672d9-2e74-46ad-83fc-9e7ae3610d62" />

 AI Copilot Interface
<img width="1438" height="809" alt="Copilot" src="https://github.com/user-attachments/assets/4f0f0864-05ce-4206-8cc3-be580a9b6b08" />

 Copilot SQL Query and Results
<img width="1438" height="815" alt="Copilot_query" src="https://github.com/user-attachments/assets/1a7e84d1-037a-41ff-bfc4-56c66481e32a" />

 Navigation and Application Modules
 <img width="1440" height="811" alt="Navigation" src="https://github.com/user-attachments/assets/7cf93c76-0f22-4784-8131-a020e7f3eed0" />

8. Testing

Access Control Verification: Tested each role to confirm authorized navigation and verify that direct API calls to unauthorized routes return an HTTP 403 Forbidden error.

Security & Auth Testing: Verified input validation, password hashing, JWT bearer token checks, and lockout after 5 invalid attempts.

Administrative Operations: Tested adding, locking, unlocking, and changing roles for users, ensuring safeguard rules for Admin accounts work as intended.

Copilot Accuracy: Validated all 15+ natural language intents against the underlying SQLite database outputs.

8. Conclusion

Milestone Completion: Successfully transforms FranchiseOps AI into a secure, multi-role enterprise application.

Key Achievements: Delivered FastAPI authentication integration, server-enforced RBAC, automated operational background agents, real-time SQL execution via AI Copilot, and an administrative control panel.

Project Status: Meets all functional and technical criteria required for Infosys Springboard Internship 7.0 Batch 4.0.
