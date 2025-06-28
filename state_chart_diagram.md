# State Chart Diagram - Augmented Reality Shopping App

## User Account State Chart

```mermaid
stateDiagram-v2
    [*] --> Guest
    Guest --> Registered : Register
    Guest --> LoggedIn : Login
    Registered --> LoggedIn : Login
    LoggedIn --> Guest : Logout
    LoggedIn --> Active : Browse/Shop
    Active --> Inactive : Timeout
    Inactive --> Active : Activity
    Active --> Suspended : Violation
    Suspended --> Active : Admin Approval
    Active --> Deleted : Delete Account
    Deleted --> [*]
```

## Product State Chart

```mermaid
stateDiagram-v2
    [*] --> Draft
    Draft --> Active : Publish
    Active --> Inactive : Disable
    Inactive --> Active : Enable
    Active --> OutOfStock : Stock Depleted
    OutOfStock --> Active : Restock
    Active --> Discontinued : Discontinue
    Discontinued --> [*]
    
    note right of Draft
        Product created but not
        visible to customers
    end note
    
    note right of Active
        Available for purchase
        and AR try-on
    end note
    
    note right of OutOfStock
        Visible but cannot
        be added to cart
    end note
```

## Order State Chart

```mermaid
stateDiagram-v2
    [*] --> Pending
    Pending --> Confirmed : Payment Success
    Pending --> Cancelled : Cancel Order
    Pending --> Failed : Payment Failed
    
    Confirmed --> Processing : Start Processing
    Confirmed --> Cancelled : Cancel Order
    
    Processing --> Shipped : Ship Order
    Processing --> Cancelled : Cancel Order
    
    Shipped --> Delivered : Delivery Success
    Shipped --> Returned : Return Request
    Shipped --> Lost : Delivery Failed
    
    Delivered --> Returned : Return Request
    Delivered --> Completed : Feedback Submitted
    
    Returned --> Refunded : Process Refund
    Lost --> Refunded : Process Refund
    
    Refunded --> [*]
    Completed --> [*]
    Cancelled --> [*]
    Failed --> [*]
    
    note right of Pending
        Order placed, waiting
        for payment
    end note
    
    note right of Confirmed
        Payment received,
        order validated
    end note
    
    note right of Processing
        Items being picked
        and packed
    end note
```

## Payment State Chart

```mermaid
stateDiagram-v2
    [*] --> Initiated
    Initiated --> Processing : Submit Payment
    Initiated --> Cancelled : Cancel Payment
    
    Processing --> Completed : Payment Success
    Processing --> Failed : Payment Failure
    Processing --> Pending : Awaiting Confirmation
    
    Pending --> Completed : Confirmation Received
    Pending --> Failed : Confirmation Failed
    
    Completed --> Refunded : Process Refund
    Failed --> [*]
    Cancelled --> [*]
    Refunded --> [*]
    
    note right of Processing
        Payment gateway
        processing transaction
    end note
    
    note right of Pending
        Payment submitted but
        confirmation pending
    end note
```

## AR Session State Chart

```mermaid
stateDiagram-v2
    [*] --> Initializing
    Initializing --> CheckingCompatibility : Start AR
    Initializing --> Error : Initialization Failed
    
    CheckingCompatibility --> RequestingPermissions : Compatible
    CheckingCompatibility --> Error : Incompatible Device
    
    RequestingPermissions --> DetectingSurface : Permissions Granted
    RequestingPermissions --> Error : Permissions Denied
    
    DetectingSurface --> SurfaceFound : Surface Detected
    DetectingSurface --> DetectingSurface : Continue Detection
    
    SurfaceFound --> PlacingModel : User Taps
    PlacingModel --> ModelPlaced : Model Placed
    PlacingModel --> PlacingModel : Continue Placement
    
    ModelPlaced --> Interactive : Enter Interactive Mode
    Interactive --> Rotating : Rotate Model
    Interactive --> Scaling : Scale Model
    Interactive --> Moving : Move Model
    Interactive --> Capturing : Capture Photo
    Interactive --> Exiting : Exit AR
    
    Rotating --> Interactive : Rotation Complete
    Scaling --> Interactive : Scaling Complete
    Moving --> Interactive : Movement Complete
    Capturing --> Interactive : Photo Captured
    
    Exiting --> [*]
    Error --> [*]
    
    note right of Interactive
        User can manipulate
        the 3D model
    end note
```

## Support Ticket State Chart

