# argocd-install-source

## Install argocd

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl rollout status deployment -n argocd
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
