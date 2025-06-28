# Object Diagram - Augmented Reality Shopping App

```mermaid
objectDiagram
    object user1 {
        userId = "U001"
        username = "john_doe"
        email = "john@example.com"
        phoneNumber = "+1234567890"
        userType = CUSTOMER
    }

    object admin1 {
        adminId = "A001"
        permissions = ["MANAGE_PRODUCTS", "VIEW_ORDERS", "GENERATE_REPORTS"]
    }

    object support1 {
        supportId = "S001"
        specialization = "Technical Support"
    }

    object product1 {
        productId = "P001"
        name = "Nike Air Max 270"
        description = "Comfortable running shoes with Air Max technology"
        price = 129.99
        brand = "Nike"
        stockQuantity = 50
    }

    object product2 {
        productId = "P002"
        name = "iPhone 15 Pro"
        description = "Latest iPhone with advanced camera system"
        price = 999.99
        brand = "Apple"
        stockQuantity = 25
    }

    object category1 {
        categoryId = "C001"
        name = "Footwear"
        description = "Shoes and sneakers"
    }

    object category2 {
        categoryId = "C002"
        name = "Electronics"
        description = "Mobile phones and gadgets"
    }

    object cart1 {
        cartId = "CART001"
        userId = "U001"
        totalAmount = 129.99
    }

    object cartItem1 {
        itemId = "CI001"
        productId = "P001"
        quantity = 1
        price = 129.99
    }

    object order1 {
        orderId = "ORD001"
        userId = "U001"
        orderDate = "2024-01-15T10:30:00Z"
        status = CONFIRMED
        totalAmount = 129.99
    }

    object orderItem1 {
        itemId = "OI001"
        productId = "P001"
        quantity = 1
        price = 129.99
    }

    object payment1 {
        paymentId = "PAY001"
        orderId = "ORD001"
        amount = 129.99
        paymentMethod = CREDIT_CARD
        status = COMPLETED
        transactionDate = "2024-01-15T10:35:00Z"
    }

    object address1 {
        addressId = "ADD001"
        street = "123 Main Street"
        city = "New York"
        state = "NY"
        zipCode = "10001"
        country = "USA"
    }

    object feedback1 {
        feedbackId = "FB001"
        userId = "U001"
        productId = "P001"
        rating = 5
        comment = "Great shoes, very comfortable!"
        date = "2024-01-20T14:00:00Z"
    }

    object arModel1 {
        modelId = "AR001"
        productId = "P001"
        modelUrl = "https://models.example.com/nike-air-max-270.glb"
        modelType = "GLB"
    }

    object chat1 {
        chatId = "CHAT001"
        userId = "U001"
        supportId = "S001"
        status = ACTIVE
    }

    object message1 {
        messageId = "MSG001"
        senderId = "U001"
        content = "I have a question about my order"
        timestamp = "2024-01-16T09:00:00Z"
        type = TEXT
    }

    object message2 {
        messageId = "MSG002"
        senderId = "S001"
        content = "Hello! I'd be happy to help you with your order"
        timestamp = "2024-01-16T09:02:00Z"
        type = TEXT
    }

    object report1 {
        reportId = "REP001"
        type = SALES
        data = "Monthly sales report for January 2024"
        generatedDate = "2024-02-01T00:00:00Z"
    }

    %% Relationships
    user1 ||--|| cart1 : has
    user1 ||--o{ order1 : places
    user1 ||--o{ feedback1 : submits
    user1 ||--o{ chat1 : participates

    admin1 ||--o{ report1 : generates

    support1 ||--o{ chat1 : handles

    product1 ||--|| category1 : belongs_to
    product2 ||--|| category2 : belongs_to
    product1 ||--|| arModel1 : has

    cart1 ||--o{ cartItem1 : contains
    cartItem1 ||--|| product1 : references

    order1 ||--o{ orderItem1 : contains
    orderItem1 ||--|| product1 : references
    order1 ||--|| payment1 : has
    order1 ||--|| address1 : shipped_to

    chat1 ||--o{ message1 : contains
    chat1 ||--o{ message2 : contains
```

## Object Diagram Description

This object diagram shows specific instances of the classes with their actual attribute values:

### Key Instances:
- **User**: John Doe (customer)
- **Admin**: Admin with product management permissions
- **Support**: Technical support specialist
- **Products**: Nike shoes and iPhone with specific details
- **Order**: A confirmed order for Nike shoes
- **Payment**: Completed credit card payment
- **Chat**: Active support conversation

### Instance Relationships:
- User John has a cart with Nike shoes
- The order is linked to payment and shipping address
- Support staff is handling the customer's chat
- Products are categorized and have AR models
- Feedback is submitted for the purchased product

### Real-world Values:
- Actual prices, IDs, and timestamps
- Realistic product names and descriptions
- Proper relationships between instances 