# Comdel Model API (`comdel-model-api`)

This document provides a technical overview of the Comdel Model API service.

## 1. Overview

The Comdel Model API is a Python-based service responsible for serving the machine learning model that classifies YouTube comments. The `comdel-backend` service communicates with this API to determine whether a comment should be flagged as promotional or inappropriate.

-   **Language**: Python
-   **Web Framework**: Likely FastAPI or Flask (inferred from the use of `main.py` for serving).

## 2. Key Features

-   **Machine Learning Model Serving**: Loads a pre-trained machine learning model for text classification.
-   **RESTful API Endpoint**: Exposes a simple API endpoint that accepts comment text and returns a classification result.
-   **Containerized**: Designed to be run as a lightweight, standalone Docker container.

## 3. Project Structure

-   `main.py`: The main entry point of the application. This script loads the machine learning model and starts a web server to expose the prediction endpoint.
-   `requirements.txt`: A list of all the Python dependencies required to run the service. This includes a web framework (like `fastapi` or `flask`) and machine learning libraries (like `tensorflow`, `torch`, or `scikit-learn`).
-   `Dockerfile`: Contains the instructions to build a Docker image for the service, ensuring that all dependencies are installed and the application is started correctly.

## 4. API Endpoint

The primary purpose of this service is to provide a prediction endpoint. The `comdel-backend` sends a POST request to this endpoint with a JSON payload containing the comment text.

**Example Request**:

```json
{
  "text": "Check out my awesome new website for free stuff! my-site.com"
}
```

**Example Response**:

The API returns a classification result, which might look something like this:

```json
{
  "classification": "promotion",
  "confidence": 0.95
}
```

The exact structure of the request and response is defined in `main.py`.

## 5. Getting Started

The Model API is designed to be run as a containerized service using Docker.

1.  **Prerequisites**:
    -   Docker and Docker Compose.
    -   A pre-trained machine learning model file (this is likely downloaded or included in the build process).

2.  **Running the Service**:
    The service is started as part of the `docker-compose up` command from the project root. The `docker-compose.yaml` file defines the service configuration, including the build context and any necessary environment variables.

3.  **Local Development**:
    To run the service locally without Docker, you would need to:
    a.  Install Python (version 3.8 or higher).
    b.  Install the required dependencies from `requirements.txt`:
        ```bash
        pip install -r requirements.txt
        ```
    c.  Run the application:
        ```bash
        python main.py
        ```
