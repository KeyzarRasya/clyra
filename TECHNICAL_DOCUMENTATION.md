# Technical Documentation

This document provides a technical overview of the Comdel project, including its architecture, components, and setup instructions.

## 1. High-Level Architecture

The Comdel project is a multi-component application designed to automatically delete promotional and gambling-related comments from YouTube videos. It follows a microservices-based architecture, consisting of three main services:

1.  **Frontend Application (`comdel-app`)**: A web-based user interface built with SvelteKit, allowing users to manage their monitored YouTube channels and view analytics.
2.  **Backend Service (`comdel-backend`)**: A Go-based application that handles the core business logic, including user authentication, communication with the YouTube API, comment processing, and database management.
3.  **Model API (`comdel-model-api`)**: A Python-based service that exposes a machine learning model for comment analysis and classification.

These services are designed to be containerized and managed via Docker Compose for ease of development and deployment.

## 2. Project Components

### 2.1. Frontend (`comdel-app`)

The frontend is a modern web application built with SvelteKit, providing a reactive and user-friendly interface.

-   **Framework**: SvelteKit
-   **Language**: TypeScript
-   **Styling**: CSS with some components using `.svelte` styling.
-   **Key Directories**:
    -   `src/routes`: Defines the application's pages and API routes. This includes user-facing pages like the dashboard (`/dashboard`), content details (`/content/[slug]`), and authentication (`/login`).
    -   `src/components`: Contains reusable Svelte components that make up the UI, such as `Comment.svelte`, `VideoCard.svelte`, and `Scheduler.svelte`.
    -   `src/lib`: For shared utilities and library initializations.
-   **Functionality**:
    -   User authentication via Google OAuth.
    -   A dashboard to display monitored videos and analytics.
    -   A detailed view for each video to inspect comments.
    -   Subscription and payment management.

### 2.2. Backend (`comdel-backend`)

The backend service is the core of the application, written in Go. It manages data, external API interactions, and the main business logic.

-   **Language**: Go
-   **Key Dependencies**:
    -   `fiber`: A web framework for building the API.
    -   `pgx`: For connecting to the PostgreSQL database.
    -   Google API libraries for YouTube data access.
-   **Directory Structure (`internal`)**:
    -   `config`: Handles application configuration, including database and OAuth credentials.
    -   `handlers`: Contains HTTP handlers for processing incoming API requests.
    -   `services`: Implements the business logic, coordinating between repositories and external services.
    -   `repository`: Manages data access and database queries.
    -   `model`: Defines the data structures for database tables.
    -   `routes`: Defines the API endpoints and connects them to the appropriate handlers.
-   **Functionality**:
    -   Handles Google OAuth2 for user authentication.
    -   Fetches video and comment data from the YouTube API.
    -   Interfaces with the `comdel-model-api` to classify comments.
    -   Stores user data, video information, and comments in a PostgreSQL database.
    -   Manages user subscriptions and payment processing through Midtrans.

### 2.3. Model API (`comdel-model-api`)

This service provides access to the machine learning model responsible for identifying unwanted comments.

-   **Language**: Python
-   **Framework**: A Python web framework (likely Flask or FastAPI, based on `main.py`).
-   **`main.py`**: This file contains the API server that loads the trained model and exposes an endpoint for inference. The backend sends comment text to this endpoint and receives a classification result.
-   **`requirements.txt`**: Lists the Python dependencies, which would include the web framework and machine learning libraries (e.g., TensorFlow, PyTorch, or scikit-learn).

## 3. Getting Started

To run the entire application stack, Docker is required.

1.  **Prerequisites**:
    -   Docker and Docker Compose must be installed.
    -   You may need to configure environment variables, such as API keys for Google and an endpoint for the model API.

2.  **Build and Run**:
    Use the following command from the project root to build and start all the services in detached mode:
    ```bash
    docker compose up -d --build
    ```

3.  **Verify**:
    Check the status of the running containers:
    ```bash
    docker ps
    ```

4.  **Shutdown**:
    To stop and remove the containers, run:
    ```bash
    docker compose down
    ```

## 4. API and Data

-   **Backend API**: The `comdel-backend` service exposes a RESTful API that the frontend consumes. The routes are defined in the `comdel-backend/internal/routes` directory.
-   **Database**: The application uses a PostgreSQL database to persist data. The database schema is implicitly defined by the `gorm` models in the `comdel-backend/internal/model` directory.

This documentation provides a high-level technical guide to the Comdel project. For more detailed information, refer to the source code within each component's directory.
