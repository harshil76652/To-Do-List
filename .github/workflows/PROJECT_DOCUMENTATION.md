# Project Documentation: Dockerized Python To-Do List App

## Introduction
The Dockerized Python To-Do List App is a lightweight web application designed to manage daily tasks. The project uses a Python-based backend framework (Flask) and a local SQLite database, packaged within a Docker container to ensure consistent deployment across different environments.

## System Architecture
The application follows a Client-Server architecture encapsulated within a single Docker container:
1.  **Client:** The web browser renders the HTML/CSS and sends HTTP requests (GET, POST) to the server.
2.  **Server:** The Flask application receives requests, processes logic, interacts with the local database, and returns rendered HTML templates via the Jinja2 engine.
3.  **Database:** A localized `database.db` file managed by SQLite3 provides persistent data storage.

## Technology Stack
*   **Language:** Python 3.11
*   **Backend Framework:** Flask
*   **Frontend:** HTML5, CSS3, Jinja2 Templating
*   **Database:** SQLite3
*   **Containerization:** Docker & Docker Compose

## Why Use Docker for this Project?
Traditional software development often encounters the "it works on my machine" problem, where an application functions correctly on a developer's computer but fails elsewhere due to differences in operating systems, library versions, or environment configurations.

Docker solves this by packaging the application and all its dependencies into a standardized unit called a container. 

Specific benefits for this project include:
*   **Environment Consistency:** The application runs in the exact same Python 3.11 environment on Windows, macOS, or Linux.
*   **No Local Dependencies:** A developer testing this codebase does not need to install Python, Flask, or SQLite on their host machine. They only need Docker.
*   **Isolated Database:** The SQLite database is created within the container context, keeping the host machine's file system clean.

## Why *Not* Use Docker (Trade-offs)?
While Docker provides excellent consistency, it introduces certain trade-offs, especially for a project of this small scale:
*   **Overhead & Resource Usage:** Running a basic locally-hosted Flask app directly via Python consumes minimal RAM. Running it inside a Docker container requires the Docker daemon and a virtualized Linux kernel (on Windows/Mac), which consumes significantly more memory and CPU for a simple task.
*   **Added Complexity:** For a beginner, learning to write a `Dockerfile` and `docker-compose.yml`, managing port forwarding, and dealing with Docker networking is a much steeper learning curve than simply typing `pip install flask` and running a script.
*   **Slow Development Loop:** Without setting up volume mapping correctly, every small change to the Python code would theoretically require rebuilding the entire container image, slowing down the development process compared to running Flask natively in debug mode. 
*   **Database Persistence Issues:** Because containers are ephemeral (temporary), if the database file is inside the container without a mounted volume, all tasks added to the To-Do list will be permanently wiped out the moment the container restarts or shuts down.

## Docker Implementation Details
*   **Dockerfile:** Defines the base operating system (Python 3.11 slim), installs required dependencies from `requirements.txt`, copies the source code, and sets the startup command.
*   **Docker Compose:** Orchestrates the container. It maps the host machine's port 5000 to the container's port 5000, allowing local browser access, and manages volume binding for local development.

## Project Workflow
1.  **Initialization:** Upon starting `app.py`, the system verifies the existence of the SQLite database and the `tasks` table, creating them if necessary.
2.  **Read:** A `GET` request to the root URL (`/`) fetches all tasks and renders them on `index.html`.
3.  **Create:** Submitting the form initiates a `POST` request to `/add`, inserting a new record into the database.
4.  **Update:** Clicking the complete button sends a request to `/complete/<id>`, toggling the boolean status.
5.  **Delete:** Clicking the delete button sends a request to `/delete/<id>`, removing the specific record.
