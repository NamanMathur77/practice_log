## Microservices
1. In microservice architecture the application is broken down into small independent services.
2. Each service has its own logic, database, API.
3. Communication with other services is done using APIs or message queues(like kafka, rabbitmq)

### In a Monolith:

You’d have one big project handling:

1. Authentication
2. Product management
3. Orders
4. Payments
5. Notifications

Everything shares the same database and codebase.

### In Microservices:

You’d break it into smaller services:

1. AuthService → manages login, JWT tokens, users
2. ProductService → manages products and inventory
3. OrderService → handles order creation and tracking
4. PaymentService → processes payments
5. NotificationService → sends emails/SMS

Each service has its own:
Database (SQL, MongoDB, etc.)
API endpoints
Deployment pipeline

### Benefits
1. independent deployment
2. Scalability
3. Fault isolation
4. Tech flexibility
5. Faster deployment

