# Ingress Nginx service for Wodby

Deploy the Kubernetes Ingress Nginx controller with
[Wodby](https://wodby.com). This repository contains the `service.yml` manifest
used to define the Wodby infrastructure service.

- [Ingress Nginx project](https://kubernetes.github.io/ingress-nginx/)
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

## Use this service

A service is a reusable component and does not deploy by itself. Add the
service to a stack intended for cluster infrastructure, publish the stack, and
then create or upgrade the corresponding infrastructure app.

To maintain your own version of the service:

1. Fork this repository.
2. Edit [`service.yml`](service.yml).
3. Import the repository as a
   [Git-backed service](https://wodby.com/docs/2.0/services/create/#create-a-git-backed-service).
4. Reference `ingress-nginx` from your stack manifest.

Wodby imports the manifest from the selected Git branch or tag and creates a
new service revision when the Git-backed service is updated.

## Customize the service

Common changes include updating the chart version, exposing additional Helm
values, changing controller configuration, and setting workload resources.

Keep the `main` workload, `controller` container, annotation names, and Helm
value paths stable unless dependent stacks and app-level overrides are updated
at the same time. These identifiers are part of the downstream contract.

Validate a customized manifest with the Wodby CLI before importing it:

```bash
wodby service validate-manifest service.yml --org <org-id>
```

See the [service manifest reference](https://wodby.com/docs/2.0/services/template/)
for every supported field and the [managed services
index](https://github.com/wodby/services) for current catalog services.
