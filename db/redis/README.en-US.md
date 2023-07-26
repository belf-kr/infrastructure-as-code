# Hi

[한국어(KR)](./README.md) | [`English`](./README.en-US.md)

Manage redis objects.  
Used as a db for storing jwt token.

# Deployment method

Both qa and prod have the same infrastructure settings.  
Data in redis will be stored in `file share` of `Azure Files` in `AOF` way with `appendonly yes` option.
In addition, the following should be applied in advance to set the environmental variables required for the server.

1. Enable `StorageClass` for volumeMounts
1. Enable `ConfigMap` for access information

> The example below is based on `qa`.

```shell
cd qa
kubectl apply -f qa-redis-pvc.yaml
kubectl apply -f qa-redis.yaml
```

# redis-cli

Basically, redis image can be easily made an inquiry using `redis-cli`. Use it according to your situation.

```shell
# When I don't have a password
kubectl exec -it redis -- redis-cli
# If you have a password
kubectl exec -it redis -- redis-cli
auth {password}
```

> If the password is set, you can access to `redis-cli` without a password, but if you try to `r/w`, an error `(error) NOAUTH Authentication required.` is occured.
