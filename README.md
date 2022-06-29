## Setting up ArgoCD

```bash
# install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# access ArgoCD UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below token (as in documentation):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# you can change and delete init password

```

## Deploying Redux Punch

```bash
kubectl apply -n argocd -f application.yaml
```

Wait for the ArgoCD to complete the deployment, then execute
```bash
kubectl port-forward svc/redux-punch 3000:3000 -n redux-punch
```

You can now access the application on http://localhost:3000

Note that whenever this repository is modified to update the new version of redux-punch, auto deployment happens.
