# Hi

[한국어(KR)](./README.md) | [`English`](./README.en-US.md)

Provides instructions on how to create HTTP ingress.  
Activation of `NGINX Receiving Controller` and `Certificate Manager Controller` is a prerequisite in advance through [Applicable Document](https://docs.microsoft.com/ko-kr/azure/aks/ingress-tls).

# Create `Let's Encrypt` Issuer

```shell
kubectl apply -f cluster-issuer.yaml
```

You can check the issued TLS using the command below.

```shell
kubectl get certificate -n ingress-basic
```

# Ingress

## Spec

1. ns
   1. ingress-basic
1. If you import a service created by another ns, name it as `external-{ns}-{Service name used}`
1. For tls, name it as `tls-{domain address}`

## Creating and updating

```shell
kubectl apply -f main-ingress.yaml
```

## A useful command

```shell
# svc can be checked as external series for ingress
kubectl get svc -n ingress-basic
```

# Others

## Test receive configuration

It will be run in `test` namespace for ease of deletion.

```shell
kubectl create ns test
# It may not be operating normally at this time. [Please check the issue](https://github.com/belf-kr/infrastructure-as-code/issues/1)
kubectl apply -f ./test/aks-helloworld-one.yaml
kubectl apply -f ./test/aks-helloworld-two.yaml
kubectl apply -f ./test/node-test.yaml
```
