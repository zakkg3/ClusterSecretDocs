# ClusterSecret
![CI](https://github.com/zakkg3/ClusterSecret/workflows/CI/badge.svg) [![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/4283/badge)](https://bestpractices.coreinfrastructure.org/projects/4283) [![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html) [![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/clutersecret)](https://artifacthub.io/packages/search?repo=clutersecret)

---

Cluster wide secrets

ClusterSecret operator makes sure all the matching namespaces have the secret available and up to date.

 - New namespaces, if they match the pattern, will also have the secret.
 - Any change on the ClusterSecret will update all related secrets. Including changing the match pattern. 
 - Deleting the ClusterSecret deletes "child" secrets (all cloned secrets) too.

![Cluster Secret overview](https://github.com/zakkg3/ClusterSecret/raw/master/docs/clusterSecret.png)



---

Here is how it looks like:

```yaml
Kind: ClusterSecret
apiVersion: clustersecret.io/v1
metadata:
  namespace: clustersecret
  name: default-wildcard-certifiate
matchNamespace:
  - prefix_ns-*
  - anothernamespace
avoidNamespaces:
  - supersecret-ns
data:
  tls.crt: BASE64
  tls.key: BASE64
```


## Use cases.


Use it for certificates, registry pulling credentials and so on.

when you need a secret in more than one namespace. you have to: 

1- Get the secret from the origin namespace.
2- Edit the  the secret with the new namespace.
3- Re-create the new secret in the new namespace. 


This could be done with one command:

```bash
kubectl get secret <secret-name> -n <source-namespace> -o yaml \
| sed s/"namespace: <source-namespace>"/"namespace: <destination-namespace>"/\
| kubectl apply -n <destination-namespace> -f -
```

Clustersecrets automates this. It keep track of any modification in your secret and it will also react to new namespaces. 


## Limit ClusterSecret to certain namespaces.

This can be archived by changing the RBAC.
You may want to replace https://github.com/zakkg3/ClusterSecret/blob/master/yaml/00_rbac.yaml#L43-L46
for a new namespaced role and its correspondent rolebinding.

Here is the official doc:
https://kubernetes.io/docs/reference/access-authn-authz/rbac/

### Update a ClusterSecret object

This will trigger the operator to also update all secrets that it matches.


### optional

overwrite the deployment command with kopf namespaces instead of the "-A" (all namespaces)



 
 * * *
 
