# l3m
Local Large Language Model - An attempt to create a full AI stack locally


## searxng

```shell
kubectl apply \
  -f searxng/namespace.yml \
  -f searxng/persistentvolumeclaim.yml \
  -f searxng/deployment.yml \
  -f searxng/service.yml
jinja2 searxng/ingress.yml.j2 env.json | kubectl apply -f -
```