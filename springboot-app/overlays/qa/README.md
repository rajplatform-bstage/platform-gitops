# spring-dashboard — qa

- Namespace: `qa` (must already exist).
- Desired replicas: `1`.
- Image: `DOCKERHUB_USERNAME/spring-dashboard:qa`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize springboot-app/overlays/qa
```

Review before applying:

```bash
kubectl diff -k springboot-app/overlays/qa
```
