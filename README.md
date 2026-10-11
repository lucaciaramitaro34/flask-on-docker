## Flask on Docker

[![Development Build](https://github.com/lucaciaramitaro34/flask-on-docker/actions/workflows/build.yml/badge.svg?branch=main)](https://github.com/lucaciaramitaro34/flask-on-docker/actions/workflows/build.yml)

## Overview

This project is a containerized Flask web application built using Docker, PostgreSQL, Gunicorn, and Nginx. The application provides a simple REST endpoint and supports uploading and retrieving images through a web browser. Docker Compose orchestrates the services, allowing the application to run in separate development and production environments. In production, Gunicorn serves the Flask application while Nginx acts as a reverse proxy and serves static and uploaded media files.


## DEMO

![Flask Image Upload Demo](Flask-on-docker.gif)

The following demonstration shows the application running, uploading an image, and viewing the uploaded image in the browser.


## Build Instructions - Development

1. Clone the repository:
```
git clone https://github.com/lucaciaramitaro34/flask-on-docker.git

cd flask-on-docker
```
2. Build and start services:
```
docker compose up -d --build
```
3. Initialize database (first time only):
```
docker compose exec web python manage.py create_db
```
4. Test the application:

Open the following to upload an image:

http://localhost:8007/upload

To view your uploaded image, open the following:

http://localhost:8007/media/IMAGE_FILE_NAME

where you replace IMAGE_FILE_NAME with your uploaded image file name

## NOTE: 

If docker is running on a remote machine, you must establish an SSH port-forwarding tunnel to open these URLs locally.

5. Stop the application:
```
docker compose down -v
```

## Build Instructions - Production

1. If you plan on running the production version of this tutorial, you must create .env.prod and .env.prod.db environment variables using local credentials that are not committed to Git

Use the following commands to copy the example files, replacing the placeholders with local credentials.
```
cp .env.prod.example .env.prod

cp .env.prod.db.example .env.prod.db 
```

2. After this, build and start containers with:
```
docker compose -f docker-compose.prod.yml up -d --build

docker compose -f docker-compose.prod.yml exec web python manage.py create_db
```
3. Access the application using the same commands as above:

Open the following to upload an image:

http://localhost:8007/upload

To view your uploaded image, open the following:

http://localhost:8007/media/IMAGE_FILE_NAME

where you replace IMAGE_FILE_NAME with your uploaded image file name

4. Stop production services:
```
docker compose -f docker-compose.prod.yml down -v
```
## Acknowledgments

Based on the TestDriven.io Dockerizing Flask tutorial.


