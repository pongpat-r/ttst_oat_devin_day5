# Q&A Issue Tracker Web Application

---

## 1. Background

Create a web application for tracking and managing Q&A issues in a structured forum-style system.

The application should provide clear visibility of issues, ownership, status, and resolution progress.

---

## 2. Objective

Build a clean and modern Q&A forum tracker similar in concept to Stack Overflow, focused on structured issue management and project tracking.

---

## 3. Core Features

---

## 3.1 Home Screen – Q&A List

Display a paginated list of Q&A records:

- Maximum **15 items per page**
- Card-style layout
- Each item is clickable and opens a detail page

Each card must display:

- Title of question
- Content preview  
  - If content exceeds character limit, truncate and append `...`
- Category tag
- Severity tag
- Asked by (name)
- Issue date
- Status (Closed or Ongoing)

Pagination:

- Use query parameter format: `?page=1`
- Backend must return total count for pagination control

---

## 3.2 Q&A Detail Page

Display complete information for a selected Q&A record.

Fields:

- Question No
- Issue Date
- Issue By Name
- Issue By Company
- Requestor Company
- Requestor Name
- Issue / TODO
- Severity
- Category
- Title
- Content
- Due Date (MM/DD/YYYY)
- PIC Company
- PIC Name
- Action & Result
- Status
- Completion Date (MM/DD/YY)

---

## 4. Field Rules & Behavior

### 4.1 Auto-Generated Fields

- **Question No**
  - Auto-increment starting from 1

- **Issue Date**
  - Automatically set when creating a new Q&A
  - Not editable

- **Completion Date**
  - Automatically set when status is changed to `Closed`

---

### 4.2 Time Handling

- All time-related data must be stored in **UTC**
- Display all timestamps in **user local time**

---

### 4.3 String Input Fields

The following fields are editable text (string) inputs:

- Issue By Name
- Issue By Company
- Requestor Company
- Requestor Name
- Title
- Content
- PIC Company
- PIC Name
- Action & Result

---

### 4.4 Dropdown Fields

**Issue / TODO**
- Issue
- TODO
- Confirm

**Severity**
- Low
- Medium
- High

**Category**
- Environment
- Documentation
- Function
- Proj Management

**Status**
- Open
- Waiting for close
- Closed

---

### 4.5 Date Fields

- Issue Date → Auto-set on creation (not editable)
- Due Date → DateTime picker
- Completion Date → Auto-set when marked as Closed

---

## 5. Dashboard

Create a dashboard screen to provide overview and monitoring.

Dashboard must include:

- Graph: Issues by Status
- Graph: Issues by Severity
- Graph: Issues by Category
- Summary metrics:
  - Total Issues
  - Open Issues
  - Closed Issues
  - Overdue Issues

Purpose:
Provide quick visual overview of project health and workload.

---

## 6. Technical Stack

### 6.1 Frontend

- Framework: Next.js
- Language: JavaScript
- Styling: CSS

---

### 6.2 Backend

- Runtime: Next.js API Routes (Node.js)
- Database: PostgreSQL
- Authentication: NextAuth.js

---

## 7. Database Requirements

Table: `questions`

Suggested columns:

- id (SERIAL PRIMARY KEY)
- issue_date (TIMESTAMP UTC)
- issue_by_name (TEXT)
- issue_by_company (TEXT)
- requestor_company (TEXT)
- requestor_name (TEXT)
- issue_type (VARCHAR)
- severity (VARCHAR)
- category (VARCHAR)
- title (TEXT)
- content (TEXT)
- due_date (TIMESTAMP UTC)
- pic_company (TEXT)
- pic_name (TEXT)
- action_result (TEXT)
- status (VARCHAR)
- completion_date (TIMESTAMP UTC)
- created_at (TIMESTAMP UTC)
- updated_at (TIMESTAMP UTC)

Index recommended on:
- status
- severity
- category
- issue_date

---

## 8. Security Requirements

### 8.1 Prevent SQL Injection

- Use parameterized queries or ORM
- Never concatenate raw user input into SQL statements

### 8.2 Input Validation

- Validate all inputs server-side
- Enforce dropdown enum values
- Apply length limits to string inputs

### 8.3 Authentication & Authorization

- Protect API routes using NextAuth.js
- Restrict access to authenticated users
- Optional: role-based access control

### 8.4 XSS Protection

- Escape user-generated content
- Avoid unsafe HTML rendering
- Sanitize inputs when necessary

### 8.5 CSRF Protection

- Use built-in protections from Next.js and NextAuth.js
- Validate origin for sensitive requests

---

## 9. Deployment

### 9.1 Docker Support

Application must be deployable using Docker.

Include:

- Dockerfile
- docker-compose.yml
- PostgreSQL container
- App container
- Environment variables configuration

---

### 9.2 Container Structure

- Next.js application container
- PostgreSQL database container
- Production build enabled

---

## 10. Testing Requirements

### 10.1 Unit Testing

- API route validation
- Field validation logic
- Authentication checks

### 10.2 Integration Testing

- CRUD operations
- Pagination behavior
- Status update behavior
- Completion date auto-update logic

### 10.3 Security Testing

- Injection attempts
- Unauthorized API access
- XSS payload testing

---

## 11. Non-Functional Requirements

- Clean and modern UI
- Responsive layout
- Server-side pagination
- Optimized database indexing
- Production-ready configuration
- Secure by design
- Clear separation of frontend and backend responsibilities

---

## 12. Future Improvements (Optional)

- Full-text search
- Filtering and sorting
- Export to CSV
- Email notifications
- Audit log tracking
