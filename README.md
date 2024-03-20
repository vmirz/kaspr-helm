# kaspr-operator Helm Chart

This Helm chart is designed to simplify the deployment and management of the `kaspr-operator` and its associated resources, specifically the `KafkaMessageScheduler`, in your Kubernetes cluster. 

## Introduction

`kaspr-helm` is a Helm chart for deploying the Kaspr operator and its associated resources, including the KafkaMessageScheduler, in Kubernetes environments.

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
   ```
   helm install kaspr-operator ./kaspr-helm --values operator.values.yaml -n kaspr-operator --create-namespace
   ```

3. **Install KafkaMessageScheduler resources**:
   ```
   helm install kaspr-schedulers ./kaspr-helm --values kms.values.yaml
   ```

## Custom Resource Definitions (CRDs)

CRDs are included in the `/crd` directory and are installed automatically with the Helm chart. However, they need to be manually updated or removed when necessary.

- **Updating CRDs**:
  ```
  kubectl apply -f ./crd/<crd-file>.yaml
  ```

- **Removing CRDs**:
  ```
  kubectl delete -f ./crd/<crd-file>.yaml
  ```

## Configuration

The Helm chart supports various configurations through values files:

- **`operator.values.yaml`**: Configures the deployment of the Kaspr operator.
- **`kms.values.yaml`**: Configures the KafkaMessageScheduler resources.

Refer to these files for detailed configuration options.

## Operator Installation Modes

- **Cluster-wide**: Set `watchAnyNamespace` to `True` in `operator.values.yaml` for the operator to monitor resources across all namespaces.
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