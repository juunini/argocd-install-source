```sh
argocd app create argocd \
  --repo https://github.com/juunini/argocd-install-source.git \
  --revision HEAD \
  --path argocd \
  --dest-namespace argocd \
  --dest-server https://kubernetes.default.svc \
  --sync-option CreateNamespace=true \
  --sync-policy automated
```
