# k8s_argocd

## Installation of argoCD into the cluster
Installation ArgoCD

✅ 1. Add the Argo CD Helm repo

```
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
```

✅ 2. Pick the Argo CD chart version
Check available versions:
```
helm search repo argo/argo-cd --versions
```
Example output includes versions like:
```
• 7.5.x
• 7.4.x
• etc.
```
Let's assume you want to install chart version 7.5.2 (example — replace with your preferred one).

✅ 3. create a namespace

```
k create namespace argocd
```

✅ 4. (Optional) Provide a custom values.yaml
If you want to modify the installation (e.g., enabling LoadBalancer or Ingress), create a file:
values.yaml
```
server:
  service:
    type: LoadBalancer
  ingress:
    enabled: false
```
Then install with:
```
helm install argocd argo/argo-cd \
  -n argocd \
  -f values.yaml \
  --version 9.1.4
```



It takes long time to show the services…





This deploys:
```
	• argocd-server
	• argocd-application-controller
	• argocd-repo-server
	• dex (optional)
	• redis
	• configs / RBAC
```
✅ 5. Access the UI
Use the LB + the /etc/hosts file


Open:

`https://argo.cd:80`

```
Username: admin
password: JHaNFcepvlRt0C7R
```
✅ 6. Get initial admin password
```
k -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d
```



## Examples
### Example 1 - Basic application
path: gitops/basic --> this is the source of true for the basic example


### Example 2 - kustomize application
path: kustomize/overlays/dev --> this is the source of true for dev

path: kustomize/overlays/prod --> this is the source of true for prod


### Example 3 - Helm charts
path: helm/ --> this is the source of true for the helm-chart

#### download an helm-chart
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update

helm search repo prometheus-community/kube-prometheus-stack



helm pull prometheus-community/kube-prometheus-stack --version 79.7.1

tar -xvf kube-prometheus-stack-79.7.1.tgz

rm kube-prometheus-stack-79.7.1.tgz
