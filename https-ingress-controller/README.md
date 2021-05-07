# 업데이트 방법

```shell
kubectl apply -f cluster-issuer.yaml
kubectl apply -f hello-world-ingress.yaml --namespace ingress-basic
```

# 테스트 컨테이너

삭제하기 편하도록 `test` namespace에서 진행하였습니다.

```shell
kubectl create ns test
kubectl apply -f aks-helloworld-one.yaml -n test
kubectl apply -f aks-helloworld-two.yaml -n test
```
