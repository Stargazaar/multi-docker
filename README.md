# Multi-Container Application Setup
This section covers managing multi-container applications using Docker and deploying them to AWS Elastic Beanstalk. 

## Overview
Multi-container applications consist of discrete services such as:
- React Client
- Express API Server
- Worker Process
- Redis (In-memory storage)
- Postgres (Database)
- Nginx (Routing Server)

Each service runs in its own container and communicates over a network. Using Docker Compose simplifies defining, running, and linking these containers together locally. For production environments, Docker containers are deployed using AWS Elastic Beanstalk with a multi-container approach.

## Docker Compose Setup
- Define each service in a `docker-compose.yml` file.
- Specify service image, build context, ports, environment variables, and volumes.
- Docker Compose automatically creates an internal network allowing services to reference each other by service name.

## AWS Elastic Beanstalk Multi-Container Deployment
For production, deploy containers on AWS using a `Dockerrun.aws.json` file specifying:
- Container names and images (pre-built and pushed to Docker Hub).
- Hostnames for container-to-container communication.
- Essential flags indicating critical containers.
- Port mappings and links between containers.

The `essential` flag controls the container's importance; if an essential container crashes, all containers in the group shut down. Nginx is made essential because it coordinates routing for the app.

## Container Networking and Links
- Containers in Elastic Beanstalk link to each other by hostname.
- Docker Compose uses service names for inter-container communication.
- Nginx acts as a reverse proxy routing requests to the React client and API server.

## Additional Notes
- Building Docker images for each service separately improves modularity and deployability.
- Development workflows include separate Dockerfiles for development and production environments.
- Environment variables and secrets should be handled carefully in production deployments.

