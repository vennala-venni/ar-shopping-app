# Class Diagram - Augmented Reality Shopping App

```mermaid
classDiagram
    class User {
        -userId: String
        -username: String
        -email: String
        -password: String
        -phoneNumber: String
        -userType: String
        +register()
        +login()
        +logout()
        +updateProfile()
    }

    class Admin {
        -adminId: String
        -permissions: String
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
        -price: Number
        -brand: String
        -stockQuantity: Number
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
        -totalAmount: Number
        +addItem()
        +removeItem()
        +updateQuantity()
        +calculateTotal()
        +clear()
    }

    class CartItem {
        -itemId: String
        -productId: String
        -quantity: Number
        -price: Number
        +updateQuantity()
        +calculateSubtotal()
    }

    class Order {
        -orderId: String
        -userId: String
        -orderDate: String
        -status: String
        -totalAmount: Number
        +placeOrder()
        +cancelOrder()
        +trackOrder()
        +updateStatus()
    }

    class OrderItem {
        -itemId: String
        -productId: String
        -quantity: Number
        -price: Number
        +calculateSubtotal()
    }

    class Payment {
        -paymentId: String
        -orderId: String
        -amount: Number
        -paymentMethod: String
        -status: String
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
        -rating: Number
        -comment: String
        -date: String
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
        -status: String
        +sendMessage()
        +endChat()
    }

    class Message {
        -messageId: String
        -senderId: String
        -content: String
        -timestamp: String
        -type: String
    }

    class Report {
        -reportId: String
        -type: String
        -data: String
        -generatedDate: String
        +generateReport()
        +exportReport()
    }

    User ||--o{ Order : places
    User ||--o{ Feedback : submits
    User ||--o{ Chat : participates
    User ||--|| Cart : has

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
- Orders are linked to payments
- AR models are associated with products
- Support staff handle customer chats

### Data Types:
- **String**: Text data (IDs, names, descriptions)
- **Number**: Numeric values (prices, quantities, ratings) 
