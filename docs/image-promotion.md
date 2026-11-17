# Image promotion workflow

Use immutable image tags, preferably the full Git commit SHA, rather than reusing `latest`.

Example:
- Node.js image: `DOCKERHUB_USERNAME/node-js-app-1:COMMIT_SHA`
- Spring Boot image: `DOCKERHUB_USERNAME/spring-dashboard:COMMIT_SHA`

After CI publishes an image, update the `newTag` field in the target overlay's `kustomization.yaml`.

Example:

```yaml
images:
  - name: DOCKERHUB_USERNAME/node-js-app-1
    newName: DOCKERHUB_USERNAME/node-js-app-1
    newTag: 0123456789abcdef
```

The GitOps commit is the deployment change. Argo CD detects it and reconciles the DEV Application automatically. For QA/UAT/PROD, use reviewed promotion commits and manual Argo CD sync until the approval workflow is implemented.

For stronger supply-chain traceability, record and promote the image digest (`sha256:...`) as well as the human-readable tag. Kustomize's `images.newTag` field accepts tags; digest-based references can be configured using Kustomize image digest support.
