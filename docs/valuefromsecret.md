### Value From another secret.

With this we can tell ClusterSecret to take the values from an existing secret.
yaml/Object_example/value-from-obj.yaml have a working example. Note that you will need first to have the obj2.yaml applied (the source secret).

```
data:
  valueFrom:
    secretKeyRef:
      name: <secre-name>
      namespace: <source-namespace>
```

to-do is to specify keys or matched keys to only sync that ones. For now it will sync the whole secret.