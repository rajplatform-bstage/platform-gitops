# platform-gitops

GitOps configuration repository for the Node.js and Spring Boot applications.

## Repository layout

- `nodejs-app/`: Kustomize base and DEV/QA/UAT/PROD overlays for Node.js.
- `springboot-app/`: Kustomize base and DEV/QA/UAT/PROD overlays for Spring Boot.
- `argocd/applications/`: Argo CD Application resources.

## Important assumptions

1. Existing Kubernetes namespaces are named `dev`, `qa`, `uat`, and `prod`.
2. Node.js listens on container port `3000` and exposes `GET /health`.
3. Spring Boot listens on container port `8081` and exposes Spring Actuator health endpoints.
4. Docker Hub repositories are:
   - `DOCKERHUB_USERNAME/node-js-app-1`
   - `DOCKERHUB_USERNAME/spring-dashboard`
5. Replace `DOCKERHUB_USERNAME` in all Kustomize files with your Docker Hub username before deployment.
6. The image tags are examples. Your GitHub Actions workflows must publish the matching tags before deploying.

## Deployment safety

- DEV Argo CD Applications have automated sync enabled.
- QA, UAT, and PROD Applications are intentionally configured for manual sync.
- Do not enable automated sync for higher environments until promotion, approvals, image availability, resource capacity, and rollback procedures have been tested.
- These manifests do not create namespaces. They target the existing namespaces listed above.
- Review every rendered manifest before applying it.

## Validate locally with kubectl

From the repository root:

```bash
kubectl kustomize nodejs-app/overlays/dev
kubectl kustomize springboot-app/overlays/dev

kubectl diff -k nodejs-app/overlays/dev
kubectl diff -k springboot-app/overlays/dev
```

To deploy manually (only after reviewing the diff):

```bash
kubectl apply -k nodejs-app/overlays/dev
kubectl apply -k springboot-app/overlays/dev
```

Check:

```bash
kubectl get deployments,services,pods -n dev
```

## Argo CD

Apply the Application definitions after Argo CD is installed and configured to access this Git repository:

```bash
kubectl apply -f argocd/applications/
```

The Application resources use placeholder repository URL:

`https://github.com/YOUR_GITHUB_ORG/platform-gitops.git`

Replace it with your actual repository URL in all files under `argocd/applications/`.

For private GitHub repositories, configure repository credentials in Argo CD; do not put tokens in these YAML files.

## GitHub Actions integration (planned)

The application repositories should:
1. Test and build the application.
2. Build and push a uniquely tagged Docker image to Docker Hub (prefer the Git commit SHA as the tag).
3. Update the corresponding image tag in this repository.
4. Commit the GitOps change using a narrowly scoped GitHub token or GitHub App.

Argo CD then reconciles the environment according to its sync policy. Do not store Docker Hub passwords or GitHub tokens in this repository.

## Before first deployment

- Confirm the actual application ports and health paths.
- Confirm images exist in Docker Hub and are pullable by Kubernetes.
- Replace all placeholders.
- Check worker CPU/memory capacity and existing workload resource requests.
- Review the output of `kubectl diff -k`.
- Test DEV first.
