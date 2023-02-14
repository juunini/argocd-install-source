```sh
argocd app create argo-events \
  --repo https://github.com/juunini/argocd-install-source.git \
  --revision HEAD \
  --path argo-events \
  --dest-namespace argo-events \
  --dest-server https://kubernetes.default.svc \
  --sync-option CreateNamespace=true \
  --sync-policy automated
```
