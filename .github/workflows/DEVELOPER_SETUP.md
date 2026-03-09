# Developer Setup Guide

This guide provides instructions on how to set up and run the Dockerized Python To-Do List App locally.

## 1. Prerequisites Installation

### Docker Desktop
You must have Docker installed to run this containerized application.
1. Download Docker Desktop from: https://www.docker.com/products/docker-desktop/
2. Run the installer and follow the operating system prompts.
3. Once installed, launch Docker Desktop and ensure the engine is running (the Docker icon should be visible in your system tray).

### Git
You need Git to clone the repository.
1. Download Git from: https://git-scm.com/downloads
2. Run the installer and follow the default prompts.

## 2. Project Setup

Open your terminal or command prompt and follow these steps:

### Clone the Repository
```bash
git clone https://github.com/MAITREYY/Docker-expi.git
```

### Navigate into the Project Folder
```bash
cd Docker-expi
```

### Build and Run the Container
Use Docker Compose to build the image and start the container as a service:
```bash
docker-compose up --build
```
Note: The `--build` flag ensures that Docker rebuilds the image if any changes were made to the `Dockerfile` or `requirements.txt`.

### Access the Application
Once the terminal shows that the Flask server is running, open your web browser and navigate to:
http://localhost:5000

## 3. Managing the Application

### Stop the Application
To stop the running application, go to the terminal where `docker-compose up` is running and press:
`CTRL + C`

Alternatively, you can open a new terminal in the `Docker-expi` directory and run:
```bash
docker-compose down
```
This stops and removes the active containers.

### Rebuild the Application
If you add new Python packages to `requirements.txt` or modify the `Dockerfile`, you must rebuild the image:
```bash
docker-compose up --build
```
