# Kaspr Helm

This Helm repository is designed to simplify the deployment and management of the `kaspr-operator` and its related custom resources, specifically the `KafkaMessageScheduler`, in your Kubernetes cluster. 

## Introduction

This repository comes with two charts:
- The `operator` chart is for deploying the kaspr kubernetes operator application.
- The `resources` chart is for deploying kaspr custom resources, specifically the KafkaMessageScheduler, in Kubernetes environments.

## Prerequisites

- Kubernetes cluster
- Helm 3.x

## Getting Started

1. **Clone the repository**:
   ```
   git clone https://github.com/totalwinelabs/kaspr-helm.git
   cd kaspr-helm
   ```

2. **Install the Kaspr operator**:

    The command below installs the Kaspr operator using the default values file included with the chart, which is sufficient for most deployments. However, if you wish to fine-tune the deployment according to your specific needs, you can provide your own values file.
   ```
   helm install kaspr-operator charts/operator -n kaspr-operator --create-namespace
   ```

3. **Install KafkaMessageScheduler resources**:

    To properly create the resources you want, you should provide a custom values file that overrides the default settings to meet your specific configuration needs. You can use the -f or --values flag to specify your own values file during the installation. For example, if you have a custom values file named my-kms-values.yaml, you can install the KafkaMessageScheduler resources like this:
   ```
   helm install kaspr-scheduler charts/resources -f my-kms-values.yaml
   ```

## Custom Resource Definitions (CRDs)

CRDs are included in the `/crds` directory of the operator chart and are installed automatically with the Helm chart. However, they need to be manually updated or removed when necessary.

- **Updating CRDs**:
  ```
  kubectl apply -f ./charts/operator/crds
  ```

- **Removing CRDs**:
  ```
  kubectl delete -f ./charts/operator/crds
  ```

## Configuration

The Helm chart supports configurations through values files:

- **`charts/operator/values.yaml`**: Configures the deployment of the Kaspr operator.
- **`charst/reseources/values.yaml`**: Configures the KafkaMessageScheduler resources.

Refer to these files for detailed configuration options. You should provide a custom values file that overrides the default settings when deploying kaspr custom resources to meet your specific needs.

## Operator Installation Modes

- **Cluster-wide**: Set `watchAnyNamespace` to `True` in operator's `values.yaml` for the operator to monitor resources across all namespaces.
- **Namespace-specific**: Define specific namespaces in `watchNamespaces` in `operator.values.yaml`. The operator's deployment namespace is always included.

## Uninstallation

To uninstall the Kaspr operator:

```
helm uninstall kaspr-operator -n kaspr-operator
```

Remember to manually remove the CRDs if necessary.

## Support

For issues or questions, please open an issue in the GitHub repository.

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.