# Sequence Diagram - Augmented Reality Shopping App

## Main Purchase Flow with AR Try-On

```mermaid
sequenceDiagram
    participant U as User
    participant UI as User Interface
    participant AS as Auth Service
    participant PS as Product Service
    participant CS as Cart Service
    participant OS as Order Service
    participant PMS as Payment Service
    participant ARS as AR Service
    participant NS as Notification Service

    Note over U, NS: User Registration and Login Flow
    U->>UI: Register/Login
    UI->>AS: Authenticate User
    AS-->>UI: Authentication Result
    UI-->>U: Login Success

    Note over U, NS: Product Browsing and Search
    U->>UI: Browse Products
    UI->>PS: Get Product List
    PS-->>UI: Product Catalog
    UI-->>U: Display Products

    U->>UI: Search Product
    UI->>PS: Search Products
    PS-->>UI: Search Results
    UI-->>U: Display Search Results

    Note over U, NS: Product Details and AR Try-On
    U->>UI: View Product Details
    UI->>PS: Get Product Details
    PS-->>UI: Product Information
    UI-->>U: Show Product Details

    U->>UI: Try in AR
    UI->>ARS: Load AR Model
    ARS->>PS: Get AR Model URL
    PS-->>ARS: AR Model Data
    ARS-->>UI: AR Model Ready
    UI-->>U: Launch AR Experience

    Note over U, NS: Add to Cart
    U->>UI: Add to Cart
    UI->>CS: Add Item to Cart
    CS->>PS: Check Stock Availability
    PS-->>CS: Stock Status
    CS-->>UI: Cart Updated
    UI-->>U: Item Added to Cart

    Note over U, NS: Checkout Process
    U->>UI: Proceed to Checkout
    UI->>CS: Get Cart Items
    CS-->>UI: Cart Contents
    UI-->>U: Show Checkout Form

    U->>UI: Enter Shipping Details
    UI->>OS: Validate Address
    OS-->>UI: Address Valid
    UI-->>U: Address Confirmed

    Note over U, NS: Payment Processing
    U->>UI: Make Payment
    UI->>PMS: Process Payment
    PMS->>OS: Create Order
    OS->>PS: Update Stock
    PS-->>OS: Stock Updated
    OS-->>PMS: Order Created
    PMS-->>UI: Payment Success
    UI-->>U: Order Confirmed

    Note over U, NS: Order Tracking
    U->>UI: Track Order
    UI->>OS: Get Order Status
    OS-->>UI: Order Details
    UI-->>U: Show Order Status

    Note over U, NS: Customer Support
    U->>UI: Chat Support
    UI->>NS: Initiate Chat
    NS-->>UI: Chat Session
    UI-->>U: Chat Interface

    Note over U, NS: Feedback Submission
    U->>UI: Submit Feedback
    UI->>PS: Save Feedback
    PS-->>UI: Feedback Saved
    UI-->>U: Feedback Submitted
```

## Order Cancellation Flow

```mermaid
sequenceDiagram
    participant U as User
    participant UI as User Interface
    participant OS as Order Service
    participant PMS as Payment Service
    participant PS as Product Service
    participant NS as Notification Service

    U->>UI: Cancel Order
    UI->>OS: Request Cancellation
    OS->>OS: Check Order Status
    alt Order Can Be Cancelled
        OS->>PMS: Process Refund
        PMS-->>OS: Refund Processed
        OS->>PS: Restore Stock
        PS-->>OS: Stock Restored
        OS-->>UI: Order Cancelled
        UI-->>U: Cancellation Confirmed
        OS->>NS: Send Cancellation Email
    else Order Cannot Be Cancelled
        OS-->>UI: Cancellation Denied
        UI-->>U: Show Error Message
    end
```

## Admin Management Flow

```mermaid
sequenceDiagram
    participant A as Admin
    participant UI as Admin Interface
    participant PS as Product Service
    participant OS as Order Service
    participant RS as Report Service
    participant NS as Notification Service

    A->>UI: Login as Admin
    UI->>A: Admin Dashboard

    Note over A, NS: Product Management
    A->>UI: Manage Products
    UI->>PS: Get Product List
    PS-->>UI: All Products
    UI-->>A: Product Management Interface

    A->>UI: Add/Edit Product
    UI->>PS: Save Product
    PS-->>UI: Product Saved
    UI-->>A: Product Updated

    Note over A, NS: Order Management
    A->>UI: View Orders
    UI->>OS: Get All Orders
    OS-->>UI: Order List
    UI-->>A: Order Management Interface

    A->>UI: Update Order Status
    UI->>OS: Update Status
    OS->>NS: Notify Customer
    OS-->>UI: Status Updated
    UI-->>A: Order Status Changed

    Note over A, NS: Report Generation
    A->>UI: Generate Reports
    UI->>RS: Create Report
    RS->>OS: Get Order Data
    OS-->>RS: Order Statistics
    RS->>PS: Get Product Data
    PS-->>RS: Product Statistics
    RS-->>UI: Report Generated
    UI-->>A: Download Report
```

## Sequence Diagram Description

### Main Purchase Flow:
1. **Authentication**: User registers/logs in
2. **Product Discovery**: Browse and search products
3. **AR Experience**: Try products in augmented reality
4. **Cart Management**: Add items to cart
5. **Checkout**: Complete purchase with payment
6. **Order Tracking**: Monitor order status
7. **Support**: Access customer support when needed
8. **Feedback**: Submit product reviews

### Key Interactions:
- **AR Service**: Handles 3D model loading and rendering
- **Payment Service**: Processes transactions securely
- **Order Service**: Manages order lifecycle
- **Notification Service**: Sends updates to users
- **Product Service**: Manages inventory and product data

### Error Handling:
- Stock availability checks
- Payment validation
- Order cancellation rules
- Address validation

### Admin Functions:
- Product management
- Order oversight
- Report generation
- Customer support coordination 