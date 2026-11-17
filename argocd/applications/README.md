# Argo CD Applications

These eight Application manifests assume Argo CD is installed in namespace `argocd`.

Before applying:
1. Replace `YOUR_GITHUB_ORG` in all eight YAML files with your GitHub organization or username.
2. Confirm the GitOps repository URL and branch (`main`).
3. Confirm that the referenced Docker Hub image tags exist.
4. Confirm that namespaces `dev`, `qa`, `uat`, and `prod` already exist.

DEV Applications have automated sync, pruning, and self-healing enabled. QA/UAT/PROD have no automated sync block, so they require a manual sync action in Argo CD.

Apply:

```bash
kubectl apply -f argocd/applications/
```

For a private GitHub repository, register repository credentials securely in Argo CD before creating these Applications.
