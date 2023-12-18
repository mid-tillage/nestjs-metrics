# nestjs-metrics

## Table of Contents
- [Description](#description)
- [Installation](#installation)
- [Running the App](#running-the-app)
- [Test](#test)
- [Docker](#docker)
  - [Image Resource Usage Metrics](#image-resource-usage-metrics)
- [Kubernetes](#kubernetes)
  - [Pod Resource Usage Metrics](#pod-resource-usage-metrics)

## Description

Prometheus and Grafana example using [Nest](https://github.com/nestjs/nest) framework, Prometheus and Grafana.

## Installation

```bash
$ npm install
```

## Running the app
The following commands allow you to run the application

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Docker

```bash
# Build Docker image
docker build -t nestjs-metrics -f Dockerfile .

# Run Docker container (with example port mappings and environment variables)
docker run -p 3000:3000 -e NODE_ENV=production nestjs-metrics
```

### Image resource usage metrics

The table below shows resource usage metrics for the `store-admin-ws` Docker container.

| REPOSITORY        | TAG    | IMAGE ID      | CREATED      | SIZE  |
|-------------------|--------|---------------|--------------|-------|
| nestjs-metrics    | latest | 912acc385b94  | 2 hours ago  | 162MB |


## Kubernetes

```bash
# Start Minikube to create a local Kubernetes cluster
minikube start

# Configure the shell to use Minikube's Docker daemon
& minikube -p minikube docker-env --shell powershell | Invoke-Expression

# Build Docker image with a specific tag and Dockerfile
docker build -t store-admin-ws -f Dockerfile .

# Apply Kubernetes configuration with helm to create deployments
cd kubernetes/nestjs-metrics
helm dependency update
helm install nestjs-metrics .

# Port-forward to access the Kubernetes pod locally
kubectl port-forward nestjs-metrics-66759d774d-wbfk7 3000:3000
kubectl port-forward svc/nestjs-metrics-grafana 8080:80
```

### Pod resource usage metrics

The table below shows resource usage metrics for the `nestjs-metrics` related pods.

```bash
minikube addons enable metrics-server
kubectl top pods
```

**Note:** If you just enabled the metrics-server addon, remember to wait a couple of seconds before running the `kubectl top pods` command.

| NAME                                                     | CPU(cores) | MEMORY(bytes) |
|----------------------------------------------------------|------------|---------------|
| nestjs-metrics-66759d774d-wbfk7                          | 6m         | 31Mi          |
| nestjs-metrics-grafana-6568847dfc-7kwjs                  | 2m         | 168Mi         |
| nestjs-metrics-kube-state-metrics-5894cc84bf-r8f8c       | 1m         | 30Mi          |
| nestjs-metrics-prometheus-node-exporter-jk58r            | 1m         | 18Mi          |
| nestjs-metrics-prometheus-pushgateway-56b44d5b8d-qlfg5   | 1m         | 17Mi          |
| nestjs-metrics-prometheus-server-66d9d8f87f-sdcg5        | 4m         | 176Mi         |

![image](https://github.com/sys-internals/nestjs-metrics/assets/142703856/73f1e168-2691-43f4-a61b-d8c48e715624)

![image](https://github.com/sys-internals/nestjs-metrics/assets/142703856/ffecf08f-094c-434f-b89b-4f4534c57671)



