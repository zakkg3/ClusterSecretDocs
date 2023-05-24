## install

### Using the official helm chart

```bash
helm repo add clutersecret https://charts.clustersecret.io/
helm install cluster-secret clutersecret/cluster-secret --version 0.1.0
```

### kubectl

clone the repo and apply

```bash
cd ClusterSecret
kubectl apply -f ./yaml
```


## Requirements

Current version 0.0.8 is tested for Kubernetes >= 1.25

For older kubernes (<1.19) use the image tag "0.0.6" in  yaml/02_deployment.yaml



## step by step

To instal ClusterSecret operator we need to create (in this order):

 - RBAC resources (avoid if you are not running RBAC) to allow the operator to create/update/patch secrets: yaml/00_
 - Custom resource definition for the ClusterSecret resource: yaml/01_crd.yaml
 - The ClusterSecret operator itself: yaml/02_deployment.yaml || For **ARM architectures**: yaml/arm32v7/02_deployment.yam
