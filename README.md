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

## Files and Structure
HelloWorldDocker/
│
├── src/
│ └── HelloWorld.java
│
├── Dockerfile
│
└── .github/
└── workflows/
└── docker.yml
