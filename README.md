# infrastructure-as-code

[`한국어(KR)`](./README.md) | [English](./README.en-US.md)

서비스 리소스를 관리하기 위한 iac repo 입니다.

> 주로 k8s를 관리하고 있습니다.

각각의 디렉터리에 자세한 설명히 작성되어 있습니다.

보안상 중요한 config의 경우 `Private` repo에서 따로 관리되고 있습니다.

# Spec

## k8s

1. v1.19.9
1. node 3개

## helm

1. v3.5.4

# namespace

| ns   | 논리적 용도                                                                                          |
| ---- | ---------------------------------------------------------------------------------------------------- |
| test | 동작 확인과 같은 테스트를 위한 오브젝트가 배치됩니다. 언제든지 삭제되어도 문제가 되지 않아야 합니다. |
| dev  | 개발을 위한 오브젝트가 배치됩니다. 언제든지 삭제되어도 문제가 되지 않아야 합니다.                    |
| qa   | `prod`으로 넘어가기전 사용됩니다.                                                                    |
| prod | 실 서비스 용도입니다.                                                                                |

# rule

1. `yaml` 에 만드시 namespace를 명시합니다.

# objects

1. [ingress](./https-ingress-controller)
1. [storage](./storage)
1. [db](./db)
