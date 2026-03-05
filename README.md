# Flask on Docker


## Overview

This repository demonstrates how to deploy a production-ready Flask web application using Docker and container orchestration. The project includes a Flask backend, a PostgreSQL database, and an Nginx reverse proxy configured through Docker Compose. Users can upload images through the web interface, which are stored in a persistent media volume and served efficiently by Nginx. The project illustrates best practices for containerized web services, including separation of development and production environments, persistent storage with Docker volumes, and secure handling of environment variables.

## Demo

Below is an example of the application workflow:

1. Run the containerized web service
2. Upload an image through the `/upload` endpoint
3. Access the uploaded file through `/media/<filename>`

![Demo](demo.gif)


---

## Architecture

The application uses a **three-container architecture**:

* **Flask (Gunicorn)** – handles application logic and API endpoints
* **PostgreSQL** – persistent relational database
* **Nginx** – reverse proxy that serves static and media files

Docker volumes are used to persist:

* database data
* static files
* uploaded media files

---

## Build Instructions

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/flask-on-docker.git
cd flask-on-docker
```

---

### 2. Start the development environment

```bash
docker-compose up --build
```

This starts:

* Flask development server
* PostgreSQL database
* Nginx reverse proxy

The application will be available at:

```
http://localhost:1337
```

---

### 3. Run the production environment

```bash
docker-compose down -v
docker-compose -f docker-compose.prod.yml up -d --build
```

---

### 4. Initialize the database

```bash
docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```

---

### 5. Upload and view images

Upload an image through:

```
http://localhost:1337/upload
```

View uploaded files through:

```
http://localhost:1337/media/<image_filename>
```

Example:

```
http://localhost:1337/media/example.png
```

---

## Security

Production credentials are stored in environment files and **excluded from version control** using `.gitignore`. This prevents accidental exposure of sensitive information such as database credentials.

---

## Technologies Used

* Python / Flask
* Docker & Docker Compose
* PostgreSQL
* Nginx
* Gunicorn

---

## Continuous Integration

A GitHub Actions workflow automatically builds the project to ensure the development environment starts successfully.

This ensures that all commits maintain a working containerized build.

