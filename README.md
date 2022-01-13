# Service ingress-nginx

## Update instructions

- Get manifests from `https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v[VERSION]/deploy/static/provider/cloud/deploy.yaml`
- Clean up helm labels (we don't use helm)
- Clean up empty annotations