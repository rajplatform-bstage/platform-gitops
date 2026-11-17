# spring-dashboard — prod

- Namespace: `prod` (must already exist).
- Desired replicas: `2`.
- Image: `DOCKERHUB_USERNAME/spring-dashboard:prod`.
- This overlay inherits the shared manifests from `../../base`.

Render with:

```bash
kubectl kustomize springboot-app/overlays/prod
```

Review before applying:

```bash
kubectl diff -k springboot-app/overlays/prod
```
