# Hi

[`한국어(KR)`](./README.md) | [English](./README.en-US.md)

mysql 관련 object를 관리합니다.  
ORM을 위해 필요한 database가 미리 생성되어 있어야 합니다.  
이를 위해서 컨테이너 실행 시 기본 init sql을 실행할 수 있는 별도의 이미지가 필요합니다.

# 필수

아래의 작업을 필수적으로 진행합니다.

> `tag` 은 패치 내역에 맞게 동적으로 바꾸도록 합니다.

```shell
cd basic-image
docker build -t ghcr.io/belf-kr/basic-mysql-5.7.16:v0.1.0 .
docker push ghcr.io/belf-kr/basic-mysql-5.7.16:v0.1.0
```

# 종류

## Deployment

qa 환경에서 사용되는 mysql db 입니다.  
Azure File Storage를 사용합니다.

### 배포 방법

사전에 아래의 내용이 적용되어 있어야합니다.

1. volumeMounts를 위한 `StorageClass` 활성화
1. 접속 정보를 위한 `ConfigMap` 활성화
1. init sql를 위한 image으로 tag가 잘 지정됫는지 확인

```shell
cd deployment
kubectl apply -f qa-mysql-pvc.yaml
kubectl apply -f qa-mysql.yaml
```

## replicated-stateful

prod 환경에서 사용되는 mysql db 입니다.  
`master`, `slave` 이루어진 mysql replication 입니다.  
Azure Disk Storage를 사용합니다.

### 배포 방법

사전에 아래의 내용이 적용되어 있어야합니다.

1. volumeMounts를 위한 `default StorageClass` 활성화
   > 여기서는 AKS에서 기본으로 제공하는 StorageClass의 `Azure Disk` 를 사용하기 때문에 따로 건드릴 것은 없습니다.
1. init sql를 위한 image으로 tag가 잘 지정됫는지 확인

```shell
cd replicated-stateful
kubectl apply -f prod-mysql-cm.yaml
kubectl apply -f prod-mysql-svc.yaml
kubectl apply -f prod-mysql.yaml
```

# mysql-cli

`prod` 환경의 경우 외부에서 접속할 수 없도록 되어있습니다.  
때문에 db에 접속해서 query를 실행하고 싶은 경우 k8s cluster에 mysql container를 배포 후 컨테이너 내부를 통하여 접속해야합니다.

> 아래에 있는 환경에 따른 접속방법은 템플릿으로만 사용하세요. 접속 주소는 언제든지 변경될 수 있음으로 `config-map` 를 참고하도록 합니다.

## container 실행

```shell
kubectl run mysql-client --image=mysql:5.7 -it --rm --restart=Never -- /bin/bash
```

## qa

```shell
$ mysql -h mysql.qa -u {사용자이름} -p
$ Enter password: {비밀번호}
```

## prod: master

```shell
$ mysql -h mysql-0.mysql.prod -u {사용자이름} -p
$ Enter password: {비밀번호}
```

## prod: slave

```shell
$ mysql -h mysql-read.prod -u {사용자이름} -p
$ Enter password: {비밀번호}
```
