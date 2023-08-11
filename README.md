Chart-repo
==========

This is just a helm-chart repo test. You can install an nginx website with it
like this:
```bash
helm repo add norling https://norling.github.io/chart-repo/
helm show values norling/website > values.yaml
<edit values.yaml>
helm install -f values.yaml <name> norling/website
```

### Dependencies

The system needs the certmanager CRDs installed before the system can run. To
install them, run:
```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.12.0 \
  --set installCRDs=true
```

For ingress to work, install the nginx ingress controller first.
This can be done in various ways, depending on which kuberenetes system is used,
but this is how to install it using helm:
```bash
helm upgrade --install ingress-nginx ingress-nginx \
    --repo https://kubernetes.github.io/ingress-nginx \
    --namespace ingress-nginx --create-namespace
```

Documentation for ingress-nginx is available at:
https://kubernetes.github.io/ingress-nginx/
