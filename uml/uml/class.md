```mermaid
classDiagram
    %% ===== Core people =====
    class User {
      <<abstract>>
      +int userId
      +string name
      +string email
    }
    class Student {
      +string studentId
    }
    class Faculty {
      +string facultyId
    }
    class Librarian {
      +string employeeId
    }

    User <|-- Student
    User <|-- Faculty
    User <|-- Librarian
    ...

    %% ===== Books & copies =====
    class Book {
      +string isbn
      +string title
      +string author
      +string subject
    }
    class BookCopy {
      +string copyId
      +string barcode
      +string status  %% Available/CheckedOut/Reserved
      +string location
    }

    Book "1" *-- "1..*" BookCopy : composition

    %% ===== Transactions & reservations =====
    class BorrowingTransaction {
      +int loanId
      +date checkoutDate
      +date dueDate
      +date returnDate
      +int renewalsCount
    }
    class Reservation {
      +int reservationId
      +date requestDate
      +string status  %% Active/Cancelled/Fulfilled
      +int queuePosition
    }

    User "1" --> "0..*" BorrowingTransaction : makes
    BookCopy "1" --> "0..*" BorrowingTransaction : for
    User "1" --> "0..*" Reservation : places
    Book "1" --> "0..*" Reservation : for title

    %% ===== Fines & notifications =====
    class Fine {
      +int fineId
      +decimal amount
      +date assessedAt
      +date paidAt
      +string status  %% Unpaid/Paid
    }
    class Notification {
      +int notificationId
      +string type   %% Checkout/Reminder/Overdue
      +string channel  %% Email
      +date sentAt
      +string message
    }

    BorrowingTransaction "1" --> "0..1" Fine : may incur
    User "1" --> "0..*" Notification : receives
    BorrowingTransaction "1" --> "0..*" Notification : triggers
    Reservation "1" --> "0..*" Notification : triggers

    %% ===== Policies & services =====
    class LoanPolicy {
      +int policyId
      +string userType  %% Student/Faculty
      +int maxDays
      +int maxRenewals
      +decimal finePerDay
    }
    LoanPolicy "1" --> "0..*" BorrowingTransaction : governs

    class INotification {
      <<interface>>
      +send(user, message)
    }
    class EmailNotificationService {
      +send(user, message)
    }

    EmailNotificationService ..|> INotification : realization
    BorrowingTransaction ..> INotification : uses
