# Hi

[한국어(KR)](./README.md) | [`English`](./README.en-US.md)

Manage mysql related objects.  
The database must be pre-created for ORM .  
This requires a separate image to run the default init sql when running the container.

# Required Tasks

The following tasks are mandatory.

> Let's dynamically change `tag` to match the patch history.

```shell
cd basic-image
docker build -t ghcr.io/belf-kr/basic-mysql-5.7.16:v0.1.0 .
docker push ghcr.io/belf-kr/basic-mysql-5.7.16:v0.1.0
```

# Types

## Deployment

Mysql db used in qa environment.  
Use Azure File Storage.

### Deployment method

The following should be applied beforehand.

1. Enable `StorageClass` for volumeMounts
1. Enable `ConfigMap` for access information
1. Verify that the tag is well specified as an image for init sql

```shell
cd deployment
kubectl apply -f qa-mysql-pvc.yaml
kubectl apply -f qa-mysql.yaml
```

## replicated-stateful

Mysql db used in the prod environment.  
It is mysql replication that consists of `master` and `slave`.  
Use Azure Disk Storage.

### Deployment method

The following should be applied beforehand.

1. Enable `default StorageClass` for volumeMounts
   > We use the `Azure Disk` of StorageClass, which is native to AKS, so there's nothing to touch.
1. Verify that the tag is well specified as an image for init sql

```shell
cd replicated-stateful
kubectl apply -f prod-mysql-cm.yaml
kubectl apply -f prod-mysql-svc.yaml
kubectl apply -f prod-mysql.yaml
```

# mysql-cli

The `prod` environment is not accessible from outside.  
Therefore, if you want to access the db and run query, you must deploy mysql container in the k8s cluster and access it through the inside of the container.

> Use only templates for access methods based on the environment below. Refer to `config-map` because the connection address can be changed at any time.

## Run container

```shell
kubectl run mysql-client --image=mysql:5.7 -it --rm --restart=Never -- /bin/bash
```

## qa

```shell
$ mysql -h mysql.qa -u {user name} -p
$ Enter password: {password}
```

## prod: master

```shell
$ mysql -hmysql-0.mysql.prod -u {user name} -p
$ Enter password: {password}
```

## prod: slave

```shell
$ mysql -h mysql-read.prod -u {user name} -p
$ Enter password: {password}
```
