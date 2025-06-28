# Class Diagram - Augmented Reality Shopping App

```mermaid
classDiagram
    class User {
        -userId: String
        -username: String
        -email: String
        -password: String
        -phoneNumber: String
        -address: Address
        -userType: UserType
        +register()
        +login()
        +logout()
        +updateProfile()
    }

    class Admin {
        -adminId: String
        -permissions: List<Permission>
        +manageProducts()
        +viewOrders()
        +generateReports()
        +manageUsers()
    }

    class CustomerSupport {
        -supportId: String
        -specialization: String
        +handleChat()
        +resolveIssues()
        +escalateTicket()
    }

    class Product {
        -productId: String
        -name: String
        -description: String
        -price: Double
        -category: Category
        -brand: String
        -images: List<Image>
        -arModel: ARModel
        -stockQuantity: Integer
        +getDetails()
        +updateStock()
        +isAvailable()
    }

    class Category {
        -categoryId: String
        -name: String
        -description: String
        +getProducts()
    }

    class Cart {
        -cartId: String
        -userId: String
        -items: List<CartItem>
        -totalAmount: Double
        +addItem()
        +removeItem()
        +updateQuantity()
        +calculateTotal()
        +clear()
    }

    class CartItem {
        -itemId: String
        -productId: String
        -quantity: Integer
        -price: Double
        +updateQuantity()
        +calculateSubtotal()
    }

    class Order {
        -orderId: String
        -userId: String
        -orderDate: DateTime
        -status: OrderStatus
        -totalAmount: Double
        -shippingAddress: Address
        -items: List<OrderItem>
        +placeOrder()
        +cancelOrder()
        +trackOrder()
        +updateStatus()
    }

    class OrderItem {
        -itemId: String
        -productId: String
        -quantity: Integer
        -price: Double
        +calculateSubtotal()
    }

    class Payment {
        -paymentId: String
        -orderId: String
        -amount: Double
        -paymentMethod: PaymentMethod
        -status: PaymentStatus
        -transactionDate: DateTime
        +processPayment()
        +refund()
        +getStatus()
    }

    class Address {
        -addressId: String
        -street: String
        -city: String
        -state: String
        -zipCode: String
        -country: String
        +validate()
        +format()
    }

    class Feedback {
        -feedbackId: String
        -userId: String
        -productId: String
        -rating: Integer
        -comment: String
        -date: DateTime
        +submitFeedback()
        +updateFeedback()
    }

    class ARModel {
        -modelId: String
        -productId: String
        -modelUrl: String
        -modelType: String
        +loadModel()
        +renderModel()
    }

    class Chat {
        -chatId: String
        -userId: String
        -supportId: String
        -messages: List<Message>
        -status: ChatStatus
        +sendMessage()
        +endChat()
    }

    class Message {
        -messageId: String
        -senderId: String
        -content: String
        -timestamp: DateTime
        -type: MessageType
    }

    class Report {
        -reportId: String
        -type: ReportType
        -data: Object
        -generatedDate: DateTime
        +generateReport()
        +exportReport()
    }

    enum UserType {
        CUSTOMER
        ADMIN
        SUPPORT
    }

    enum OrderStatus {
        PENDING
        CONFIRMED
        SHIPPED
        DELIVERED
        CANCELLED
    }

    enum PaymentStatus {
        PENDING
        COMPLETED
        FAILED
        REFUNDED
    }

    enum PaymentMethod {
        CREDIT_CARD
        DEBIT_CARD
        PAYPAL
        BANK_TRANSFER
    }

    enum ChatStatus {
        ACTIVE
        CLOSED
        PENDING
    }

    enum MessageType {
        TEXT
        IMAGE
        FILE
    }

    enum ReportType {
        SALES
        INVENTORY
        USER_ACTIVITY
        REVENUE
    }

    %% Relationships
    User ||--o{ Order : places
    User ||--o{ Feedback : submits
    User ||--o{ Chat : participates
    User ||--|| Cart : has
    User ||--o{ Address : has

    Admin ||--o{ Report : generates
    Admin ||--o{ Product : manages
    Admin ||--o{ Order : views

    CustomerSupport ||--o{ Chat : handles

    Product ||--o{ CartItem : contained_in
    Product ||--o{ OrderItem : ordered_in
    Product ||--o{ Feedback : receives
    Product ||--|| ARModel : has
    Product ||--|| Category : belongs_to

    Cart ||--o{ CartItem : contains
    Order ||--o{ OrderItem : contains
    Order ||--|| Payment : has
    Order ||--|| Address : shipped_to

    Chat ||--o{ Message : contains

    Category ||--o{ Product : contains
```

## Class Diagram Description

This class diagram represents the core entities and their relationships in the Augmented Reality Shopping App:

### Main Classes:
- **User**: Represents all users (customers, admins, support)
- **Product**: Products available for purchase with AR capabilities
- **Cart**: Shopping cart functionality
- **Order**: Order management and tracking
- **Payment**: Payment processing
- **Feedback**: User reviews and ratings
- **ARModel**: Augmented reality models for products
- **Chat**: Customer support chat system

### Key Relationships:
- Users can place multiple orders and submit feedback
- Products can be in multiple carts and orders
- Orders are linked to payments and shipping addresses
- AR models are associated with products
- Support staff handle customer chats

### Enums:
- User types, order statuses, payment statuses, and other enumerated values 