```sh
argocd app create argo-workflows \
  --repo https://github.com/juunini/argocd-install-source.git \
  --revision HEAD \
  --path argo-workflows \
  --dest-namespace argo \
  --dest-server https://kubernetes.default.svc \
  --sync-option CreateNamespace=true \
  --sync-policy automated
```
