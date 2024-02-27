# using-ec2-rds
- springboot 프로젝트와 EC2 RDS를 연동해서 사용해보자
- 기존의 상황에서는 EC2 리눅스 환경에서 docker를 이용한 데이터베이스 컨테이너화를 진행하여 yml파일에 해당 컨테이너 이름을 넣고 매핑한 포트 번호를 사용해서 스프링 부트 프로젝트가 구동되게 했다.
- 그러나 현재는 AWS에서 제공하는 RDS를 사용해서 진행할 수 있게 했다.

# ⛏Architecture
![image](https://github.com/yeomyaloo/using-ec2-rdb/assets/81970382/61200db8-f7ed-41f0-b850-a9785fe415a3)

# ✏Process
## 1. EC2 환경 생성
- 해당 환경에서는 springboot 프로젝트를 다운로드 받거나 젠킨스를 이용해 빌드 배포 작업을 진행해 jar 파일을 최종적으로 담고 있을 환경입니다.
## 2. RDS 생성
- AWS에서 제공하는 Mysql RDS를 생성한 후 제공되는 엔드 포인트를 이용해서 디비버 등에 사용합니다.
## 3. springboot 프로젝트 설정
```
server:
  port: 8085

spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    password: <RDS 생성 시 설정한 비밀번호>
    url: jdbc:mysql://<여기에 RDS 엔드포인트 작성>:3306/fisa?useSSL=false&allowPublicKeyRetrieval=true
    username: <RDS 생성 시 설정한 유저 아이디>
  jpa:
    database: mysql
    database-platform: org.hibernate.dialect.MySQL8Dialect
    generate-ddl: true
    hibernate:
      ddl-auto: none
    show-sql: true

```
