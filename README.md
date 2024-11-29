# Deploying the Minimal 3-Tier Web Application using Kubernetes

This project defines Kubernetes manifests and Helm charts to deploy a 3-tier web application, including frontend, backend, database, and ingress routing. It uses Helm for PostgreSQL and Traefik installation and provides a structured approach to manage deployments, secrets, services, and ingress routes.

This section defines kubernetes manifests to deploy:

- The services defined in [K8s_3-tier_webapp](https://github.com/Frnn4268/K8s_3-tier_webapp)
- Postgresql (via [a helm chart](https://github.com/bitnami/charts/tree/main/bitnami/postgresql))
- Traefik ingress controller (and config to route traffic to the application)

## Layout

The following shows the layout of this directory:

```
├── api-golang
│   ├── Deployment.yaml
│   ├── IngressRoute.yaml
│   ├── Secret.yml
│   └── Service.yaml
├── api-node
│   ├── Deployment.yaml
│   ├── IngressRoute.yaml
│   ├── Secret.yaml
│   └── Service.yaml
├── client-react
│   ├── ConfigMap.yaml
│   ├── Deployment.yaml
│   ├── IngressRoute.yaml
│   └── Service.yaml
├── common
│   ├── Middleware.yaml
│   ├── Namespace.yaml
├── load-generator-python
│   ├── ConfigMap.yaml
│   └── Deployment.yaml
└── postgresql
    ├── Job.db-migrator.yaml
    └── Secret.db-password.yaml
```

## Breakdown

Helm is used to install:

1. `Postgresql`
2. `Traefik` (ingress controller)

Each service effectively gets broken down into:

1. `Deployment`: Contains the application
2. `Secret`: Contains database credentials
3. `Service`: Internal load balancer routing traffic to the deployment pods.
4. `IngressRoute`: Configures Ingress controller to route traffic to the proper service

The database migration is structured as a Kubernetes `Job`.

## Tasks

The top level `Taskfile` provides all necessary commands to deploy the application:

```
❯ task --list-all
task: Available tasks for this project:
* apply-all:
* api-golang:apply:                                     Apply kubernetes resource manifests for api-golang application
* api-node:apply:                                       Apply kubernetes resource manifests for api-node application
* client-react:apply:                                   Apply kubernetes resource manifests for client-react application
* common:apply-namespace:                               Apply Kubernetes Namespace
* common:apply-traefik-middleware:                      Deploy Traefik middleware
* common:deploy-traefik:                                Deploy Traefik using Helm
* load-generator-python:apply:                          Apply kubernetes resource manifests for load-generator-python application
* load-generator-python:create-image-pull-secret:       Create image pull secret to pull from private registry
* postgresql:apply-initial-db-migration-job:            Run init.sql script against the DB
* postgresql:install-postgres:                          Deploy PostgreSQL using Helm
```

## Problem Solved

This project provides a comprehensive solution for deploying a 3-tier web application using Kubernetes. It simplifies the deployment process by defining Kubernetes manifests for various services, including a React frontend, Node.js and Go backends, a PostgreSQL database, and a Traefik ingress controller.

## Summary

The project includes Kubernetes manifests and Helm charts to deploy a `3-tier web application`. It covers the deployment of frontend and backend services, database setup, and ingress routing.

### Key Content
- api-golang: Deployment, IngressRoute, Secret, Service
- api-node: Deployment, IngressRoute, Secret, Service
- client-react: ConfigMap, Deployment, IngressRoute, Service
- common: Middleware, Namespace
- load-generator-python: ConfigMap, Deployment
- postgresql: Job.db-migrator, Secret.db-password

If you want to see the "Kubernetes 3-Tier Web Application (K8s_3-tier_webapp)" feel free to use this link to view and adjust the repository contents to your needs: [K8s_3-tier_webapp](https://github.com/Frnn4268/K8s_3-tier_webapp)
