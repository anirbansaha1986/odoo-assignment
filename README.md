<div align="center">

# Helm Chart - Avoin Systems Assignment

[![AKS Helm chart deployment](https://github.com/sla686/odoo-assignment/actions/workflows/azure-kubernetes-service-helm.yaml/badge.svg)](https://github.com/sla686/odoo-assignment/actions/workflows/azure-kubernetes-service-helm.yaml)

[Description](#description) •
[Prerequisites](#prerequisites) •
[Installation](#installation) •
[Removal](#removal)

</div>

## Description

- This is a [Helm](https://helm.sh/) chart repository for deploying an [odoo](https://www.odoo.com/) application to a Kubernetes cluster.
- The repository's CI/CD pipeline is configured to deploy application's Helm chart to Azure Kubernetes Service ([AKS](https://learn.microsoft.com/en-us/azure/aks/)).

## Prerequisites

Kubernetes cluster must be configured with:

1. An ingress controller with ingressClassName _ngnix_.
2. A CSI provisioner for volumes.

## Installation

1. Clone the repository:

```
git clone https://github.com/sla686/odoo-assignment.git odoo-app
cd odoo-app
```

2. Install [kubectl](https://kubernetes.io/docs/tasks/tools/) command-line tool.

3. Export _KUBECONFIG_ variable pointing to the kubernetes configuration file:

```
export KUBECONFIG=/path/to/kubeconfig
```

4. Create a new namespace for your application if you need:

```
kubectl create namespace <namespace>
```

5. Install [Helm](https://helm.sh/docs/intro/install/) package manager.

6. To install the application, you have to provide connection credentials to connect to the application database. You can specify them in your values.yaml file:

```
odooDB:
  credentials:
    user: <user>
    password: <password>
    database: <database>
```

and then run the following command:

```
helm install --namespace <application-namespace> <application-name> .
```

You can also provide them in your command directly:

```
helm install --namespace <application-namespace> \
  --set odooDB.credentials.user=<user> \
  --set odooDB.credentials.password=<password> \
  --set odooDB.credentials.database=<database> \
  <application-name> .
```

7. Check details about your release:

```
helm status -n <application-namespace> <application-name>
```

## Removal

You can uninstall the application with the following command:

```
helm uninstall -n <application-namespace> <application-name>
```

Don't forget to remove the namespace from your Kubernetes cluster if you don't need it anymore:

```
kubectl delete namespace <namespace>
```
