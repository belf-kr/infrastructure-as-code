# Hi

[`한국어(KR)`](./README.md) | [English](./README.en-US.md)

파일을 저장하는 storage 오브젝트입니다. Azure Files를 사용하며 주로 `파일 공유` 기능을 사용합니다.

# 할당 방법

`azure-files-sc.yaml` 으로 스토리지 계정을 할당 후 필요한 `pvc` 를 생성해서 동적으로 사용하시면 됩니다.

> `pvc` 는 영구적인 저장소가 필요한 서비스 및 object에서 관리하도록 디자인되어 있습니다.
