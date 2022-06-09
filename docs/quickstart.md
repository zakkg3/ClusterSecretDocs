## quick start:

create a ClusterSecret object yaml like the one above, or in the example in yaml/Object_example/obj.yaml and apply it in your cluster `kubectl apply -f yaml/Object_example/obj.yaml`

The ClusterSecret operator will pick it up and will create the secret in every matching namespace:  match `matchNamespace` but not matching  `avoidNamespaces` RegExp's.

You can specify multiple matching or non-matching RegExp. By default it will match all, same as defining matchNamespace = * 

### Get the clustersecrets

```bash
$> kubectl get csec -n clustersecret
NAME            TYPE
global-secret
```

### Minimal example

```yaml
apiVersion: clustersecret.io/v1
kind: ClusterSecret
metadata:
  name: global-secret
  namespace: my-fav-namespce
data:
  username: MTIzNDU2Cg==
  password: Nzg5MTAxMTIxMgo=
```