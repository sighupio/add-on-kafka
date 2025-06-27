<h1 align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/sighupio/distribution/refs/heads/main/docs/assets/white-logo.png">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/sighupio/distribution/refs/heads/main/docs/assets/black-logo.png">
  <img alt="Shows a black logo in light color mode and a white one in dark color mode." src="https://raw.githubusercontent.com/sighupio/distribution/refs/heads/main/docs/assets/white-logo.png">
</picture><br/>
  Kafka Add-On Module
</h1>

![Release](https://img.shields.io/badge/Latest%20Release-v0.3.0-blue)
![License](https://img.shields.io/github/license/sighupio/add-on-kafka?label=License)
![Slack](https://img.shields.io/badge/slack-@kubernetes/fury-yellow.svg?logo=slack&label=Slack)

<!-- <SD-DOCS> -->

**Kafka Add-On** provides the Kafka add-on for [SIGHUP Distribution (SD)][kfd-repo].

If you are new to SD please refer to the [official documentation][sd-docs] on how to get started with SD.

## Overview

**Kafka Add-On** uses the [Strimzi operator][strimzi-page] to install and manage Kafka clusters in a Kubernetes environment.

All the components are deployed in the `kafka-operator` namespace in the cluster.

## Packages

The following packages are included in the SIGHUP Distribution Kafka katalog:

| Package                                                      | Version   | Description                                                                                                                                          |
|--------------------------------------------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| [strimzi-cluster-operator](katalog/strimzi-cluster-operator) | `v0.45.0` | Strimzi provides a way to run an Apache Kafka® cluster on Kubernetes in various deployment configurations, deployed in cluster-wide configuration.   |
| [monitoring-configs](katalog/monitoring-configs)             | `v0.3.0`  | Monitoring configurations for Strimzi Kafka Operator                                                                                                 |

Click on each package to see its full documentation.

## Compatibility

| Kubernetes Version |   Compatibility    | Notes                                               |
|--------------------|:------------------:|-----------------------------------------------------|
| `1.30.x`           | :white_check_mark: | No known issues                                     |
| `1.31.x`           | :white_check_mark: | No known issues                                     |
| `1.32.x`           | :white_check_mark: | No known issues                                     |

Check the [compatibility matrix][compatibility-matrix] for additional information about previous releases of the modules.

The module is still in version `0.X.X` but can be used in production, we are strictly following the possible breaking
changes that can be introduced by the Strimzi operator.

## Usage

### Prerequisites

| Tool                        | Version   | Description                                                                                                                                                    |
|-----------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [furyctl][furyctl-repo]     | `>=0.6.0` | The recommended tool to download and manage SD modules and their packages. To learn more about `furyctl` read the [official documentation][furyctl-repo].     |
| [kustomize][kustomize-repo] | `>=5.0.0` | Packages are customized using `kustomize`. To learn how to create your customization layer with `kustomize`, please refer to the [repository][kustomize-repo]. |

### Deployment

1. List the packages you want to deploy and their version in a `Furyfile.yml`

```yaml
bases:
  - name: kafka/strimzi-cluster-operator
    version: "v0.3.0"
  - name: kafka/monitoring-configs
    version: "v0.3.0"
```

> See `furyctl` [documentation][furyctl-repo] for additional details about `Furyfile.yml` format.

2. Execute `furyctl vendor -H` to download the packages

3. Inspect the download packages under `./vendor/katalog/kafka`.

4. Define a `kustomization.yaml` that includes the `./vendor/katalog/kafka` directory as resource.

```yaml
resources:
- ./vendor/katalog/kafka/strimzi-cluster-operator
- ./vendor/katalog/kafka/monitoring-configs
```

5. To deploy the packages to your cluster, execute:

```bash
kustomize build . | kubectl apply -f -
```

## Examples

### Deploying a Kafka cluster

Check the example in the example folder [kafka-standard](./examples/kafka-standard) to have an overview on how to deploy
a complete Kafka Cluster using the operator.

<!-- Links -->

[strimzi-page]: https://strimzi.io
[kfd-repo]: https://github.com/sighupio/distribution
[furyctl-repo]: https://github.com/sighupio/furyctl
[kustomize-repo]: https://github.com/kubernetes-sigs/kustomize
[sd-docs]: https://docs.sighup.io/docs/distribution/
[compatibility-matrix]: https://github.com/sighupio/add-on-kafka/blob/main/docs/COMPATIBILITY_MATRIX.md

<!-- </SD-DOCS> -->

<!-- <FOOTER> -->

## Contributing

Before contributing, please read first the [Contributing Guidelines](docs/CONTRIBUTING.md).

### Reporting Issues

In case you experience any problem with the module, please [open a new issue](https://github.com/sighupio/add-on-kafka/issues/new/choose).

## License

This module is open-source and it's released under the following [LICENSE](LICENSE)

<!-- </FOOTER> -->
