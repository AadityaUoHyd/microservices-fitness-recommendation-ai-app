# Microservices Fitness Recommendation AI App  
App where a user provides their activity type, duration (in minutes), and calories burnt — and in response
this AI‑powered app gives a fitness recommendation. Demo Microservices Project.

## Table of Contents  
- [Technologies Used](#technologies‑used)  
- [Getting Started](#getting‑started)  
  - [Prerequisites](#prerequisites)  
  - [Clone the repository](#clone‑the‑repository)  
  - [Configuration](#configuration)  
  - [Running the services](#running‑the‑services)  
- [Architecture & Components](#architecture‑&‑components)  
- [Features](#features)  
- [How It Works](#how‑it‑works)  
- [Development & Extending](#development‑&‑extending)  
- [Deployment](#deployment)  
- [Contributing](#contributing)  
- [License](#license)  
- [Contact](#contact)  

## Technologies Used  
- Backend: Spring Boot (Java)  
- Databases: PostgreSQL, MongoDB  
- Messaging / Eventing: Apache Kafka, RabbitMQ  
- Containerisation: Docker  
- Frontend: React.js  
- Microservices architecture (multiple services, API gateway)  
- Additional: REST APIs, event‑driven design  

## Getting Started  

### Prerequisites  
Before you begin, ensure you have:  
- Docker & Docker Compose installed  
- Java 21+ (if running services directly via Spring Boot)  
- Node.js + npm/yarn (for the React frontend)  
- Git  

### Clone the repository  
```bash
git clone https://github.com/AadityaUoHyd/microservices-fitness-recommendation-ai-app.git
cd microservices-fitness-recommendation-ai-app
````

### Configuration

* There should be configuration files (application.properties / application.yml) for each service (backend microservices, config server etc.).
* Setup environment variables or local config values for:

    * PostgreSQL connection (hostname, port, db name, username, password)
    * MongoDB connection
    * Kafka / RabbitMQ endpoints
    * Ports for each microservice / API Gateway
* In `docker-compose.yml` (if provided) you may need to adjust volumes, network, ports, credentials for local testing.

### Running the services

#### Option A: Using Docker Compose

```bash
docker‑compose up --build
```

This should spin up all required services (PostgreSQL, MongoDB, Kafka, RabbitMQ, microservices, frontend).
Open the browser at something like `http://localhost:<gateway-port>` to access the frontend.

#### Option B: Running locally (development mode)

* Run each Spring Boot service individually via IDE or `mvn spring-boot:run`.
* Run frontend via `cd frontend && npm install && npm start`.
* Ensure all dependencies (databases, brokers) are running locally.

## Architecture & Components

This project follows a microservices architecture composed of several modules (for example):

* **Config Server** — centralised configuration service for all microservices.
* **Service Discovery / Registry** — for example using Eureka or similar.
* **API Gateway** — routes incoming requests from frontend to appropriate backend microservice.
* **User / Profile Service** — handles user data (if user login/profile is required).
* **Activity Service** — receives and stores user activity (activity type, duration, calories).
* **AI Recommendation Service** — processes activity data (via event queue) and returns a personalised fitness recommendation.
* **Frontend (React)** — user interface for inputting activity and viewing recommendations.
* **Messaging / Event Bus** — Kafka and/or RabbitMQ used for asynchronous event propagation (e.g., ActivityService → AIService).
* **Databases**:

    * PostgreSQL is used for structured relational data (e.g., user profiles, activity logs).
    * MongoDB is used for more flexible data, logging or AI output storage.

## Features

* User enters: activity type (such as “running”, “cycling”, “swimming”), duration (minutes), calories burnt.
* AI‑powered recommendation engine suggests next steps or fitness advice based on input.
* Event‑driven microservices architecture: clear separation of concerns, independent services.
* Demonstrates use of both relational (Postgres) and NoSQL (Mongo) storage.
* Demonstrates messaging with Kafka & RabbitMQ for asynchronous workflows.
* Containerised with Docker for easy local orchestration & deployment.
* Simple front‑end UI in React for quick interaction.

## How It Works

1. The user accesses the React frontend, inputs their activity details: activity type, duration, calories.
2. Frontend sends this data to the API Gateway, which forwards to the Activity Service.
3. Activity Service persists the data in PostgreSQL (or MongoDB) and publishes an event (via Kafka/RabbitMQ) indicating an activity record was created.
4. The AI Recommendation Service listens to the event topic/queue, consumes the message, applies its recommendation logic (could be rule‑based or ML).
5. The Recommendation Service produces a recommendation output, stores it (optionally) and sends a response back.
6. The frontend displays the recommendation to the user.
7. The system can accumulate activity history for analytics, trend detection or future model training.

## Development & Extending

You might consider adding or improving the following:

* More activity types, richer input (heart rate, distance, user weight/age) and finer tuned recommendation logic.
* Integrate a real ML model for fitness recommendations (instead of only simple rules) — e.g., using Python microservice, TensorFlow/PyTorch.
* Add user authentication and profiles (e.g., login, JWT tokens via Spring Security).
* Add analytics/dashboard to view past activity, trends, progress.
* Add health check endpoints, monitoring (Prometheus/Grafana), logging (ELK stack).
* Move from Docker Compose to Kubernetes for orchestration and scalability.
* Add CI/CD pipeline (GitHub Actions, Jenkins) for automated build, test, deploy.

## Deployment

* For local/dev: use `docker‑compose.yml`.
* For production: build Docker images for each service, push to container registry, then deploy on Kubernetes or managed container service.
* Use environment‑specific configurations (e.g., via Spring Cloud Config) for production vs dev.
* Secure the system: use SSL/TLS, secure message brokers, limit service access, use API authentication/authorization.
* Set up logging, monitoring, and observability to track system health as more users use the service.

## Contributing

Contributions are very welcome:

1. Fork the repository.
2. Create a new branch: `git checkout ‑b feature/YourFeature`.
3. Commit your changes: `git commit ‑m "Add some feature"`.
4. Push to your branch: `git push origin feature/YourFeature`.
5. Open a Pull Request describing your changes.
6. Make sure to include tests where applicable, update documentation, keep code style consistent.


## Contact

For questions or suggestions:

* GitHub Repository: [https://github.com/AadityaUoHyd/microservices‑fitness‑recommendation‑ai‑app](https://github.com/AadityaUoHyd/microservices-fitness-recommendation-ai-app)
* Author: Aaditya B Chatterjee (or appropriate name)
---