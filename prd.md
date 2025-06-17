# 📘 Product Requirements Document (PRD)

## Project Title  
**LibraMVP – Minimal Library Management System**

---

## Objective

Build a simple, functional Library Management MVP for:
- Admins (librarians) to manage books and users.
- Members (students) to borrow and return books.
- Real-time tracking of book availability and due dates.

---

## Target Users

- **Librarian (Admin):** Manage inventory and users.
- **Library Member (User):** Browse, borrow, and return books.

---

## Core Features – MVP Scope

### 🛠️ Admin Features
- Add/Edit/Delete Books
- View current and historical book loans
- Register, edit, or deactivate member accounts

### 📚 Member Features
- Search books by title, author, or category
- Borrow available books (if in stock)
- Return borrowed books
- View borrowing history and current loans

### 🔄 System Features
- Real-time book availability updates
- Due date assignment (default: 14 days)
- Simple login for both user types

---

## Out of Scope (MVP)
- Online book reservation queue
- Late return fines or reminders
- Multi-branch library support
- Barcode/RFID integration

---

## Success Criteria
- Admin can manage books and members via dashboard
- Members can borrow/return books with accurate state tracking
- System reflects current availability and due dates correctly

---

## Suggested Tech Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Frontend  | React or Streamlit                  |
| Backend   | Node.js / FastAPI / Flask           |
| Database  | Supabase (PostgreSQL)               |
| Auth      | Supabase Auth (email + password)    |
| Hosting   | Supabase / Vercel / Netlify         |

---

## Data Model (MVP)

### 📄 Users
- `id`: UUID
- `name`: Text
- `email`: Text (unique)
- `role`: Enum (`admin` or `user`)
- `status`: Active / Inactive

### 📄 Books
- `id`: UUID
- `title`: Text
- `author`: Text
- `isbn`: Text (optional)
- `category`: Text
- `copies_total`: Integer
- `copies_available`: Integer

### 📄 Loans
- `id`: UUID
- `user_id`: FK → Users
- `book_id`: FK → Books
- `borrow_date`: Timestamp
- `due_date`: Timestamp
- `return_date`: Timestamp (nullable)

---

## User Flow


