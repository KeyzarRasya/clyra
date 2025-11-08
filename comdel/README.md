# Comdel Frontend (`comdel-app`)

This document provides a technical overview of the Comdel frontend application.

## 1. Overview

The Comdel frontend is a web application built with SvelteKit. It serves as the user interface for the Comdel service, allowing users to connect their YouTube accounts, manage monitored videos, and view analytics related to comment moderation.

-   **Framework**: [SvelteKit](https://kit.svelte.dev/)
-   **Language**: TypeScript
-   **Package Manager**: npm

## 2. Key Features

-   **Google OAuth Integration**: Securely log in using a Google account.
-   **Dashboard**: A central hub to display a list of monitored YouTube videos and key statistics.
-   **Video Content View**: A detailed page for each video, showing the latest comments and moderation actions.
-   **Subscription Management**: An interface for handling user subscriptions and payments.
-   **Responsive Design**: A clean and user-friendly interface that works across different devices.

## 3. Project Structure

The most important directories in this project are:

-   `src/routes`: Defines all the pages and API endpoints of the application. Each file or folder in this directory corresponds to a URL route.
    -   `/dashboard`: The main user dashboard.
    -   `/content/[slug]`: The detailed view for a specific video.
    -   `/login`: The login page.
    -   `/payment`: The payment processing page.
-   `src/components`: Contains reusable Svelte components that are used across different pages, such as `VideoCard.svelte`, `Comment.svelte`, and `SidebarButton.svelte`.
-   `src/lib`: Includes shared modules, utilities, and client-side libraries.
-   `static`: For static assets like images and fonts.

## 4. Getting Started

To run the frontend application in a local development environment, follow these steps.

### Prerequisites

-   [Node.js](https://nodejs.org/) (version 18 or higher)
-   npm (usually included with Node.js)

### Installation

1.  Navigate to the `comdel` directory:
    ```bash
    cd comdel
    ```

2.  Install the project dependencies:
    ```bash
    npm install
    ```

### Running the Development Server

Once the dependencies are installed, you can start the SvelteKit development server:

```bash
npm run dev
```

By default, the application will be available at `http://localhost:5173`. You can also start the server and automatically open it in a new browser tab:

```bash
npm run dev -- --open
```

## 5. Building for Production

To create a production-ready build of the application, run the following command:

```bash
npm run build
```

This will create an optimized version of the application in the `build` directory. You can preview the production build locally with `npm run preview`.

For deployment, you may need to install a SvelteKit [adapter](https://kit.svelte.dev/docs/adapters) depending on your target hosting environment.