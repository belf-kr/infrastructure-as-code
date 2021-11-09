# Hi

redis object를 관리합니다.  
jwt token을 저장하기위한 db로 사용됩니다.

# 배포 방법

qa, prod 모두 인프라 설정은 같습니다.  
redis의 데이터는 `appendonly yes` 옵션으로 `AOF` 방식으로 `Azure Files` 의 `파일 공유` 에 데이터를 저장합니다.  
이외 server에 필요한 환경변수를 설정하기 위하여 사전에 아래의 내용이 적용되어 있어야합니다.

1. volumeMounts를 위한 `StorageClass` 활성화
1. 접속 정보를 위한 `ConfigMap` 활성화

> 아래의 예제는 `qa` 를 기준으로 설명하고 있습니다.

```shell
cd qa
kubectl apply -f qa-redis-pvc.yaml
kubectl apply -f qa-redis.yaml
```

# redis-cli

기본적으로 redis image는 `redis-cli` 를 이용하여 손쉽게 데이터를 조회할 수 있습니다. 상황에 맞게 사용하도록 합니다.

```shell
# 비밀번호 없을 때
kubectl exec -it redis -- redis-cli
# 비밀번호가 있는 경우
kubectl exec -it redis -- redis-cli
auth {비밀번호}
```

> 비밀번호가 설정된 경우 비밀번호 없이 `redis-cli` 까지는 접속은 되지만 `r/w` 를 하려고 하면 `(error) NOAUTH Authentication required.` 에러가 발생합니다.
