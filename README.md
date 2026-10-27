

## Project Rationale

### Base Image and Multi-Stage Build

I used nginx:alpine as the final base image because it is lightweight and provides the web server needed to serve the application without including unnecessary development tools. The Dockerfile uses a multi-stage build where Node.js is used in the first stage to build the application, while the final stage only contains the files needed to run the completed application with Nginx. This keeps the final image smaller and separates the build environment from the runtime environment.

### Service Choices

The application uses two separate services: the web service and a Redis cache service. I kept Redis separate from the web container because each container has a different responsibility. The web container serves the application, while Redis provides the caching service. Using redis:7-alpine also means that I can use an existing Redis image instead of installing and managing Redis inside the web container.

Keeping the services separate makes the application easier to manage and follows the container approach of using separate services for separate responsibilities. Docker Compose connects the services and controls their startup order. The Redis health check ensures that the cache service is ready before the web service depends on it.

### Sources

Docker Documentation - Multi-stage builds:
https://docs.docker.com/build/building/multi-stage/

Docker Documentation - Control startup and shutdown order in Compose:
https://docs.docker.com/compose/how-tos/startup-order/

Docker Hub - Nginx Official Image:
https://hub.docker.com/_/nginx

Docker Hub - Redis Official Image:
https://hub.docker.com/_/redis
# Cloud Computing Project

This repository contains my Cloud Computing lab work using Docker, Docker Compose, Redis, Nginx, and AWS SAM.

## Run the Docker Application

From the root directory of the project, run:

docker compose up -d

To check that the containers are running:

docker compose ps

To test the web application:

curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8080

A successful response should return:

200

To stop and remove the containers:

docker compose down

## Run the AWS Lambda Function Locally

From the root directory, move into the local-fn directory:

cd local-fn

Run the Lambda function using AWS SAM:

sam local invoke -e events/event.json

A successful invocation should return a response containing:

"statusCode": 200
"message": "hello world"

## Project Verification

The Docker application and AWS Lambda function were tested locally. The repository was also cloned into a separate directory and tested successfully to confirm that the project can be reproduced from the GitHub repository.


## Project Rationale

### Base Image and Multi-Stage Build

I used nginx:alpine as the final base image because it is lightweight and suitable for serving the built web application. A multi-stage build is used so that Node.js is used to build the application, while only the final build files are copied into the Nginx image. This helps keep the final image smaller and avoids including unnecessary build dependencies.

### Service Choices

The application uses two separate services: the web service and Redis. The web service runs the application, while Redis is used as a separate cache service.

Keeping the services separate makes the application easier to manage and follows the containerization approach of having different services perform different responsibilities.

### Sources

Docker Documentation - Multi-stage builds:
https://docs.docker.com/build/building/multi-stage/

Docker Documentation - Control startup and shutdown order in Compose:
https://docs.docker.com/compose/how-tos/startup-order/

Docker Hub - Nginx Official Image:
https://hub.docker.com/_/nginx

Docker Hub - Redis Official Image:
https://hub.docker.com/_/redis

