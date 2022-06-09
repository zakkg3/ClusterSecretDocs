## install

### Clone & kubectl

`git clone git@github.com:zakkg3/ClusterSecret.git`


### Helm chart.

Comming soon official helm chart. 


### Requirements

Current version 0.0.8 is tested for Kubernetes >= 1.25

For older kubernes (<1.19) use the image tag "0.0.6" in  yaml/02_deployment.yaml

### tl;dr install

```bash
cd ClusterSecret
kubectl apply -f ./yaml
```

### step by step

To instal ClusterSecret operator we need to create (in this order):

 - RBAC resources (avoid if you are not running RBAC) to allow the operator to create/update/patch secrets: yaml/00_
 - Custom resource definition for the ClusterSecret resource: yaml/01_crd.yaml
 - The ClusterSecret operator itself: yaml/02_deployment.yaml || For **ARM architectures**: yaml/arm32v7/02_deployment.yam