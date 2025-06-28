# Activity Diagram - Augmented Reality Shopping App

## Main User Shopping Flow

```mermaid
flowchart TD
    Start([Start]) --> Login{User Logged In?}
    Login -->|No| Register[Register/Login]
    Login -->|Yes| Browse[Browse Products]
    Register --> Browse
    
    Browse --> Search[Search Products]
    Search --> ViewDetails[View Product Details]
    ViewDetails --> TryAR{Try in AR?}
    
    TryAR -->|Yes| ARExperience[Launch AR Experience]
    TryAR -->|No| AddToCart{Add to Cart?}
    ARExperience --> AddToCart
    
    AddToCart -->|Yes| Cart[Add to Cart]
    AddToCart -->|No| Browse
    Cart --> ContinueShopping{Continue Shopping?}
    
    ContinueShopping -->|Yes| Browse
    ContinueShopping -->|No| Checkout[Proceed to Checkout]
    
    Checkout --> ValidateCart{Valid Cart?}
    ValidateCart -->|No| Cart
    ValidateCart -->|Yes| Shipping[Enter Shipping Details]
    
    Shipping --> Payment[Make Payment]
    Payment --> PaymentSuccess{Payment Successful?}
    
    PaymentSuccess -->|No| Payment
    PaymentSuccess -->|Yes| OrderConfirmation[Order Confirmed]
    
    OrderConfirmation --> TrackOrder[Track Order]
    TrackOrder --> Feedback{Submit Feedback?}
    
    Feedback -->|Yes| SubmitFeedback[Submit Feedback]
    Feedback -->|No| End([End])
    SubmitFeedback --> End
```

## AR Try-On Experience Flow

```mermaid
flowchart TD
    Start([Start AR Experience]) --> LoadModel[Load AR Model]
    LoadModel --> CheckDevice{Device Compatible?}
    
    CheckDevice -->|No| ShowError[Show Compatibility Error]
    CheckDevice -->|Yes| RequestPermissions[Request Camera Permissions]
    
    RequestPermissions --> PermissionsGranted{Permissions Granted?}
    PermissionsGranted -->|No| ShowError
    PermissionsGranted -->|Yes| InitializeAR[Initialize AR Session]
    
    InitializeAR --> DetectSurface[Detect Surface]
    DetectSurface --> SurfaceFound{Surface Found?}
    
    SurfaceFound -->|No| ShowInstructions[Show Surface Detection Instructions]
    SurfaceFound -->|Yes| PlaceModel[Place 3D Model]
    
    ShowInstructions --> DetectSurface
    PlaceModel --> ModelPlaced{Model Placed?}
    
    ModelPlaced -->|No| PlaceModel
    ModelPlaced -->|Yes| InteractiveMode[Interactive Mode]
    
    InteractiveMode --> UserActions{User Actions}
    UserActions -->|Rotate| RotateModel[Rotate Model]
    UserActions -->|Scale| ScaleModel[Scale Model]
    UserActions -->|Move| MoveModel[Move Model]
    UserActions -->|Capture| CapturePhoto[Capture Photo]
    UserActions -->|Exit| ExitAR[Exit AR Mode]
    
    RotateModel --> InteractiveMode
    ScaleModel --> InteractiveMode
    MoveModel --> InteractiveMode
    CapturePhoto --> SavePhoto[Save Photo]
    SavePhoto --> InteractiveMode
    ExitAR --> End([End AR Experience])
```

## Order Processing and Tracking Flow

```mermaid
flowchart TD
    Start([Order Placed]) --> PaymentProcessing[Payment Processing]
    PaymentProcessing --> PaymentStatus{Payment Status}
    
    PaymentStatus -->|Failed| PaymentRetry[Retry Payment]
    PaymentStatus -->|Successful| OrderConfirmed[Order Confirmed]
    
    PaymentRetry --> PaymentProcessing
    OrderConfirmed --> InventoryCheck[Check Inventory]
    
    InventoryCheck --> StockAvailable{Stock Available?}
    StockAvailable -->|No| Backorder[Backorder Item]
    StockAvailable -->|Yes| ProcessOrder[Process Order]
    
    Backorder --> NotifyCustomer[Notify Customer]
    ProcessOrder --> PickItems[Pick Items]
    
    PickItems --> PackItems[Pack Items]
    PackItems --> GenerateLabel[Generate Shipping Label]
    
    GenerateLabel --> ShipOrder[Ship Order]
    ShipOrder --> UpdateStatus[Update Order Status]
    
    UpdateStatus --> TrackingNumber[Send Tracking Number]
    TrackingNumber --> InTransit[In Transit]
    
    InTransit --> DeliveryStatus{Delivery Status}
    DeliveryStatus -->|Delivered| Delivered[Delivered]
    DeliveryStatus -->|Failed| DeliveryFailed[Delivery Failed]
    
    Delivered --> RequestFeedback[Request Feedback]
    DeliveryFailed --> Reschedule[Reschedule Delivery]
    
    Reschedule --> InTransit
    RequestFeedback --> End([End])
```

## Customer Support Flow

