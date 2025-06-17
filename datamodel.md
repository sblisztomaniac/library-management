# 📊 Data Model – LibraMVP

This document defines the database schema for the Library Management MVP. The model is normalized, simple, and Supabase/PostgreSQL-compatible.

---

## 📄 Table: `users`

| Column Name   | Data Type     | Constraints                  | Description                         |
|---------------|---------------|------------------------------|-------------------------------------|
| id            | UUID          | Primary Key, auto-generated  | Unique identifier for each user     |
| name          | TEXT          | NOT NULL                     | Full name of the user               |
| email         | TEXT          | UNIQUE, NOT NULL             | User email (used for login)         |
| role          | TEXT          | CHECK (`admin` or `user`)    | Role of user                        |
| status        | TEXT          | DEFAULT 'active'             | 'active' or 'inactive'              |
| created_at    | TIMESTAMP     | DEFAULT now()                | Time of registration                |

---

## 📄 Table: `books`

| Column Name       | Data Type     | Constraints                  | Description                          |
|-------------------|---------------|------------------------------|--------------------------------------|
| id                | UUID          | Primary Key, auto-generated  | Unique book ID                       |
| title             | TEXT          | NOT NULL                     | Title of the book                    |
| author            | TEXT          | NOT NULL                     | Author of the book                   |
| isbn              | TEXT          | UNIQUE (optional)            | ISBN number                          |
| category          | TEXT          |                              | Genre or category                    |
| copies_total      | INTEGER       | DEFAULT 1, NOT NULL          | Total number of copies owned         |
| copies_available  | INTEGER       | DEFAULT 1, NOT NULL          | Copies currently available to borrow |
| created_at        | TIMESTAMP     | DEFAULT now()                | When book was added                  |

---

## 📄 Table: `loans`

| Column Name   | Data Type     | Constraints                            | Description                                |
|---------------|---------------|----------------------------------------|--------------------------------------------|
| id            | UUID          | Primary Key, auto-generated            | Unique loan record                         |
| user_id       | UUID          | Foreign Key → `users(id)`              | Borrowing member                           |
| book_id       | UUID          | Foreign Key → `books(id)`              | Borrowed book                              |
| borrow_date   | TIMESTAMP     | DEFAULT now(), NOT NULL                | When the book was borrowed                 |
| due_date      | TIMESTAMP     | NOT NULL                               | When the book is due (default: +14 days)   |
| return_date   | TIMESTAMP     | NULLABLE                               | When the book was returned (if returned)   |

---

## 🔁 Relationships

- A `user` can borrow many `books` → 1:N (`users` → `loans`)
- A `book` can be borrowed many times → 1:N (`books` → `loans`)
- Only users with role = `'user'` can create loans (enforced at app level)

---

## 🔐 Notes on Authentication

- Use Supabase Auth (email/password) to manage `users`.
- Extend metadata from Auth into `users` table if needed (e.g., `role` sync).

---

## 🧠 Example Queries

**1. Get all books currently borrowed:**
```sql
SELECT * FROM loans
WHERE return_date IS NULL;
