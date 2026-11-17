# node-js-app-1 — qa

- Namespace: `qa` (must already exist).
- Desired replicas: `1`.
- Image: `DOCKERHUB_USERNAME/node-js-app-1:qa`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize nodejs-app/overlays/qa
```

Review before applying:

```bash
kubectl diff -k nodejs-app/overlays/qa
```
