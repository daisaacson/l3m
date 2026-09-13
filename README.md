# l3m
Local Large Language Model - An attempt to create a full AI stack locally


## searxng

```shell
kubectl apply \
  -f searxng/namespace.yml \
  -f searxng/persistentvolumeclaim.yml \
  -f searxng/deployment.yml \
  -f searxng/service.yml
jinja2 searxng/ingress.yml.j2 env.json | \
  kubectl apply -f -
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
