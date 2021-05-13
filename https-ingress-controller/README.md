# Hi

HTTP ingress를 생성하는 방법에 대해 가이드합니다.  
사전에 [해당 문서](https://docs.microsoft.com/ko-kr/azure/aks/ingress-tls)를 통해 `NGINX 수신 컨트롤러`, `인증서 관리자 컨트롤러` 활성화를 필수 조건으로 합니다.

# Let's Encrypt 발급자 생성

```shell
kubectl apply -f cluster-issuer.yaml
```

아래의 명령어를 통해 발급된 TLS를 확인할 수 있습니다.

```shell
kubectl get certificate -n ingress-basic
```

# Ingress

## Spec

1. ns
   1. ingress-basic
1. 다른 ns에서 생성된 service를 가져오는 경우 `external-{ns}-{사용하는 서비스 이름}` 으로 네이밍
1. tls의 경우 `tls-{도메인 주소}` 으로 네이밍

## 생성 및 업데이트

```shell
kubectl apply -f main-ingress.yaml
```

# 이외

## 수신 구성 테스트

삭제하기 편하도록 `test` namespace에서 실행하도록 되어있습니다.

```shell
kubectl create ns test
kubectl apply -f ./test/aks-helloworld-one.yaml
kubectl apply -f ./test/aks-helloworld-two.yaml
kubectl apply -f ./test/node-test.yaml
```