```mermaid
flowchart TD
    Start([Customer Needs Support]) --> SupportChannel{Support Channel}
    
    SupportChannel -->|Chat| InitiateChat[Initiate Chat]
    SupportChannel -->|Email| SendEmail[Send Email]
    SupportChannel -->|Phone| CallSupport[Call Support]
    
    InitiateChat --> ChatQueue[Enter Chat Queue]
    SendEmail --> EmailQueue[Enter Email Queue]
    CallSupport --> CallQueue[Enter Call Queue]
    
    ChatQueue --> AssignAgent[Assign Support Agent]
    EmailQueue --> AssignAgent
    CallQueue --> AssignAgent
    
    AssignAgent --> AgentAvailable{Agent Available?}
    AgentAvailable -->|No| WaitQueue[Wait in Queue]
    AgentAvailable -->|Yes| StartSession[Start Support Session]
    
    WaitQueue --> AssignAgent
    StartSession --> IdentifyIssue[Identify Issue]
    
    IdentifyIssue --> IssueType{Issue Type}
    IssueType -->|Order Related| OrderSupport[Order Support]
    IssueType -->|Product Related| ProductSupport[Product Support]
    IssueType -->|Technical| TechnicalSupport[Technical Support]
    IssueType -->|Payment| PaymentSupport[Payment Support]
    
    OrderSupport --> ResolveOrder[Resolve Order Issue]
    ProductSupport --> ResolveProduct[Resolve Product Issue]
    TechnicalSupport --> ResolveTechnical[Resolve Technical Issue]
    PaymentSupport --> ResolvePayment[Resolve Payment Issue]
    
    ResolveOrder --> IssueResolved{Issue Resolved?}
    ResolveProduct --> IssueResolved
    ResolveTechnical --> IssueResolved
    ResolvePayment --> IssueResolved
    
    IssueResolved -->|No| Escalate[Escalate Issue]
    IssueResolved -->|Yes| CloseTicket[Close Support Ticket]
    
    Escalate --> EscalatedSupport[Escalated Support]
    EscalatedSupport --> IssueResolved
    CloseTicket --> End([End])
```

## Admin Management Flow

```mermaid
flowchart TD
    Start([Admin Login]) --> AdminDashboard[Admin Dashboard]
    AdminDashboard --> AdminAction{Admin Action}
    
    AdminAction -->|Manage Products| ProductManagement[Product Management]
    AdminAction -->|View Orders| OrderManagement[Order Management]
    AdminAction -->|Generate Reports| ReportGeneration[Report Generation]
    AdminAction -->|Customer Support| SupportManagement[Support Management]
    
    ProductManagement --> ProductAction{Product Action}
    ProductAction -->|Add Product| AddProduct[Add New Product]
    ProductAction -->|Edit Product| EditProduct[Edit Existing Product]
    ProductAction -->|Delete Product| DeleteProduct[Delete Product]
    ProductAction -->|Manage Inventory| ManageInventory[Manage Inventory]
    
    AddProduct --> ValidateProduct{Product Valid?}
    EditProduct --> ValidateProduct
    ValidateProduct -->|No| ShowError[Show Validation Error]
    ValidateProduct -->|Yes| SaveProduct[Save Product]
    
    ShowError --> ProductManagement
    SaveProduct --> ProductManagement
    
    OrderManagement --> OrderAction{Order Action}
    OrderAction -->|View Orders| ViewOrders[View All Orders]
    OrderAction -->|Update Status| UpdateOrderStatus[Update Order Status]
    OrderAction -->|Process Refunds| ProcessRefunds[Process Refunds]
    
    ViewOrders --> FilterOrders[Filter Orders]
    UpdateOrderStatus --> NotifyCustomer[Notify Customer]
    ProcessRefunds --> RefundProcessed[Refund Processed]
    
    ReportGeneration --> ReportType{Report Type}
    ReportType -->|Sales Report| SalesReport[Generate Sales Report]
    ReportType -->|Inventory Report| InventoryReport[Generate Inventory Report]
    ReportType -->|User Activity| UserActivityReport[Generate User Activity Report]
    
    SalesReport --> ExportReport[Export Report]
    InventoryReport --> ExportReport
    UserActivityReport --> ExportReport
    
    SupportManagement --> SupportAction{Support Action}
    SupportAction -->|View Tickets| ViewTickets[View Support Tickets]
    SupportAction -->|Assign Agents| AssignAgents[Assign Support Agents]
    SupportAction -->|Monitor Performance| MonitorPerformance[Monitor Support Performance]
    
    ViewTickets --> TicketStatus{Update Ticket Status}
    AssignAgents --> AgentAssignment[Agent Assignment]
    MonitorPerformance --> PerformanceMetrics[Performance Metrics]
    
    End([End Admin Session])
```

## Activity Diagram Description

### Main User Shopping Flow:
- **Authentication**: Registration and login process
- **Product Discovery**: Browsing, searching, and viewing products
- **AR Experience**: Optional AR try-on before purchase
- **Cart Management**: Adding items and managing cart
- **Checkout Process**: Shipping details and payment
- **Post-Purchase**: Order tracking and feedback

### AR Try-On Experience:
- **Device Compatibility**: Checks for AR capabilities
- **Permissions**: Camera and sensor access
- **Surface Detection**: AR plane detection
- **Interactive Mode**: Model manipulation and capture
- **User Controls**: Rotate, scale, move, and capture

### Order Processing:
- **Payment Processing**: Secure transaction handling
- **Inventory Management**: Stock verification and updates
- **Fulfillment**: Picking, packing, and shipping
- **Tracking**: Real-time order status updates
- **Delivery**: Final delivery and feedback collection

### Customer Support:
- **Multi-channel Support**: Chat, email, and phone
- **Queue Management**: Efficient agent assignment
- **Issue Classification**: Categorizing support requests
- **Resolution Process**: Problem-solving and escalation
- **Ticket Management**: Tracking and closing support cases

### Admin Management:
- **Product Management**: CRUD operations for products
- **Order Oversight**: Monitoring and updating orders
- **Reporting**: Analytics and business intelligence
- **Support Coordination**: Managing customer support operations

### Key Decision Points:
- Payment success/failure handling
- Stock availability checks
- Support issue resolution
- Order status transitions
- AR compatibility validation 