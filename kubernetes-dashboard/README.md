```sh
argocd app create kubernetes-dashboard \
  --repo https://github.com/juunini/argocd-install-source.git \
  --revision HEAD \
  --path kubernetes-dashboard \
  --dest-namespace kubernetes-dashboard \
  --dest-server https://kubernetes.default.svc \
  --sync-option CreateNamespace=true \
  --sync-policy automated
```
