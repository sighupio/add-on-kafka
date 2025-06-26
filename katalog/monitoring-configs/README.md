# Monitoring Configs

<!-- <SD-DOCS> -->

This package provides the monitoring configurations for the Strimzi Kafka Operator.

## Requirements

- Kubernetes >= `1.16.0`
- Kustomize >= `v3.5.4`
- [SIGHUP Monitoring][module-monitoring]

## Deployment

You can deploy the package with the following command:

```bash
kustomize build . | kubectl apply -f -
```

> NB: this package should be used if there is at least one Kafka cluster deployed with the operator. Otherwise, a lot of alerts
> will be triggered.

<!-- Links -->

[module-monitoring]: https://github.com/sighupio/module-monitoring

<!-- </SD-DOCS> -->
