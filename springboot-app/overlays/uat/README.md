# spring-dashboard — uat

- Namespace: `uat` (must already exist).
- Desired replicas: `2`.
- Image: `DOCKERHUB_USERNAME/spring-dashboard:uat`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize springboot-app/overlays/uat
```

Review before applying:

```bash
kubectl diff -k springboot-app/overlays/uat
```
