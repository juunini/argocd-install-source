```sh
argocd app create argo-rollouts \
  --repo https://github.com/juunini/argocd-install-source.git \
  --revision HEAD \
  --path argo-rollouts \
  --dest-namespace argo-rollouts \
  --dest-server https://kubernetes.default.svc \
  --sync-option CreateNamespace=true \
  --sync-policy automated

kubectl apply -n argocd \
    -f https://raw.githubusercontent.com/argoproj-labs/rollout-extension/v0.2.1/manifests/install.yaml
```
