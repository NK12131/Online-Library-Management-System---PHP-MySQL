# 📚 Online Library Management System

> A PHP & MySQL web app for running a college library — students browse and track their borrowed books, while admins manage the catalogue, issue and return books, and record fines.

Built as a college project for the **Web Services & Applications** course.

---

## ✨ Features

### 👩‍🎓 Student portal
- **Sign up** with name, email, mobile number and password — a unique Student ID is generated automatically
- **Live email check** (AJAX) during sign-up to prevent duplicate accounts
- **Login** with email and password; blocked accounts are refused
- **Dashboard** showing books currently issued and books not yet returned
- **Issued books history** with issue date, return date and any fine
- **My Profile** — view and update personal details
- **Change password** and **forgot password** (verified by registered email + mobile number)

### 🛠️ Admin panel
- **Dashboard** with live counts: books listed, books issued, books not returned, registered students, authors and categories
- **Categories** — add, edit, delete, mark active/inactive
- **Authors** — add, edit, delete
- **Books** — add, edit, delete (title, category, author, ISBN, price)
- **Issue books** — look up a student and a book by ID/ISBN (AJAX) and issue it
- **Returns & fines** — mark a book as returned and record the fine
- **Registered students** — view all students and block/unblock accounts
- **Change admin password**

---

## 🧰 Tech Stack

| Layer     | Technology                                  |
|-----------|---------------------------------------------|
| Backend   | PHP (PDO with prepared statements)          |
| Database  | MySQL / MariaDB                             |
| Frontend  | HTML, Bootstrap 3, jQuery, DataTables       |
| Icons     | Font Awesome, Glyphicons                    |
| Hosting   | XAMPP (local) · Heroku + ClearDB (original deployment) |

---

## 📁 Project Structure

```
Library-Management-System/
├── index.php                 # Student login
├── signup.php                # Student registration
├── dashboard.php             # Student dashboard
├── issued-books.php          # Student's issued books
├── my-profile.php            # Profile management
├── change-password.php
├── user-forgot-password.php
├── adminlogin.php            # Admin login
├── check_availability.php    # AJAX email check
├── captcha.php               # Captcha image generator
├── studentid.txt             # Counter used to generate Student IDs
├── includes/                 # Header, footer, DB config (student side)
├── admin/                    # Admin panel
│   ├── dashboard.php
│   ├── add-/edit-/manage-books.php
│   ├── add-/edit-/manage-authors.php
│   ├── add-/edit-/manage-categories.php
│   ├── issue-book.php
│   ├── manage-issued-books.php
│   ├── update-issue-bookdeails.php
│   ├── reg-students.php
│   └── includes/             # Header, footer, DB config (admin side)
├── assets/                   # CSS, JS, fonts, images
└── SQL/
    └── library.sql           # Database schema + sample data
```

---

## 🗄️ Database Schema

The `library` database contains six tables:

| Table                   | Purpose                                           |
|-------------------------|---------------------------------------------------|
| `admin`                 | Admin accounts                                    |
| `tblstudents`           | Registered students (ID, name, email, mobile, status) |
| `tblcategory`           | Book categories (with active/inactive status)     |
| `tblauthors`            | Authors                                           |
| `tblbooks`              | Books (name, category, author, ISBN, price)       |
| `tblissuedbookdetails`  | Issue records (book, student, dates, return status, fine) |

---

## 🚀 Getting Started

### Prerequisites
- [XAMPP](https://www.apachefriends.org/) (Apache + MySQL + PHP), or any equivalent LAMP/WAMP/MAMP stack

### Installation

1. **Clone the repo** into your XAMPP `htdocs` folder:
   ```bash
   cd /path/to/xampp/htdocs
   git clone https://github.com/parthjain99/Library-Management-System.git library
   ```

2. **Start Apache and MySQL** from the XAMPP control panel.

3. **Create the database**
   - Open [http://localhost/phpmyadmin](http://localhost/phpmyadmin)
   - Create a database named `library`
   - Import `SQL/library.sql`

4. **Point the app at your local database.** Edit **both** `includes/config.php` and `admin/includes/config.php`:
   ```php
   define('DB_HOST','localhost');
   define('DB_USER','root');
   define('DB_PASS','');
   define('DB_NAME','library');
   ```
   *(The repo's root `config.php` already contains these local values for reference.)*

5. **Open the app**
   - Student portal: [http://localhost/library](http://localhost/library)
   - Admin panel: [http://localhost/library/admin](http://localhost/library/admin)

### Demo admin login

| Username | Password   |
|----------|------------|
| `admin`  | `Test@123` |

---

## 🌐 Live Demo

The project was originally deployed at **https://libraryzz.herokuapp.com**.
*Note: Heroku discontinued its free tier in November 2022, so this link may no longer be active.*

---

## 🔒 Security Notes

This is a learning project and isn't production-ready as-is. Before deploying it publicly, consider:

- **Removing hard-coded credentials** from `includes/config.php` and `admin/includes/config.php` — load them from environment variables instead, and rotate any credentials that have been committed.
- **Upgrading password hashing** from `md5()` to PHP's `password_hash()` / `password_verify()`.
- **Strengthening password recovery** — email + mobile number alone is weak verification.
- **Replacing the `studentid.txt` counter** with a database-generated ID to avoid race conditions.
- **Adding CSRF protection** to forms.

---

## 🤝 Contributing

Pull requests are welcome. For larger changes, please open an issue first to discuss what you'd like to change.

## 👤 Author

**Nithin Kumar**