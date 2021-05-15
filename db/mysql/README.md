# Hi

mysql 관련 object를 관리합니다.  
ORM을 위해 필요한 database가 미리 생성되어 있어야 합니다.  
이를 위해서 컨테이너 실행 시 기본 init sql을 실행할 수 있는 별도의 이미지가 필요합니다.

# 필수

아래의 작업을 필수적으로 진행합니다.

> tag은 패치 내역에 맞게 동적으로 바꾸도록 합니다.

```shell
cd basic-image
docker build -t ghcr.io/belf-kr/basic-mysql-5.7:v0.1.0 .
docker push ghcr.io/belf-kr/basic-mysql-5.7:v0.1.0
```

# 종류

## deployment

qa 환경에서 사용되는 mysql db 입니다.  
Azure File Storage를 사용합니다.

```shell
cd deployment
kubectl apply -f qa-mysql-pvc.yaml
kubectl apply -f qa-mysql.yaml
```

## replicated-stateful

prod 환경에서 사용되는 mysql db 입니다.  
`master`, `slave` 이루어진 mysql replication 입니다.  
Azure Disk Storage를 사용합니다.
