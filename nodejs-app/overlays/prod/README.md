# node-js-app-1 — prod

- Namespace: `prod` (must already exist).
- Desired replicas: `2`.
- Image: `DOCKERHUB_USERNAME/node-js-app-1:prod`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize nodejs-app/overlays/prod
```

Review before applying:

```bash
kubectl diff -k nodejs-app/overlays/prod
```
