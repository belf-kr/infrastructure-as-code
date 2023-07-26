# infrastructure-as-code

[`한국어(KR)`](./README.md) | [English](./README.en-US.md)

IaC repo for managing service resources.

> It mainly managed by k8s.

It is written in detail in each directory.

Security-critical configurations are managed separately by the `Private` repo.

# Spec

## k8s

1. v1.19.9
1. Three nodes

## helm

1. v3.5.4

# namespace

| ns   | logical use                                                                                                      |
| ---- | ---------------------------------------------------------------------------------------------------------------- |
| Test | Object is placed for testing, such as checking behavior. It shouldn't be a problem if you delete it at any time. |
| dev  | Object is placed for development. It shouldn't be a problem if you delete it at any time.                        |
| qa   | Used before moving on to `prod`.                                                                                 |
| prod | For real service purpose.                                                                                        |

# rule

1. Namespace must be specified in `yaml`.

# objects

1. [ingress](./https-ingress-controller)
1. [storage](./storage)
1. [db](./db)
