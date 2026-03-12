# example-app-animals
An example app for deployment on OpenShift via ArgoCD that outputs animal names.

You can deploy this via ArgoCD like this:
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: random-animal-app
  namespace: openshift-gitops 
spec:
  project: default
  source:
    repoURL: 'https://github.com/yourusername/your-repo.git' # Replace with your repo
    targetRevision: HEAD
    path: app
  destination:
    server: 'https://kubernetes.default.svc'
    namespace: ranimals # Replace with your target namespace
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
  syncOptions:
    - CreateNamespace=true
```

Ensure this label is on your target namespace:

`argocd.argoproj.io/managed-by=openshift-gitops`