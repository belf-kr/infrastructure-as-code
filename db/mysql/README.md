# Hi

mysql 관련 object를 관리합니다.

# 종류

## deployment

qa 환경에서 사용되는 mysql db 입니다.  
Azure File Storage를 사용합니다.

## replicated-stateful

prod 환경에서 사용되는 mysql db 입니다.  
`master`, `slave` 이루어진 mysql replication 입니다.  
Azure Disk Storage를 사용합니다.