# DefaultAttack

A demonstration project showcasing secure vs vulnerable CI/CD pipelines for Node.js applications with Docker containerization.

## Overview

This project demonstrates different approaches to CI/CD security, featuring both vulnerable and secure GitHub Actions workflows for:
- Docker image building and publishing
- NPM package creation and publishing
- Security scanning with tools like TruffleHog and Octoscan

## Project Structure

```
.
├── index.js                          # Simple Node.js application
├── package.json                      # NPM package configuration
├── Dockerfile                        # Docker container definition
├── README.md                         # This file
└── .github/workflows/
    ├── docker-safe.yml              # Secure Docker CI/CD workflow
    ├── docker-vulnerable.yml        # Vulnerable Docker CI/CD workflow
    ├── npm-safe.yml                 # Secure NPM CI/CD workflow
    └── npm-vulnerable.yml           # Vulnerable NPM CI/CD workflow
```

## Application

The core application is a minimal Node.js script that outputs "Hello, world!" to the console. The Dockerfile creates a Debian-based container that runs a simple echo command.

### Local Development

Run the application locally:
```bash
node index.js
```

### Docker

Build and run the Docker container:
```bash
# Build the image
docker build -t defaultattack .

# Run the container
docker run defaultattack
```

## CI/CD Workflows

This project includes four different GitHub Actions workflows to demonstrate security best practices:

### Docker Workflows

1. **docker-safe.yml** - Implements security scanning with TruffleHog before pushing images
2. **docker-vulnerable.yml** - Builds and pushes without security scanning

### NPM Workflows

1. **npm-safe.yml** - Two-stage workflow with TruffleHog scanning of package archives
2. **npm-vulnerable.yml** - Two-stage workflow without security scanning

### Security Features

The secure workflows include:
- **Octoscan** integration for vulnerability scanning
- **TruffleHog** for secret detection in Docker images and NPM packages
- **SARIF** uploads for GitHub Security tab integration
- Limited checkout depth and proper token handling

## Required Secrets

To use the CI/CD workflows, configure these GitHub repository secrets:
- `CI_CD_TOKEN` - GitHub token with appropriate permissions
- `DOCKER_USERNAME` - Docker Hub username
- `DOCKER_TOKEN` - Docker Hub access token
- `NPM_TOKEN` - NPM authentication token

## Purpose

This project serves as an educational tool to demonstrate:
- The importance of security scanning in CI/CD pipelines
- How to implement secret detection in containerized applications
- Best practices for artifact handling in multi-stage workflows
- The difference between secure and vulnerable deployment practices

## License

MIT
