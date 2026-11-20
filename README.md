# Smart-Student-Management-System
Payment management module for a School Management System: parents upload payment slips and track paid/pending status and due amounts, while administrators verify slips and update student payment records. Built with Java.
# School Management System: Payment Management Module

A Java-based web module that computerizes a school's manual fee payment process. Parents can submit payment slips online and track their child's payment status, while administrators verify the slips and record approved payments in the school database.

This repository contains **only the payment management component** of a 5-member group project (SE2012). It was designed and developed by me as part of the larger School Management System.

---

## Table of Contents

- [Features](#features)
- [User Roles](#user-roles)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Design](#database-design)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [UI Theme](#ui-theme)
- [Screenshots](#screenshots)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

## Features

### 1. Student Payment Status
- Shows whether a student's payment is **Paid** or **Pending**.
- For pending payments, displays the **amount already paid** and the **remaining due amount**.

### 2. Payment Slip Submission
- Parents can upload a payment slip (image or PDF) for a specific student and fee.
- Each submission is stored with a status of `PENDING`, `APPROVED`, or `REJECTED`.
- Parents can see the review result of each submitted slip.

### 3. Student Payment Record Viewing
- Parents can view the full payment history of their child.
- Administrators can view and search payment records for all students.
- Administrators review submitted slips, **approve or reject** them, and approved payments are saved to the school database and reflected in the student's payment status.

---

## User Roles

| Role | Capabilities |
|------|--------------|
| **Parent** | Upload payment slips, view payment status (paid / pending, amount paid, amount due), view payment history |
| **Administrator** | Review submitted slips, approve or reject them, add and manage student payment records, view all payment records |

---

## Tech Stack

> Update this section to match what you actually used.

| Layer | Technology |
|-------|------------|
| Backend | Java (e.g. Servlets / Spring Boot) |
| Frontend | HTML, CSS, JavaScript (e.g. JSP / Thymeleaf) |
| Database | MySQL |
| Build tool | Maven / Gradle |
| IDE | IntelliJ IDEA |
| Version control | Git & GitHub |

---

## Project Structure

> Replace with your real folder layout. Example:

```
payment-management/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/school/payment/
│   │   │       ├── controller/     # Request handling (parent & admin)
│   │   │       ├── service/        # Business logic (balance calculation, approval)
│   │   │       ├── dao/            # Database access
│   │   │       ├── model/          # Payment, PaymentSlip, Fee entities
│   │   │       └── util/           # DB connection, file upload helpers
│   │   ├── resources/
│   │   └── webapp/
│   │       ├── css/                # Red & white theme styles
│   │       ├── js/
│   │       └── pages/              # Parent and admin pages
├── database/
│   └── payment.sql                 # Schema script
├── uploads/                        # Stored payment slips (git-ignored)
└── README.md
```

---

## Database Design

The module uses the shared school MySQL database. Main tables (adjust to match your schema):

| Table | Purpose |
|-------|---------|
| `student_fee` | Total fee amount and due date per student |
| `payment_slip` | Uploaded slips: student, amount, file path, submitted date, status (`PENDING` / `APPROVED` / `REJECTED`), admin remarks |
| `payment_record` | Verified payments created when an admin approves a slip |

**Payment status logic**

```
amount_paid = SUM(approved payments for the student)
amount_due  = total_fee - amount_paid
status      = PAID if amount_due == 0, otherwise PENDING
```

---

## Getting Started

### Prerequisites

- Java JDK 17 or later (match your project's version)
- MySQL 8.x
- Maven or Gradle
- IntelliJ IDEA (recommended)
- A servlet container such as Apache Tomcat (if not using embedded Spring Boot)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/school-payment-management.git
   cd school-payment-management
   ```

2. **Create the database**
   ```bash
   mysql -u root -p < database/payment.sql
   ```

3. **Configure the database connection**

   Update the connection settings (e.g. in `application.properties` or your DB utility class):
   ```properties
   db.url=jdbc:mysql://localhost:3306/<database_name>
   db.username=<your_username>
   db.password=<your_password>
   ```

4. **Configure the upload directory**

   Set the folder where payment slips will be saved, and make sure it is writable.

5. **Build and run**
   ```bash
   mvn clean install
   mvn spring-boot:run     # or deploy the WAR to Tomcat
   ```

6. **Open the app**

   Visit `http://localhost:8080/` in your browser.

---

## Usage

**As a parent**
1. Log in and open the payments page for your child.
2. Check the payment status, amount paid, and amount due.
3. Click **Submit Payment Slip**, choose the file, enter the paid amount, and submit.
4. Wait for admin approval; the status updates once the slip is verified.

**As an administrator**
1. Log in and open **Pending Slips**.
2. Open a slip, compare it against the submitted details, then **Approve** or **Reject** (with remarks).
3. Approved payments are saved to the database and update the student's balance automatically.
4. Use **Payment Records** to search and view the history of any student.

---

## UI Theme

The interface uses a **red and white** theme to match the rest of the School Management System.

| Role | Color |
|------|-------|
| Primary | Red |
| Background | White |

---

## Screenshots

> Add screenshots here once the UI is ready.

| Parent: Payment Status | Parent: Slip Upload | Admin: Slip Review |
|---|---|---|
| ![Payment status](docs/screenshots/payment-status.png) | ![Slip upload](docs/screenshots/slip-upload.png) | ![Slip review](docs/screenshots/slip-review.png) |

---

## Future Improvements

- Email or SMS notifications when a slip is approved or rejected
- Downloadable payment receipts (PDF)
- Online payment gateway integration
- Payment reports and analytics for administrators
- Installment plans and late-fee handling

---

## Author

**<Your Name>**
Payment Management Module, School Management System (SE2012 Group Project)

GitHub: [@your-username](https://github.com/your-username)
