# Core

Core manifests are the base of the cluster. They're applied manually, or bootstrapped by the cluster.

## argocd.yaml
This manifest is used to bootstrap argocd on the cluster. It creates the `argocd` namespace, and installs the ArgoCD dependencies.
When creating this file on the control plane, it will automatically be applied to the cluster.

It should be copied to `/var/lib/rancher/k3s/server/manifests/argocd.yaml` on the control plane node.

## sync.yaml
This manifest is used to create a "root" application called `sync` in ArgoCD. 

This pattern is called `App of Apps` and is used to manage the cluster declaratively with ArgoCD.
It configures ArgoCD to watch the `apps` directory in this repository, and syncs the applications in that directory.
The applications configured there can then refer to manifests local to this repository, or remote repositories.

It is applied manually.

## aws-creds.sealed.yaml
This manifest is used to create a secret in the `kube-system` namespace, which is used to authenticate to AWS.

It is applied manually.
