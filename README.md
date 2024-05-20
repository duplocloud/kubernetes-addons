# DuploCloud Kubernetes Addons  

This is the Global repository for all of the DuploCloud Kubernetes Addons. These are used by adding a setting on a DuploCloud Infrastructure. The DuploCloud portal will install these as Kustomize resource from FluxCD into an Infrastructure. The addons will be maintained through this repository in with a GitOps model.  

## Register an Addons Repo 

To register addons for your portal, you simply register the Git repository by creating a FluxCD GitRepository resource. 

```yaml
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: addons
  namespace: duplocloud-system
spec:
  interval: 5m
  url: https://github.com/duplocloud/kubernetes-addons
  ref:
    branch: main
```

## Deploy and Addon 

Duplo deploys these addons by ultimately deploying these kustomize resources using FluxCD. 

```yaml
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: keda
  namespace: duplocloud-system
spec:
  interval: 10m
  targetNamespace: default
  sourceRef:
    kind: GitRepository
    name: plugins
  path: keda
  prune: true
  timeout: 1m
```

## References  

- [Duplocloud](https://duplocloud.com/)
- [FluxCD](https://fluxcd.io/)
- [Kustomize](https://kustomize.io/)
- [Helm](https://helm.sh/)
