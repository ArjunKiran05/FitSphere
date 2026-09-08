# FitSphere — Intelligent Fitness Microservices Platform

FitSphere is a backend-focused fitness platform built with Java and Spring Boot using a microservices architecture. The system separates core domains into independently deployable services and combines synchronous REST communication, asynchronous messaging, relational and NoSQL persistence, service discovery, API gateway routing, and AI-powered fitness recommendations.

## Architecture

```text
                         ┌──────────────────────┐
                         │   React Frontend     │
                         │   fitness-app-front  │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │       Gateway        │
                         │   API Gateway/Route  │
                         └──────────┬───────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
       ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
       │ UserService │      │ ActivitySvc │      │  AI Service │
       └──────┬──────┘      └──────┬──────┘      └──────┬──────┘
              │                    │                     │
              ▼                    ▼                     ▼
       ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
       │ PostgreSQL  │      │  MongoDB    │      │ Gemini API  │
       └─────────────┘      └─────────────┘      └─────────────┘

                 ┌───────────────────────────────┐
                 │     Service Discovery         │
                 │     Eureka Server             │
                 └───────────────────────────────┘

                 ┌───────────────────────────────┐
                 │     Config Server             │
                 │ Centralized configuration     │
                 └───────────────────────────────┘

                 ┌───────────────────────────────┐
                 │        RabbitMQ               │
                 │ Async event communication     │
                 └───────────────────────────────┘
```

## Services

### User Service
Handles user-related functionality and persists application data in PostgreSQL.

### Activity Service
Manages fitness/activity-related operations and uses MongoDB for activity-oriented data persistence.

### AI Service
Integrates with Google Gemini to generate AI-powered personalized fitness recommendations.

### API Gateway
Provides a single entry point for client requests and routes traffic to the appropriate microservice.

### Eureka Server
Provides service discovery so microservices can locate and communicate with one another without hard-coded service locations.

### Config Server
Centralizes configuration for the microservices and keeps service-specific configuration separate from application code.

### React Frontend
Provides the client-side interface for interacting with the fitness platform.

## Technology Stack

- **Backend:** Java, Spring Boot, Spring Cloud
- **Service Discovery:** Netflix Eureka
- **API Gateway:** Spring Cloud Gateway
- **Synchronous Communication:** REST, Spring WebClient
- **Asynchronous Communication:** RabbitMQ
- **Databases:** PostgreSQL, MongoDB
- **AI:** Google Gemini API
- **Frontend:** React.js
- **Containerization:** Docker
- **Build:** Maven
- **Version Control:** Git, GitHub

## Key Engineering Concepts

FitSphere demonstrates:

- Microservices architecture with independently deployable services
- Service discovery with Eureka
- API gateway-based request routing
- Synchronous inter-service communication using WebClient
- Asynchronous, event-driven communication with RabbitMQ
- Polyglot persistence using PostgreSQL and MongoDB
- Centralized configuration management
- Layered architecture and dependency injection with Spring Boot
- Exception handling and REST API design
- AI integration for personalized application features
- Docker-based service containerization

## Project Structure

```text
FitSphere/
├── activityservice/
├── aiservice/
├── configserver/
├── eureka/
├── gateway/
├── userservice/
└── fitness-app-frontend/
```

## Running the Project Locally

### Prerequisites

Make sure the following are installed:

- Java 17+
- Maven
- Node.js and npm
- PostgreSQL
- MongoDB
- RabbitMQ
- Docker (optional)

### Environment Variables

Sensitive configuration should be supplied through environment variables rather than committed to Git.

For example:

```text
DB_URL=jdbc:postgresql://localhost:5432/fitness_user_db
DB_USERNAME=postgres
DB_PASSWORD=<your_database_password>
GEMINI_API_URL=<your_gemini_api_url>
GEMINI_API_KEY=<your_gemini_api_key>
```

See `configserver/.env.example` for the repository's example configuration format.

### Backend

Start the infrastructure services and then run the Spring Boot services in an order that allows service discovery and centralized configuration to become available:

1. Config Server
2. Eureka Server
3. User Service
4. Activity Service
5. AI Service
6. API Gateway

Each service can be started from its own directory using Maven.

```bash
mvn spring-boot:run
```

### Frontend

From the frontend directory:

```bash
npm install
npm start
```

The exact frontend command may vary according to the package configuration in `fitness-app-frontend`.

## Configuration & Security

Do not commit database passwords, API keys, or other secrets. Local credentials should be supplied using environment variables or another local secret-management mechanism.

## Future Improvements

- Add centralized authentication and authorization
- Introduce distributed tracing and centralized logging
- Expand automated integration and contract testing
- Add CI/CD with GitHub Actions
- Improve fault tolerance with retries, timeouts, and circuit breakers
- Expand observability and production deployment support

## Author

**Arjun K**

GitHub: https://github.com/ArjunKiran05
