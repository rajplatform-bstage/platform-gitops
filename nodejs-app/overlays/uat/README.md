# node-js-app-1 — uat

- Namespace: `uat` (must already exist).
- Desired replicas: `2`.
- Image: `DOCKERHUB_USERNAME/node-js-app-1:uat`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize nodejs-app/overlays/uat
```

Review before applying:

```bash
kubectl diff -k nodejs-app/overlays/uat
```