```mermaid
stateDiagram-v2
    [*] --> Created
    Created --> Assigned : Assign to Agent
    Created --> Closed : Auto-close (Duplicate/Spam)
    
    Assigned --> InProgress : Agent Starts Working
    Assigned --> Reassigned : Reassign to Different Agent
    
    InProgress --> WaitingForCustomer : Need Customer Response
    InProgress --> Escalated : Escalate to Senior Agent
    InProgress --> Resolved : Issue Resolved
    
    WaitingForCustomer --> InProgress : Customer Responds
    WaitingForCustomer --> Closed : No Response (Timeout)
    
    Escalated --> InProgress : Senior Agent Takes Over
    Escalated --> Resolved : Issue Resolved
    
    Resolved --> Closed : Customer Confirms
    Resolved --> Reopened : Customer Reopens
    
    Reopened --> Assigned : Reassign to Agent
    Closed --> [*]
    
    note right of Created
        Customer submits
        support request
    end note
    
    note right of InProgress
        Agent actively
        working on issue
    end note
```

## Shopping Cart State Chart

```mermaid
stateDiagram-v2
    [*] --> Empty
    Empty --> Active : Add First Item
    Active --> Active : Add More Items
    Active --> Active : Remove Items
    Active --> Empty : Remove All Items
    Active --> Checkout : Proceed to Checkout
    Active --> Abandoned : Inactivity Timeout
    
    Checkout --> Processing : Payment Processing
    Checkout --> Active : Return to Cart
    
    Processing --> Completed : Payment Success
    Processing --> Active : Payment Failed
    
    Completed --> [*]
    Abandoned --> [*]
    Empty --> [*]
    
    note right of Active
        Cart has items and
        is being modified
    end note
    
    note right of Abandoned
        Cart with items but
        no activity for 24h
    end note
```

## State Chart Description

### User Account States:
- **Guest**: Unregistered user with limited access
- **Registered**: User account created but not logged in
- **LoggedIn**: Authenticated user session
- **Active**: User actively using the application
- **Inactive**: Session timeout, requires re-authentication
- **Suspended**: Account temporarily suspended
- **Deleted**: Account permanently removed

### Product States:
- **Draft**: Product created but not published
- **Active**: Available for purchase and AR try-on
- **Inactive**: Temporarily disabled
- **OutOfStock**: Visible but cannot be purchased
- **Discontinued**: Product no longer available

### Order States:
- **Pending**: Order placed, payment pending
- **Confirmed**: Payment received, order validated
- **Processing**: Items being prepared for shipping
- **Shipped**: Order dispatched with tracking
- **Delivered**: Successfully delivered to customer
- **Returned**: Customer returned the order
- **Refunded**: Money returned to customer
- **Completed**: Order fulfilled with feedback
- **Cancelled**: Order cancelled before shipping
- **Failed**: Payment failed, order not confirmed
- **Lost**: Order lost in transit

### Payment States:
- **Initiated**: Payment request created
- **Processing**: Payment gateway processing
- **Pending**: Awaiting confirmation
- **Completed**: Payment successful
- **Failed**: Payment failed
- **Refunded**: Payment returned to customer
- **Cancelled**: Payment cancelled

### AR Session States:
- **Initializing**: Starting AR session
- **CheckingCompatibility**: Validating device capabilities
- **RequestingPermissions**: Getting camera/sensor access
- **DetectingSurface**: Finding AR plane
- **SurfaceFound**: AR plane detected
- **PlacingModel**: User positioning 3D model
- **ModelPlaced**: 3D model positioned
- **Interactive**: User manipulating model
- **Exiting**: Ending AR session

### Support Ticket States:
- **Created**: Ticket submitted by customer
- **Assigned**: Assigned to support agent
- **InProgress**: Agent actively working
- **WaitingForCustomer**: Awaiting customer response
- **Escalated**: Moved to senior agent
- **Resolved**: Issue resolved
- **Reopened**: Customer reopened resolved ticket
- **Closed**: Ticket permanently closed

### Shopping Cart States:
- **Empty**: No items in cart
- **Active**: Items in cart, being modified
- **Checkout**: User proceeding to payment
- **Processing**: Payment being processed
- **Completed**: Purchase completed
- **Abandoned**: Cart with items but inactive

### Key State Transitions:
- **Triggers**: Events that cause state changes
- **Conditions**: Business rules for transitions
- **Actions**: Operations performed during transitions
- **Guards**: Validation checks before transitions 