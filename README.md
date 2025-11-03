# Automate Docker Deployment with GitHub Actions (HelloWorld Java App)

## Overview
This project demonstrates how to automate the build and deployment of a simple Java application to Docker Hub using **GitHub Actions**. The app prints a personalized message from Alex Dayberry inside a Docker container.

## Project Description
The workflow automatically builds a Docker image from a Java source file (`HelloWorld.java`) and pushes it to Docker Hub whenever a commit is pushed to the `master` branch.

## Technologies Used
- **Java 23 (OpenJDK)**
- **Docker**
- **GitHub Actions**
- **Ubuntu Runner (CI/CD Environment)**
 
## Dockerfile
```dockerfile
FROM openjdk:23
WORKDIR /app
COPY src/ /app/
RUN javac *.java
CMD ["java", "HelloWorld"]
```
GitHub Actions Workflow

The workflow file .github/workflows/docker.yml automates the process:

Logs in to Docker Hub using stored secrets (DOCKER_USERNAME, DOCKER_PASSWORD)

Builds the Docker image tagged with the GitHub run number

name: Build and Push to Docker Hub

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Log in to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Build Docker Image
        run: docker build -t ${{ secrets.DOCKER_USERNAME }}/is147:${{ github.run_number }} .

      - name: Push Docker Image
        run: docker push ${{ secrets.DOCKER_USERNAME }}/is147:${{ github.run_number }}
How to Run the App

After the workflow completes:

Pull your image from Docker Hub:
```
docker pull your-dockerhub-username/is147:<tag>
```

Run the image:
```
docker run your-dockerhub-username/is147:<tag>
```

Output:
```
Hello, Docker and Java! - from Alex Dayberry
```
Continuous Integration Benefits

Automated Builds: No manual Docker build commands required.

Consistent Deployments: Ensures every push results in a fresh, versioned image.

Traceability: Each build uses the github.run_number tag for version history.
