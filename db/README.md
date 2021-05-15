# Hi

DB 관련 Object를 관리합니다.  
Storage 관련 Object는 해당 디렉터리에서 관리하지 않으며 mount만 진행합니다.

# 종류

## mysql-deployment

qa 환경에서 사용되는 mysql db 입니다.  
Azure File Storage를 사용합니다.

## mysql-replicated-stateful

prod 환경에서 사용되는 mysql db 입니다.  
`master`, `slave` 이루어진 mysql replication 입니다.  
Azure Disk Storage를 사용합니다.

## redis

jwt Token을 저장하는 db 입니다.
