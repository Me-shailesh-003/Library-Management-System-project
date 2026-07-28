Automated Library Management System (LMS) – RDBMS Project

An enterprise-grade Relational Database Management System (RDBMS) designed and implemented in MySQL 8.0. This project transforms manual library bookkeeping into an automated system following Third Normal Form (3NF), with stored procedures, triggers, and referential integrity.

KEY TECHNICAL HIGHLIGHTS

- 100% Normalized Relational Schema (3NF)
- Automated transactional checkout using the BorrowBook stored procedure
- Event-driven fine calculation using the FineTrigger database trigger
- Primary Keys and Foreign Keys for referential integrity

DATABASE SCHEMA

Category
- CategoryID (Primary Key)
- CategoryName

Author
- AuthorID (Primary Key)
- AuthorName

Book
- BookID (Primary Key)
- Title
- AuthorID (Foreign Key)
- CategoryID (Foreign Key)
- Quantity

Member
- MemberID (Primary Key)
- MemberName
- Phone
- Email

Loan
- LoanID (Primary Key)
- BookID (Foreign Key)
- MemberID (Foreign Key)
- IssueDate
- DueDate
- ReturnDate

Fine
- FineID (Primary Key)
- LoanID (Foreign Key)
- FineAmount

AUTOMATED BUSINESS LOGIC

Member Registration:
CALL AddMember('Amit', '9876543222', 'amit@gmail.com');

Book Checkout:
CALL BorrowBook(2, 1, '2026-07-20', '2026-07-30');

Late Fee Trigger:
UPDATE Loan
SET ReturnDate = '2026-07-18'
WHERE LoanID = 2;

The trigger calculates overdue days and inserts the fine automatically.

REPOSITORY STRUCTURE

LibraryManagementSystem.sql
LMS_Project_Report.docx
README.md

HOW TO RUN

1. Clone the repository.
2. Open MySQL.
3. Run:
mysql -u root -p

Then execute:
source LibraryManagementSystem.sql;

Verification Queries:

SELECT LoanID, Title, MemberName, IssueDate, DueDate, ReturnDate
FROM Loan
JOIN Book ON Loan.BookID = Book.BookID
JOIN Member ON Loan.MemberID = Member.MemberID;

SELECT SUM(FineAmount) AS TotalRevenueINR FROM Fine;

SELECT Title, MemberName
FROM Loan
JOIN Book ON Loan.BookID = Book.BookID
JOIN Member ON Loan.MemberID = Member.MemberID
WHERE ReturnDate IS NULL;



