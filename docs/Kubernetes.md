# Description

Optionally, you can develop locally on Kubernetes which is how CHEFS is deployed in production.

# Prerequisites

## Kubernetes

You'll need to install Kubernetes on your machine, in this tutorial, we'll be using `minikube`. You can follow this [install guide](https://minikube.sigs.k8s.io/docs/start/) for your operating system.

### MacOS

First install Docker as your driver, and have Docker running.

`brew install minikube`

`minikube start`

## Terraform

Follow the [install guide](https://developer.hashicorp.com/terraform/downloads) for your operating system to install Terraform.

# Setup

Initialize Terraform:

```bash
terraform init
```

Apply the Terraform file to deploy it:

```bash
terraform apply
```

Tunnel

```bash
minikube tunnel
```
