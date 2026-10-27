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

