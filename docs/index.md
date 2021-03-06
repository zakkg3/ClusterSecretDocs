# ClusterSecret
![CI](https://github.com/zakkg3/ClusterSecret/workflows/CI/badge.svg) [![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/4283/badge)](https://bestpractices.coreinfrastructure.org/projects/4283)[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

---

Kubernetes ClusterSecret 

Global inter-namespace cluster secrets - Secrets that work across namespaces  - Clusterwide secrets

ClusterSecret operator makes sure all the matching namespaces have the secret available. New namespaces, if they match the pattern, will also have the secret.
Any change on the ClusterSecret will update all related secrets. Deleting the ClusterSecret deletes "child" secrets (all cloned secrets) too.

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


### Digests

latest = 0.0.9

docker.io/flag5/clustersecret:

to-do: Automate Digest into doc 
{{ latestTag }}:{{ latestDiegest }}

0.0.7 digest: sha256:c8dffeefbd3c8c54af67be81cd769e3c18263920729946b75f098065318eddb1
0.0.7_arm32: digest: sha256:ffac630417bd090c958c9facf50a31ba54e0b18c89ef52d8eec5c1326a5f20ad


 

 
 * * *
 
