# Requirements – University Library System (Book Borrowing Process)

## Stakeholder Matrix

| Stakeholder         | Role / Responsibility        | Influence on System |
|---------------------|------------------------------|---------------------|
| Student             | Borrows books, requests renewals | High |
| Faculty             | Borrows books, extended privileges | High |
| Librarian           | Manages borrowing, fines, and renewals | High |
| IT Administrator    | Maintains system, ensures uptime | Medium |
| University Admin    | Sets policies, monitors system use | Medium |

## User Stories

1. As a student, I want to search for books by title so that I can quickly find what I need.
2. As a faculty member, I want to borrow books for a longer duration so that I can use them in research.
3. As a student, I want to reserve a book that is currently checked out so that I can borrow it when it becomes available.
4. As a librarian, I want to calculate fines automatically so that I don’t need to track them manually.
5. As a librarian, I want to send email confirmations so that borrowers have a record of their transactions.
6. As a student, I want to renew my borrowed books online so that I don’t have to visit the library.
7. As an IT admin, I want the system to integrate with the university login system so that authentication is secure.
8. As a librarian, I want to see overdue books so that I can follow up with students.
9. As a faculty member, I want email reminders before the due date so that I don’t miss deadlines.
10. As a student, I want to view my borrowing history so that I can keep track of my usage.

## Functional Requirements

1. The system shall allow search by title, author, or ISBN.
2. The system shall display real-time book availability.
3. The system shall allow reservation of checked-out books.
4. The system shall allow checkout with student/faculty ID.
5. The system shall set due dates based on user type.
6. The system shall handle renewal requests.
7. The system shall calculate fines for late returns.
8. The system shall send email confirmation after borrowing.
9. The system shall support viewing borrowing history.
10. The system shall allow librarians to override due dates.
11. The system shall block new borrowing if fines are unpaid.
12. The system shall allow multiple books in one transaction.
13. The system shall notify users before due dates.
14. The system shall log all borrowing and returning events.
15. The system shall allow administrators to configure fine rates.

## Non-Functional Requirements

1. The system shall support 200+ concurrent users.
2. The system shall respond to search queries within 2 seconds.
3. The system shall be available 99.5% of the time.
4. The system shall ensure data security with university login.
5. The system shall support mobile and desktop browsers.
6. The system shall have a user-friendly interface.
7. The system shall store transaction data for at least 5 years.

## MoSCoW Prioritization

| Requirement                                | Priority |
|--------------------------------------------|----------|
| Search for books by title/author/ISBN      | Must     |
| Real-time availability check               | Must     |
| Reserve checked-out books                  | Must     |
| Borrow using student/faculty ID            | Must     |
| Set due dates by user category             | Must     |
| Renewal requests                           | Should   |
| Fine calculation for late returns          | Must     |
| Email confirmations                        | Should   |
| Borrowing history                          | Could    |
| Librarian override for due dates           | Could    |
| Notification before due dates              | Should   |
| Mobile browser support                     | Should   |
| 99.5% system uptime                        | Must     |
| Store transaction data 5 years             | Won’t (for now) |

