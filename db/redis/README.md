# Hi

redis object를 관리합니다.

# 종류

## redis

jwt Token을 저장하는 db 입니다.

# redis-cli

비밀번호가 설정된 경우 비밀번호 없이 `redis-cli` 까지는 접속이 됩니다. 하지만 r/w를 하려고 하면 `(error) NOAUTH Authentication required.` 에러가 발생합니다.

```shell
# 비밀번호 없을 때
kubectl exec -it redis -- redis-cli
# 비밀번호 있는 경우
kubectl exec -it redis -- redis-cli
auth {비밀번호}
```
