# FitTrack AI: AI-Powered Fitness Application

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen)
![React](https://img.shields.io/badge/React-18.x-blue)

FitTrack AI is a modern, full-stack fitness tracking application built on a distributed microservices architecture. It allows users to log their physical activities and receive personalized, AI-driven feedback and insights. The system is designed to be scalable, resilient, and maintainable, leveraging a powerful tech stack including Spring Boot, React, RabbitMQ, and the Google Gemini API.

## ✨ Features

* **Secure User Management:** Robust user authentication and authorization using Keycloak (OAuth2).
* **Activity Tracking:** Log various fitness activities, view history, and track progress.
* **AI-Powered Insights:** Asynchronous processing of activities to generate personalized workout tips, feedback, and analytics using Google's Gemini API.
* **Microservices Architecture:** A decoupled system where each service (User, Activity, AI) operates independently for high scalability and fault tolerance.
* **Centralized Management:** Utilizes Spring Cloud for API gateway routing, service discovery (Eureka), and centralized configuration.

## 🏛️ System Architecture

### Components

1.  **Frontend (React):** The user interface for web and mobile clients.
2.  **API Gateway (Spring Cloud Gateway):** The single entry point for all client requests. It handles routing, rate limiting, and security.
3.  **Auth Server (Keycloak):** Manages user identity, authentication, and secures the microservices using OAuth2/JWT.
4.  **Config Server (Spring Cloud Config):** Provides centralized configuration management for all microservices.
5.  **Service Discovery (Eureka Server):** Allows services to register themselves and discover others dynamically.
6.  **User Service:** Manages user data, profiles, and settings. (Uses PostgreSQL/MySQL).
7.  **Activity Service:** Handles the creation, retrieval, and management of user fitness activities. (Uses MongoDB).
8.  **AI Service:** Consumes activity data from a message queue, interacts with the Google Gemini API to generate insights, and stores the results.
9.  **Message Queue (RabbitMQ):** Decouples the Activity Service from the AI Service, enabling reliable, asynchronous processing of tasks.

## 🛠️ Tech Stack

| Category                  | Technology                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Backend Framework** | Spring Boot, Spring Cloud                                                                                     |
| **Frontend Framework** | React.js                                                                                                      |
| **Authentication** | Keycloak (OAuth 2.0 / OpenID Connect)                                                                         |
| **Databases** | PostgreSQL / MySQL (for relational data like Users), MongoDB (for document data like Activities)               |
| **Asynchronous Messaging**| RabbitMQ (AMQP)                                                                                               |
| **Service Communication** | REST APIs, Event-Driven (via RabbitMQ)                                                                        |
| **Service Infrastructure**| Spring Cloud Gateway, Eureka Server, Spring Cloud Config Server                                               |
| **AI Integration** | Google Gemini API                                                                                             |
| **Containerization** | Docker, Docker Compose                                                                                        |

## 🚀 Getting Started

Follow these instructions to get the project up and running on your local machine for development and testing purposes.

### Prerequisites

* Java JDK 17 or later
* Maven or Gradle
* Node.js and npm
* Docker and Docker Compose
* An IDE like IntelliJ IDEA or VS Code

### Installation & Setup

1.  **Clone the repository:**
    ```sh
    git clone [https://github.com/your-username/fittrack-ai.git](https://github.com/your-username/fittrack-ai.git)
    cd fittrack-ai
    ```

2.  **Configure Environment Variables:**
    Each microservice requires its own configuration. Create an `application.properties` or `application.yml` file for each service based on the provided `.example` files. Key variables to set include:
    * Database connection details (PostgreSQL/MySQL, MongoDB)
    * RabbitMQ server address and credentials
    * Keycloak server URL, realm, and client details
    * Google Gemini API Key

3.  **Build and Run with Docker Compose (Recommended):**
    The easiest way to run the entire stack is using Docker Compose.
    ```sh
    docker-compose up --build
    ```
    This command will build images for all microservices and run them as containers, including the required databases, RabbitMQ, and Keycloak instances.

4.  **Run Services Individually (Alternative):**
    If you prefer to run services manually:
    * Navigate to each microservice directory (e.g., `user-service/`).
    * Build the service: `mvn clean install`
    * Run the service: `java -jar target/user-service-0.0.1-SNAPSHOT.jar`
    * Repeat for all backend services.

5.  **Run the Frontend:**
    ```sh
    cd frontend/
    npm install
    npm start
    ```
    The React application will be available at `http://localhost:3000`. The API Gateway will be running on a different port (e.g., `http://localhost:8080`).

## 📜 API Reference

The API Gateway exposes the microservices at the following base paths:

* **User Service:** `http://localhost:8080/api/users`
* **Activity Service:** `http://localhost:8080/api/activities`

Please refer to the Swagger/OpenAPI documentation for detailed endpoint information, which can typically be found at `http://localhost:<service-port>/swagger-ui.html` for each service.

## 🤝 Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request
