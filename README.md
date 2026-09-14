# l3m
Local Large Language Model - An attempt to create a full AI stack locally

## Prerequisites

Items not convered here:
* Load balancer: [metallb](https://metallb.io/)
* Cert-manager: [Cert-manager](https://cert-manager.io/)
  * Certifates: [Let's Encrypt](https://letsencrypt.org/)
* Storage: [Longhorn](https://longhorn.io/)

## searxng

```shell
kubectl apply \
  -f searxng/namespace.yaml \
  -f searxng/persistentvolumeclaim.yaml \
  -f searxng/deployment.yaml \
  -f searxng/service.yaml
jinja2 searxng/ingress.yaml.j2 env.json | \
  kubectl apply -f -
```

```plaintext
vi /etc/searxng/settings.yml
search:
  formats:
    - html
    - json
```

## open-webui

I'm using the [Quick Start](https://docs.openwebui.com/getting-started/quick-start/).  
Full [Kubernetes Deployment](https://docs.openwebui.com/deployment/kubernetes)  documentation.

```shell
kubectl create namespace openwebui
helm repo add open-webui https://open-webui.github.io/helm-charts
helm repo update
jinja2 open-webui/values.yaml.j2 env.json | \
  helm upgrade --install -n openwebui openwebui open-webui/open-webui -f -
```

Configure web search