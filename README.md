# Integration of CICD with Jenkins

This project demonstrates the implementation of a CI/CD pipeline using GitHub, Docker, and Git Workflow. The pipeline builds and deploys a website based on the branch where changes are committed.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Git Workflow](#git-workflow)
- [CI/CD Pipeline Workflow](#cicd-pipeline-workflow)
- [Docker Configuration](#docker-configuration)
- [Steps to Implement](#steps-to-implement)

## Prerequisites
- GitHub repository with product code (link: [GitHub Repo](https://github.com/Bapugouda-B/CICD-Jenkins))
- Docker installed
- Git installed
- Jenkins 
- Basic understanding of Git Workflow

## Git Workflow
- **Develop Branch**: The default branch for development.
- **Master Branch**: The main branch for production releases.
- Commits made to the `develop` branch will trigger the build process only.
- Commits made to the `master` branch will trigger the build and publish the website on port 82.

## CI/CD Pipeline Workflow
1. **Code Push**: Whenever code is pushed to the `master` or `develop` branch:
   - **Develop Branch**: Triggers a build without publishing.
   - **Master Branch**: Triggers a build and publishes the website.
   
2. **Docker Setup**: The project is built and deployed inside a Docker container using an Ubuntu image with Apache installed.
   
3. **Triggering the Pipeline**: The CI/CD tool monitors the branches and automatically triggers the pipeline based on the branch.

## Docker Configuration
- The Docker container is configured to install Apache, build the website, and publish the content to `/var/www/html`.
  
**Dockerfile**:
```dockerfile
# Use Ubuntu as the base image
FROM ubuntu:latest

# Install Apache
RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean

# Copy website code to Apache's default location
COPY . /var/www/html/

# Expose port 82 for the website
EXPOSE 82

# Start Apache
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
