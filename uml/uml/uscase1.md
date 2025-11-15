flowchart LR
%% Use Case Diagram – Borrow Book

%% === Actors ===
Borrower(["Borrower: Student or Faculty"]):::actor
Librarian(["Librarian"]):::actor
SSO(["University SSO - Login"]):::actor
Email(["Email System"]):::actor

%% === Use Cases ===
UC1(("UC-1 Borrow Book")):::usecase
UC2(("UC-2 Search Book")):::usecase
UC3(("UC-3 Check Availability")):::usecase
UC4(("UC-4 Reserve Book")):::usecase
UC5(("UC-5 Renew Book")):::usecase
UC6(("UC-6 Return Book")):::usecase
UC7(("UC-7 Send Confirmation")):::usecase

%% === Associations ===
Borrower --> UC1
Borrower --> UC2
Borrower --> UC3
Borrower --> UC5
Borrower --> UC6
Librarian --> UC5
Librarian --> UC6
SSO --> UC1
Email --> UC7

%% === Include / Extend (note: label syntax is '-. label .->') ===
UC1 -. <<include>> .-> UC2
UC1 -. <<include>> .-> UC3
UC1 -. <<extend>> .-> UC4
UC1 -. <<include>> .-> UC7

%% === Styling ===
classDef actor fill:#fff,border:#333,stroke-width:1px;
classDef usecase fill:#e8f5ff,stroke:#2b6cb0,stroke-width:2px,rx:30,ry:30;
