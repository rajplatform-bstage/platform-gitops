# spring-dashboard — dev

- Namespace: `dev` (must already exist).
- Desired replicas: `1`.
- Image: `DOCKERHUB_USERNAME/spring-dashboard:dev`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize springboot-app/overlays/dev
```

Review before applying:

```bash
kubectl diff -k springboot-app/overlays/dev
```
