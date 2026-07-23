# Ingress Nginx Kubernetes system service for Wodby

Ingress Nginx supplies ingress routing for Wodby Kubernetes clusters that use
the Nginx ingress controller.

This repository defines the Wodby service manifests and operational
configuration for Ingress Nginx.

- [Wodby Kubernetes platform](https://wodby.com)
- [Wodby service documentation](https://wodby.com/docs/2.0/services/)
- [Service manifest reference](https://wodby.com/docs/2.0/services/template/)

## Service overview

| Property | Manifest configuration |
| --- | --- |
| Service name | `ingress-nginx` |
| Type | Infrastructure service |
| Workload | Primary `main` Deployment with a fixed replica count |
| Container | `controller` |
| Helm chart | `ingress-nginx/ingress-nginx` from the upstream Ingress Nginx repository |
| Chart version | `4.13.2` |
| Controller configuration | Enables snippet annotations and defines Wodby annotation inputs for proxy buffer size, request body size, and annotation risk level |

The workload maps Wodby labels, annotations, and resource settings to the
corresponding Ingress Nginx Helm values.

## Role in Wodby infrastructure

Wodby installs this service through a Kubernetes system stack when it is
required by the cluster provider or selected infrastructure configuration. It
runs as a cluster-owned system app and is not offered as a user-deployable
application service.

## Platform maintenance

Changes to this repository can affect cluster provisioning, upgrades,
networking, or observability. Coordinate manifest and Helm changes with every
dependent system stack and preserve service, workload, endpoint, config, and
volume identifiers.

Wodby platform maintainers can validate the manifests with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```

See the [service manifest reference](https://wodby.com/docs/2.0/services/template/) and the [managed services index](https://github.com/wodby/services).
