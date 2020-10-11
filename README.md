# Helm charts for adminio

simple helm charts for [adminio-api](https://github.com/rzrbld/adminio-api) and [adminio-ui](https://github.com/rzrbld/adminio-ui).
written for openshift/okd but suitable for k8s. All containers run in unprivileged mode.

### Requirements
- [Helm-install](https://helm.sh/docs/intro/install/)
- k8s/okd/openshift cluster
- adminio-ui image with tag `release-1.4` or greater

### Content
- adminio: chart for [adminio-api](https://github.com/rzrbld/adminio-api)
- adminio-ui: chart for [adminio-ui](https://github.com/rzrbld/adminio-ui)

login and passwords will be stored in Secret all other env variables in ConfigMaps

### Examples
run adminio-api:
```
noglob helm install --set configmap.data.MINIO_HOST_PORT='1.1.1.1:9000',secret.MINIO_SECRET='my-scret',secret.MINIO_ACCESS='my-access',ingress.hosts[0].host=adminio.example.com,ingress.hosts[0].paths[0]='/' my-deploy-name adminio
```
run adminio-ui:
```
noglob helm install --set-string configmap.data.API_BASE_URL='http://adminio.example.com:80',configmap.data.ADMINIO_MULTI_BACKEND='false',configmap.data.ADMINIO_BACKENDS='[]',configmap.data.NGX_ROOT_PATH='/ui',configmap.data.NGX_PORT='8000' --set ingress.hosts[0].host=adminio.example.com,ingress.hosts[0].paths[0]='/ui' my-deploy-ui-name adminio-ui
```

after that, api will be available at `http://adminio.example.com/` ui at `http://adminio.example.com/ui`


### Where is my good old k8s yamls

Here it is:
```
helm install my-name adminio --dry-run --debug
```
Now you can: copy, paste and run `kubectl apply` or `oc aplly`
