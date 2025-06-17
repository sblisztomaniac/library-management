# ⚡ 15-Minute Sprint Plan – LibraMVP Backend

**Sprint Objective:**  
Bootstrap the core backend logic for book management using in-memory data and functions that can later be connected to the frontend Bolt prototype.

---

## 🕐 Timebox: 15 Minutes

### ⏱️ Minute 0–2: Project Setup
- [ ] Create `/backend` directory
- [ ] Create `/backend/data/books.js` and initialize mock book array
- [ ] Create `/backend/services/bookService.js` file

### ⏱️ Minute 2–8: Book Service Core Functions
- [ ] Implement `addBook(bookData)`  
  → Push to books array, auto-generate UUID
- [ ] Implement `editBook(bookId, updatedFields)`  
  → Find and update matching book
- [ ] Implement `deleteBook(bookId)`  
  → Remove book by ID
- [ ] Implement `getAllBooks()`  
  → Return book list

### ⏱️ Minute 8–12: Data Validation & Defaults
- [ ] Add simple validation inside `addBook` (title, author required, copies ≥ 1)
- [ ] Ensure `copies_available` = `copies_total` on creation
- [ ] Use `uuid` package or simple timestamp-based ID for mocking

### ⏱️ Minute 12–14: Testing the Functions
- [ ] Create a `/backend/testBookService.js` file
- [ ] Manually call `addBook`, `editBook`, `deleteBook`, and `getAllBooks` with sample data
- [ ] Log outputs to verify logic

### ⏱️ Minute 14–15: Commit & Plan Next Sprint
- [ ] Save all files and organize into folders
- [ ] Review `loanService.js` and `userService.js` as next targets
- [ ] Leave TODOs in code for frontend integration points (e.g., `// Hook with UI button in Admin Panel`)

---

## 📂 Folder Structure

