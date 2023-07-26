# Hi

[한국어(KR)](./README.md) | [`English`](./README.en-US.md)

Storage object that stores files. It uses Azure Files, primarily the `File Sharing` feature.

# Allocation method

Assign a storage account with `azure-files-sc.yaml` and create the required `pvc` and use it dynamically.

> `pvc` is designed to be managed by services and objects that require permanent storage.
