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

## Install ingress-nginx on argocd

| Name | Value |
| - | - |
| Repository | `https://github.com/kubernetes/ingress-nginx.git` |
| Branch | `controller-v1.5.1` |
| Path | `deploy/static/provider/cloud` |

## Install cert-manager on argocd

| Name | Value |
| - | - |
| Helm | `https://charts.jetstack.io` |
| Chart | `cert-manager` |
| Version | `v1.11.0` |

`installCRDs`: `true`
