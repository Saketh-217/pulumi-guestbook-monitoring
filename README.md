# Guestbook Monitoring with Pulumi, Prometheus and Grafana

This project is my implementation for the monitoring exercise. The goal was to take the existing Pulumi Kubernetes Guestbook example and add monitoring around it using Prometheus and Grafana.

I used Pulumi with TypeScript to deploy the application resources into a local Kubernetes cluster running on minikube. After the base application was running, I added the kube-prometheus-stack Helm chart through Pulumi so that Prometheus, Grafana, kube-state-metrics, node-exporter and Alertmanager are created as part of the same Pulumi deployment.

## What this project deploys

This Pulumi stack deploys:

- Redis leader pod and service
- Redis replica pod and service
- Frontend deployment and service
- Monitoring namespace
- Prometheus and Grafana using kube-prometheus-stack
- kube-state-metrics
- node-exporter
- Alertmanager
- Pulumi outputs for frontend and Grafana access information

## Small implementation note

While testing this locally on my Mac with minikube, I hit an `exec format error` with the older Guestbook container images. This was because the old images were not working properly with my local Apple Silicon / arm64 environment.

To keep the exercise moving and still show the Pulumi, Kubernetes and monitoring setup clearly, I changed the frontend image to an ARM-compatible nginx image. The Redis leader and replica were also moved to `redis:7-alpine`.

So the frontend here is used as a simple running web workload, and the monitoring part focuses on Kubernetes pod visibility, service health, resource metrics and Prometheus/Grafana setup. In a real production app, I would instrument the actual frontend code with a Prometheus client library or use an exporter/proxy to expose real HTTP request and error metrics.

## Prerequisites

Before running this, I used:

- Docker Desktop
- minikube
- kubectl
- Node.js and npm
- Pulumi CLI

I tested this locally using minikube.

## Start minikube

```bash
minikube start
```
