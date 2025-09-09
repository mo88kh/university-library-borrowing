```mermaid
classDiagram
    %% ===== Core people =====
    class User {
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

    Book *-- BookCopy : composition

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
      +string status
      +int queuePosition
    }

    User --> BorrowingTransaction : makes
    BookCopy --> BorrowingTransaction : for
    User --> Reservation : places
    Book --> Reservation : for title

    %% ===== Fines & notifications =====
    class Fine {
      +int fineId
      +decimal amount
      +date assessedAt
      +date paidAt
      +string status
    }
    class Notification {
      +int notificationId
      +string type
      +string channel
      +date sentAt
      +string message
    }

    BorrowingTransaction --> Fine : may incur
    User --> Notification : receives
    BorrowingTransaction --> Notification : triggers
    Reservation --> Notification : triggers
