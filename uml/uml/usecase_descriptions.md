# Use Case Descriptions – Book Borrowing Process

## 1. Borrow Book
**Actors:** Student, Librarian  
**Precondition:** Student is logged in, book is available.  
**Main Flow:**
1. Student presents ID / logs into system.
2. System checks availability.
3. Librarian confirms checkout.
4. System sets due date.
5. System records transaction.
6. Email confirmation is sent.

**Alternative Flow:** If book is not available → show error, suggest reservation.

---

## 2. Renew Book
**Actors:** Student  
**Precondition:** Book is borrowed, not overdue.  
**Main Flow:**
1. Student requests renewal.
2. System checks if renewal is allowed.
3. System updates due date.
4. Confirmation sent by email.

**Alternative Flow:** Renewal blocked if another reservation exists.

---

## 3. Reserve Book
**Actors:** Student  
**Precondition:** Book is currently checked out.  
**Main Flow:**
1. Student searches for book.
2. System shows “Checked Out.”
3. Student clicks “Reserve.”
4. System records reservation.
5. Email confirmation is sent.

**Alternative Flow:** If too many reservations exist → system blocks new request.

