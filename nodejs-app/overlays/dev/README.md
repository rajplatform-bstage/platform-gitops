# node-js-app-1 — dev

- Namespace: `dev` (must already exist).
- Desired replicas: `1`.
- Image: `DOCKERHUB_USERNAME/node-js-app-1:dev`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize nodejs-app/overlays/dev
```

Review before applying:

```bash
kubectl diff -k nodejs-app/overlays/dev
```
