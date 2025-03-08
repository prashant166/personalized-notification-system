# Personalized Notification System

## Assignment Overview

This assignment consists of three main services (User, Product, and Order) and a GraphQL API Gateway that provides a unified interface for client applications. It can also be accessed throught simple HTTP methods.

## Architecture

The system is built using a microservices architecture, with each service responsible for a specific domain:

- User Service: Manages user accounts and authentication
- Product Service: Handles product catalog and inventory
- Order Service: Processes and manages orders
- GraphQL API Gateway: Provides a single entry point for client applications

Services communicate with each other using a message queue (RabbitMQ) for asynchronous operations and REST APIs for synchronous operations.

## Services

### User Service

- **Port**: 3301
- **Responsibilities**: User registration, authentication, profile management
- **Database**: MongoDB
- **Key Endpoints**:
  - POST /api/users/register -- Register a user
  - POST /api/users/login -- Login the user
  - GET /api/users/profile -- Fetch user details
  - PUT /api/users/profile -- Update details of user

### Product Service

- **Port**: 3302
- **Responsibilities**: Product management, inventory updates
- **Database**: MongoDB
- **Key Endpoints**:
  - POST /api/products -- Create a new product 
  - GET /api/products -- Fetch all existing products
  - GET /api/products/:id -- Fetch a specific product by it's product_id
  - PUT /api/products/:id -- Update details of a specific product
  - DELETE /api/products/:id -- Delete a product

### Order Service

- **Port**: 3303
- **Responsibilities**: Order processing and management
- **Database**: MongoDB
- **Key Endpoints**:
  - POST /api/orders -- Create an order
  - GET /api/orders -- Fetch all existing orders
  - GET /api/orders/:id -- Fetch a specific order by order_id
  - GET /api/orders/user/:userId -- Fetch all orders by a specific user by their userId
  - PUT /api/orders/:id/status -- Update the status of delivery of the order

### GraphQL API Gateway

- **Port**: 4000
- **Responsibilities**: Unified API for client applications, data aggregation
- **Key Endpoint**: /graphql

## Setup and Installation

1. Clone the repository:
   ```
   git clone https://github.com/prashant166/personalized-notification-system.git
   cd personalized-notification-system
   ```

2. The entire project, including all microservices, RabbitMQ, Prometheus, and Grafana, can be started using a single script.

3. Ensure you have Docker and Docker Compose installed on your system.

4. Navigate to the root directory of the project.

5. Run the start script:
   ```
   ./scripts/start.sh
   ```

   This script does the following:
   - Builds Docker images for all services if they don't exist
   - Starts all services defined in the `docker-compose.yml` file
   - Waits for all services to be healthy before exiting

6. To stop all services, you can use:
   ```
   docker-compose down
   ```

7. All logs will be available for each service under the logs folder.

## API Documentation

Detailed API documentation can be found in the `/docs` directory of each service.

- [User Service API](./services/user-service/docs/README.md)
- [Product Service API](./services/product-service/docs/README.md)
- [Order Service API](./services/order-service/docs/README.md)

## Authentication

The system uses JWT (JSON Web Tokens) for authentication. To access protected endpoints, include the JWT in the Authorization header:

```
Authorization: Bearer <your_jwt_token>
```

To obtain a token, use the login endpoint of the User Service.

## Database

Each service uses its own MongoDB database. Ensure MongoDB is installed and running, or update the `MONGODB_URI` in the `.env` files to point to your MongoDB instances.

## Message Queue

RabbitMQ is used for inter-service communication. Ensure RabbitMQ is installed and running, or update the `RABBITMQ_URL` in the `.env` files to point to your RabbitMQ instance.


## Testing

To run tests for each service:

```
cd services/<each-service>
npm run test
```

## Service URLs

Here are the URLs for accessing various services in the project:

### Microservices
- User Service:     http://localhost:3301
- Product Service:  http://localhost:3302
- Order Service:    http://localhost:3303

```bash
./scripts/start.sh
```
