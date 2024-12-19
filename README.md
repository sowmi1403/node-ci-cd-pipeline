# Node.js CI/CD Pipeline with Docker and Kubernetes

This project demonstrates a CI/CD pipeline for a Node.js application. It includes automated testing, Docker image building, and deployment to a Kubernetes cluster with notification integration for deployment status.

## Table of Contents
1. [Overview](#overview)
2. [Setup](#setup)
   - [Prerequisites](#prerequisites)
   - [Local Setup](#local-setup)
3. [CI/CD Pipeline](#ci-cd-pipeline)
   - [GitHub Actions Workflow](#github-actions-workflow)
4. [Dockerization](#dockerization)
5. [Kubernetes Deployment](#kubernetes-deployment)
6. [Notifications](#notifications)
7. [Testing](#testing)
8. [Approach and Thought Process](#approach-and-thought-process)
9. [Contributing](#contributing)
10. [License](#license)

## Prerequisites

- **Node.js** (v16 or above)
- **Git**
- **Docker Desktop**
- **Kubernetes CLI (kubectl)**
- **Minikube** or a Kubernetes cluster
- **GitHub account** for repository management

## Setup

### Local Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd node-ci-cd
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Run the application locally:**
   ```bash
   npm start
   ```
   The application should be running at `http://localhost:3000`.

## CI/CD Pipeline

This project uses **GitHub Actions** for the CI/CD pipeline. The workflow performs the following tasks automatically:
- Runs tests on pull requests to the main branch.
- Builds a Docker image from the code.
- Deploys the Docker image to a Kubernetes cluster.

### GitHub Actions Workflow

The workflow file is located in `.github/workflows/ci.yml` and performs these steps:
1. **Checkout code** from the repository.
2. **Set up Node.js** environment.
3. **Run tests** using `npm test`.
4. **Build Docker image** and push it to Docker Hub.
5. **Deploy to Kubernetes** using `kubectl`.

To trigger the workflow, create a pull request or push to the `main` branch.

## Dockerization

To build and run the Docker container:

1. **Build the image locally:**
   ```bash
   docker build -t node-app .
   ```

2. **Run the container:**
   ```bash
   docker run -p 3000:3000 node-app
   ```

3. **Push the image to Docker Hub:**
   ```bash
   docker tag node-app <your-dockerhub-username>/node-app:latest
   docker push <your-dockerhub-username>/node-app:latest
   ```

## Kubernetes Deployment

To deploy the application to Kubernetes:

1. **Start your Kubernetes cluster using Minikube:**
   ```bash
   minikube start
   ```

2. **Apply the deployment and service files:**
   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

3. **Access the application:**
   Use `minikube service node-app-service` to get the URL for the deployed application.

## Notifications

Notifications for deployment success or failure can be configured using Slack or email integrations within GitHub Actions. This project integrates with Slack to send messages about deployment status.

**Steps to set up Slack notifications:**
- Create an incoming webhook in your Slack workspace.
- Add the webhook URL as a secret (`SLACK_WEBHOOK_URL`) in the GitHub repository settings.
- Update the workflow file to include Slack notification steps.

## Testing

This project uses **Jest** for testing. Tests are automatically run in the CI/CD pipeline on every pull request.

To run tests locally:
```bash
npm test
```

## Approach and Thought Process

The approach taken to develop this project involved:
- **Setting up a simple Node.js application** with a basic Express server.
- **Dockerizing the application** for containerized deployment.
- **Creating a CI/CD pipeline** using GitHub Actions to automate testing, building, and deployment.
- **Deploying the application to Kubernetes** for scalability and reliability.


## Repository Link

You can find the full code [here](https://github.com/sowmi1403/node-ci-cd).
