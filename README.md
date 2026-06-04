# Library-Management-System
# 📚 Library Management System

A complete, menu-driven **Library Management System** built in Java demonstrating Object-Oriented Programming principles — encapsulation, abstraction, and clean class design.

---

## 🗂️ Project Structure

```
LibrarySystem/
├── src/
│   └── library/
│       ├── Book.java           # Book entity with full encapsulation
│       ├── Member.java         # Member entity with borrow/return logic
│       ├── Library.java        # Core library management class
│       └── LibrarySystem.java  # Main program — menu-driven UI
├── docs/
│   └── class-diagram.md        # UML class diagram (text format)
├── sample_data/
│   └── sample_data.txt         # Pre-loaded books and members
└── README.md
```

---

## ⚙️ Setup & Run

### Prerequisites
- Java JDK 17 or higher  (`java -version` to check)

### Compile
```bash
mkdir -p out
javac -d out src/library/*.java
```

### Run
```bash
java -cp out library.LibrarySystem
```

---

## 🛠️ Features

### Book Management
| Feature | Description |
|---|---|
| Add Book | Add with ISBN, title, author, genre |
| Remove Book | Remove only if not currently borrowed |
| Display All | Show all books with status |
| Display Available | Show only available books |
| Search | Case-insensitive search by title, author, or genre |

### Member Management
| Feature | Description |
|---|---|
| Register Member | Register with ID, name, and contact |
| View Member | See details + borrowed books + outstanding fines |
| Display All | List all registered members |

### Transactions
| Feature | Description |
|---|---|
| Borrow Book | Borrow with 14-day loan period; blocks if fine is unpaid |
| Return Book | Return and auto-calculate overdue fine (₹5/day) |
| Pay Fine | Pay all or partial outstanding fines |

### Reports
| Feature | Description |
|---|---|
| Library Report | Summary of books, members, fines, and overdue list |

---

## 🧱 OOP Design

### Encapsulation
- All class fields are `private`
- Every field has a public getter; mutable fields have validated setters
- `Member.getBorrowedBooks()` returns an **unmodifiable view** to prevent external mutation

### Abstraction
- `Library` hides the underlying `ArrayList` storage; callers use high-level methods like `borrowBook(memberId, isbn)`
- Validation logic is centralised inside constructors and setters

### Key Design Decisions
- **Borrow limit**: Members can hold at most **5 books** simultaneously
- **Fine system**: ₹5 per overdue day, calculated automatically on return
- **Fine gate**: Members with unpaid fines cannot borrow more books
- **Duplicate guard**: Library rejects duplicate ISBNs and duplicate member IDs
- **Immutable list**: `getBorrowedBooks()` returns `Collections.unmodifiableList`

---

## 📋 Sample Data (pre-loaded on startup)

### Books
| ISBN | Title | Author | Genre |
|---|---|---|---|
| 978-3-16-148410-0 | Java Programming Guide | John Smith | Programming |
| 978-0-262-03384-8 | Introduction to Algorithms | Thomas Cormen | Computer Science |
| 978-0-13-468599-1 | Effective Java | Joshua Bloch | Programming |
| 978-0-13-235088-4 | Clean Code | Robert Martin | Programming |
| 978-0-20-161622-4 | The Pragmatic Programmer | David Thomas | Software Engineering |
| 978-0-59-651798-1 | Learning Python | Mark Lutz | Programming |
| 978-0-06-112008-4 | To Kill a Mockingbird | Harper Lee | Fiction |
| 978-0-74-320348-1 | The Hitchhiker's Guide | Douglas Adams | Science Fiction |

### Members
| ID | Name | Contact |
|---|---|---|
| M001 | Alice Johnson | alice@email.com |
| M002 | Bob Williams | bob@email.com |
| M003 | Carol Martinez | carol@email.com |

> Alice (M001) has **Effective Java** pre-borrowed at startup to demonstrate the system.

---

## 🖥️ Sample Session

```
  ╔══════════════════════════════════════════╗
  ║     LIBRARY MANAGEMENT SYSTEM  v1.0      ║
  ║           City Central Library           ║
  ╚══════════════════════════════════════════╝
  8 books  |  3 members loaded.

  Enter your choice: 6

  ┌── BORROW BOOK ──────────────────────────┐

  Enter Member ID  : M002
  Enter Book ISBN  : 978-3-16-148410-0
  ✅ Book borrowed successfully!
     Member  : Bob Williams
     Book    : Java Programming Guide
     Due Date: 2026-06-09
```

---

## 📊 Class Diagram (simplified)

```
┌─────────────┐         ┌──────────────┐
│    Book     │         │    Member    │
├─────────────┤    0..* ├──────────────┤
│ -isbn       │◄────────│ -borrowedBooks│
│ -title      │         │ -memberId    │
│ -author     │         │ -name        │
│ -genre      │         │ -contact     │
│ -isAvailable│         │ -fineAmount  │
│ -dueDate    │         ├──────────────┤
├─────────────┤         │ +borrowBook()│
│ +getters    │         │ +returnBook()│
│ +setters    │         │ +payFine()   │
│+displayInfo()│        └──────┬───────┘
└─────────────┘                │ manages
                               │
                    ┌──────────▼───────┐
                    │    Library       │
                    ├──────────────────┤
                    │ -books: List     │
                    │ -members: List   │
                    ├──────────────────┤
                    │ +addBook()       │
                    │ +borrowBook()    │
                    │ +returnBook()    │
                    │ +searchBooks()   │
                    │ +displayReport() │
                    └──────────────────┘
```

---

## ✅ Quality Checklist

- [x] All fields private with validated getters/setters
- [x] Constructor validation with `IllegalArgumentException`
- [x] Borrow limit enforcement (max 5 books)
- [x] Due date tracking (14-day loan period)
- [x] Automatic fine calculation on return (₹5/day overdue)
- [x] Fine gate — blocks borrowing when fine unpaid
- [x] Duplicate ISBN / member ID detection
- [x] Safe removal guards (can't remove borrowed book or member with active loans)
- [x] Immutable list returned from `getBorrowedBooks()`
- [x] Input validation in menu (non-empty strings, integer parsing)
- [x] Overdue report in Library Report
