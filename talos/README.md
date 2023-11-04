# Bootstrap

## Talos

### Create Talos Secrets

```
talhelper gensecret > talsecret.sops.yaml
sops -e -i talsecret.sops.yaml
talhelper genconfig
export TALOSCONFIG=~/k8s-gitops/talos/clusterconfig/talosconfig
```

```
talosctl -n 10.0.14.7 apply-config --file clusterconfig/k8s-nuc0*.yaml --insecure
talosctl -n 10.0.14.8 apply-config --file clusterconfig/k8s-nuc1*.yaml --insecure
talosctl -n 10.0.14.9 apply-config --file clusterconfig/k8s-nuc2*.yaml --insecure
talosctl -n 10.0.14.13 apply-config --file clusterconfig/k8s-dogbert*.yaml --insecure
talosctl -n 10.0.14.14 apply-config --file clusterconfig/k8s-catbert*.yaml --insecure
talosctl -n 10.0.14.15 apply-config --file clusterconfig/k8s-alice*.yaml --insecure
talosctl -n 10.0.14.16 apply-config --file clusterconfig/k8s-wally*.yaml --insecure
talosctl -n 10.0.14.17 apply-config --file clusterconfig/k8s-phil*.yaml --insecure
```

### Talos Setup

```
talosctl -n 10.0.14.7 bootstrap
talosctl -n 10.0.14.7 kubeconfig -f
kubectl get no -o wide
```

### Post Talos Setup

```
kubectl kustomize --enable-helm ./cni | kubectl apply -f -
```
