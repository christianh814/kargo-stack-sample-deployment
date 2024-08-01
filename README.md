# Kargo Stack Sample Deployment

Repo shows how to get a baseline Kargo "stack" install (i.e. Kargo + [Dependencies](https://kargo.akuity.io/how-to-guides/installing-kargo#basic-installation))

* Kargo
* Cert Manager
* Argo Rollouts

## Argo CD

You must enable helm with kustomize to your Argo CD installation by adding `--enable-kustomize` to the `argocd-cm` ConfigMap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: argocd-cm
  namespace: argocd
data:
  kustomize.buildOptions: --enable-helm
```

Once that is done, you can apply the included ApplicationSet

```shell
kubectl apply -f kargo-appset.yaml
```

## Kargo UI

This repo doesn't use ingress, so you need to get to the UI using port forwarding:

```shell
kubectl port-forward -n kargo services/kargo-api 8080:443
```

The UI will be available under [https://localhost:8080](https://localhost:8080)

If you're using the repo "as is", the login information for Kargo is set to:

Username: `admin`
Password: `admin`
