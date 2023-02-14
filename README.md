# argocd-install-source

## Install argocd

```sh
kubectl create namespace argocd

echo "apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  - https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/ha/install.yaml

components:
  - https://github.com/argoproj-labs/argocd-extensions/manifests
" > kustomization.yaml

kubectl kustomize . | kubectl apply -f - -n argocd
rm kustomization.yaml

kubectl rollout status deployment -n argocd

kubectl apply -n argocd \
    -f https://raw.githubusercontent.com/argoproj-labs/rollout-extension/v0.2.1/manifests/install.yaml

PASSWORD=kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
echo -e "
USERNAME: admin
PASSWORD: ${PASSWORD}"
```

## Install argocd cli

https://argo-cd.readthedocs.io/en/stable/cli_installation/

## Install ingress-nginx on argocd

```sh
argocd app create ingress-nginx \
  --repo https://github.com/kubernetes/ingress-nginx.git \
  --revision controller-v1.5.1 \
  --path deploy/static/provider/cloud \
  --dest-namespace ingress-nginx \
  --dest-server https://kubernetes.default.svc \
  --sync-option CreateNamespace=true \
  --sync-policy automated
```

## Install cert-manager on argocd

```sh
argocd app create cert-manager \
  --repo https://charts.jetstack.io \
  --helm-chart cert-manager \
  --revision v1.11.0 \
  --helm-set installCRDs=true \
  --dest-namespace cert-manager \
  --dest-server https://kubernetes.default.svc \
  --sync-option CreateNamespace=true \
  --sync-policy automated
```
