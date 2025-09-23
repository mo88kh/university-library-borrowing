```mermaid
classDiagram
    %% ===================== Core Orders =====================
    class Order {
      +string orderId
      +datetime placedAt
      +OrderStatus status        %% placed/accepted/preparing/ready/handedOff/cancelled
      +decimal itemsSubtotal
      +decimal discounts
      +decimal fees
      +decimal taxes
      +decimal total
      +string cancelReason?
      +datetime promisedReadyAt?
      +string source  %% e.g., "student-app"
    }

    class OrderItem {
      +string orderItemId
      +string name
      +int quantity
      +decimal unitPrice
      +decimal lineTotal
      +string notes?
    }

    class Modifier {
      +string modifierId
      +string name
      +decimal extraPrice
    }

    class AllergenFlag {
      +string code   %% e.g., NUTS, GLUTEN
      +string label
    }

    Order "1" *-- "1..*" OrderItem : composition
    OrderItem "0..*" o-- "0..*" Modifier : has
    OrderItem "0..*" o-- "0..*" AllergenFlag : allergen

    %% ===================== Status & Timeline =====================
    class StatusUpdate {
      +string statusUpdateId
      +OrderStatus fromStatus
      +OrderStatus toStatus
      +datetime at
      +string actorType  %% manager/kitchen/system
      +string actorId
      +string note?
    }
    Order "1" --> "0..*" StatusUpdate : timeline

    %% ===================== Assignment & Handoff =====================
    class CourierAssignment {
      +string assignmentId
      +string courierId
      +datetime assignedAt
      +AssignmentStatus status   %% pending/assigned/failed
      +string failureReason?
    }

    class Handoff {
      +string handoffId
      +datetime readyAt
      +datetime pickedUpAt?
      +string pickedUpBy?  %% courierId
      +string signatureOrCode?
    }

    Order "0..1" --> "1" CourierAssignment : uses
    Order "0..1" --> "1" Handoff : handoff

    %% ===================== Menu & Availability =====================
    class MenuItem {
      +string menuItemId
      +string name
      +string category
      +decimal price
      +bool active
    }

    class Availability {
      +string availabilityId
      +bool inStock
      +datetime updatedAt
      +string reason?        %% e.g., "86" / "sold-out"
    }

    class SoldOutWindow {
      +string windowId
      +datetime start
      +datetime end
      +string reason
    }

    MenuItem "1" --> "0..*" Availability : state
    MenuItem "1" --> "0..*" SoldOutWindow : blackout

    %% ===================== Printing & Reporting =====================
    class KitchenTicket {
      +string ticketId
      +datetime generatedAt
      +string format  %% PDF/print
    }
    Order "1" --> "0..1" KitchenTicket : prints

    class DailyReport {
      +string reportId
      +date forDate
      +int ordersCount
      +decimal revenue
      +decimal avgPrepTimeMinutes
      +int cancelCount
      +string csvPath
    }

    %% ===================== Security & Audit =====================
    class User {
      +string userId
      +string name
      +Role role   %% MANAGER / KITCHEN / COURIER / SUPPORT
    }
    class AuditLog {
      +string auditId
      +string entityType  %% Order, MenuItem, etc.
      +string entityId
      +string action      %% CREATE/UPDATE/CANCEL/ASSIGN
      +datetime at
      +string actorType   %% user/system
      +string actorId
      +string details
    }

    User "1" --> "0..*" AuditLog : performs
    Order "1" --> "0..*" AuditLog : changes

    %% ===================== Notifications & Services =====================
    class INotification {
      <<interface>>
      +send(to, message)
    }
    class Notification {
      +string notificationId
      +string type   %% accepted/ready/cancelled
      +datetime sentAt
      +string channel  %% email/push/SMS
      +string to
      +string payload
    }
    class NotificationService {
      +send(to, message)
    }

    Order "1" --> "0..*" Notification : emits
    NotificationService ..|> INotification : realizes
    Order ..> INotification : uses

    %% ===================== Enumerations (notes) =====================
    class OrderStatus {
      <<enumeration>>
      placed
      accepted
      preparing
      ready
      handedOff
      cancelled
    }

    class AssignmentStatus {
      <<enumeration>>
      pending
      assigned
      failed
    }
