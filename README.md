# DevOps Exam Project

## Overview

This project is a simple Express.js application served behind an Nginx reverse proxy, both containerized with Docker. It demonstrates best practices for modern DevOps workflows, including containerization and reverse proxy configuration.

## Features

-  **Express.js API**: A Node.js backend application.
-  **Nginx Reverse Proxy**: Handles incoming HTTP requests and forwards them to the Express app.
-  **Dockerized**: Both the app and Nginx run in containers.

## Project Structure

```
├── app.js                # Express application
├── Dockerfile            # Dockerfile for Express app
├── nginx.conf            # Nginx configuration
├── package.json          # Node.js dependencies
├── package-lock.json     # Lock file
└── README.md             # Project documentation
```

## Prerequisites

-  [Docker](https://www.docker.com/get-started)
-  [Node.js & npm](https://nodejs.org/)

## Setup & Usage

### 1. Build the Express App Docker Image

```
docker build -t devops-exam-app .
```

### 2. Run the Express App Container

```
docker run -d --name express-app --network devops-net -p 3000:3000 devops-exam-app
```

### 3. Create a Docker Network (if not already created)

```
docker network create devops-net
```

### 4. Run the NGINX Container with Custom Config

```
docker run -d --name nginx-proxy --network devops-net -p 80:80 -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro nginx
```

### 5. Access the Application

-  Open your browser or use curl:
   ```
   curl http://localhost/
   ```
   You should see:
   ```
   Hello, DevOps!
   ```

## Cleaning Up

```
docker rm -f express-app nginx-proxy
```

## Customization

-  **Nginx Config**: Edit `nginx.conf` as needed.
-  **Express App**: Edit `app.js` as needed.

## License

MIT
