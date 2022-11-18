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

Kubernetes cluster must be at least version **1.23.x** or higher, and be configured with:

1. An ingress controller with ingressClassName _ngnix_.
2. A CSI provisioner for volumes.

The following tools must be installed on your machine:

1. [kubectl](https://kubernetes.io/docs/tasks/tools/) command-line tool.
2. [Helm](https://helm.sh/docs/intro/install/) package manager.

## Installation

1. Clone the repository:

```
git clone https://github.com/sla686/odoo-assignment.git odoo-app
cd odoo-app
```

2. Export _KUBECONFIG_ variable pointing to the kubernetes configuration file:

```
export KUBECONFIG=/path/to/kubeconfig
```

3. Create a new namespace for your application if you need:

```
kubectl create namespace <application-namespace>
```

4. To install the application, you have to provide connection credentials so that the application can connect to the database. You can specify them in your values.yaml file:

```
odooDB:
  credentials:
    user: <user>
    password: <password>
    database: <database>
```

After that, run the following command to install the application:

```
helm install --namespace <application-namespace> <application-name> .
```

You can also provide the connection credentials directly in your command:

```
helm install --namespace <application-namespace> \
  --set odooDB.credentials.user=<user> \
  --set odooDB.credentials.password=<password> \
  --set odooDB.credentials.database=<database> \
  <application-name> .
```

5. Check details about your release:

```
helm status -n <application-namespace> <application-name>
```

The application will be hosted on the host which is specified on the ingress.
Get the hostname of your application:

```
 kubectl get ingress -n <application-namespace> -o=jsonpath='{.items[0].spec.rules[0].host}'
```

Then use the output as a link and navigate to it in your browser.

## Removal

You can uninstall the application with the following command:

```
helm uninstall -n <application-namespace> <application-name>
```

Don't forget to remove the namespace from your Kubernetes cluster if you don't need it anymore:

```
kubectl delete namespace <application-namespace>
```
