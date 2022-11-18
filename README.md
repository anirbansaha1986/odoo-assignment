# Avoin Systems Assignment

## Description

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

2. Export _KUBECONFIG_ variable pointing to the kubernetes configuration file

```
export KUBECONFIG=/path/to/kubeconfig
```

3. Install [Helm](https://helm.sh/docs/intro/install/) on your machine and run the following command to install the application.

```
helm install <namespace-to-deploy> .
```

Verify your
