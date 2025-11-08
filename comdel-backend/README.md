# Comdel Backend (`comdel-backend`)

This document provides a technical overview of the Comdel backend service.

## 1. Overview

The Comdel backend is the central service that powers the Comdel application. It is written in Go and is responsible for handling business logic, managing data, and communicating with external services like the YouTube API and the `comdel-model-api`.

-   **Language**: Go
-   **Web Framework**: [Fiber](https://gofiber.io/)
-   **Database**: PostgreSQL
-   **Database Driver**: [pgx](https://github.com/jackc/pgx)

## 2. Key Features

-   **RESTful API**: Exposes a comprehensive API for the frontend to consume.
-   **User Authentication**: Handles user sign-up and login via Google OAuth2.
-   **YouTube API Integration**: Fetches video and comment data from the YouTube Data API.
-   **Comment Moderation**: Orchestrates the comment analysis process by sending comment text to the `comdel-model-api`.
-   **Database Management**: Manages all data persistence using a PostgreSQL database.
-   **Subscription & Payments**: Integrates with the Midtrans payment gateway to manage user subscriptions.
-   **Background Jobs**: Includes a cron service for periodic tasks.

## 3. Project Structure

The project follows a standard Go project layout:

-   `cmd/main.go`: The main entry point of the application.
-   `internal/`: Contains all the core application logic, separated by concern.
    -   `config/`: For loading and managing application configuration (e.g., database credentials, API keys).
    -   `dto/`: Data Transfer Objects used for structuring API request and response bodies.
    -   `handlers/`: HTTP request handlers that parse requests and call the appropriate services.
    -   `services/`: Contains the core business logic of the application.
    -   `repository/`: Implements the database queries and data access logic.
    -   `model/`: Defines the data structures that map to database tables.
    -   `routes/`: Defines the API routes and links them to the handlers.
    -   `middleware/`: For authentication and other request middleware.
-   `pkg/`: For shared utility packages and helpers.
-   `go.mod` & `go.sum`: Manage the project's dependencies.

## 4. API Endpoints

The backend provides a variety of API endpoints to support the frontend application. The main routes are defined in `internal/routes/user_route.go`. High-level route groups include:

-   `/api/auth`: For user authentication (login, logout, callback).
-   `/api/videos`: For managing and retrieving video data.
-   `/api/comments`: For fetching and analyzing comments.
-   `/api/payment`: For handling payment notifications and subscription status.

For detailed information on each endpoint, refer to the source code in the `internal/handlers` and `internal/routes` directories.

## 5. Database

The backend uses a PostgreSQL database to store all application data, including:

-   Users
-   YouTube Videos
-   Comments
-   User Subscriptions
-   Payment Transactions

The database schema is defined by the structs in the `internal/model` directory, which are used by the `gorm` ORM.

## 6. Getting Started

The backend is designed to be run as a containerized service using Docker.

1.  **Prerequisites**:
    -   Docker and Docker Compose.
    -   A running PostgreSQL database.
    -   Environment variables for database connections, Google OAuth, and other external services.

2.  **Running the Service**:
    The service is typically started as part of the `docker-compose up` command from the project root. The `docker-compose.yaml` file defines the service configuration, environment variables, and networking.

3.  **Local Development**:
    To run the backend locally without Docker, you would need to:
    a.  Install Go (version 1.20 or higher).
    b.  Set up the required environment variables.
    c.  Run the application from the `comdel-backend` directory:
        ```bash
        go run cmd/main.go
        ```
