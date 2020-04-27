
## module-web/frontend(react)
+ 참고 프로젝트 : https://github.com/kantega/react-and-spring
+ front-end 프로젝트
+ react로 구성

## module-web(springboot)
+ 클라이언트 웹 프로젝트의 백엔드 서버
+ module-domain 모듈을 의존 받음.

```yaml
spring:

  # Profiles
  profiles:
    active: default
    include:
      - domain

# Embedded server Setting
server:
  port: 9488


---
spring:
  profiles: default

---
spring:
  profiles: production
```

## module-domain
+ JPA 레포지토리에서 사용할 Domain 모델을 선언 하여 관리

### module-domain/src/main/resources/application-domain.yml
```yaml
---
# Spring Setting
spring:
  profiles: default

  # JPA
  jpa:
    database: mysql
    database-platform: org.hibernate.dialect.MySQL5Dialect

# datasource Setting
datasource:
  demo:
    driver-class-name: net.sf.log4jdbc.sql.jdbcapi.DriverSpy
    jdbc-url: {{JDBC-URL}}
    username: {{USERNAME}}
    password: {{password}}
    connection-timeout: 30000
    idle-timeout: 600000
    max-lifetime: 1800000
    minimum-idle: 10 # same initial-size
    maximum-pool-size: 10
    pool-name: Module-Domain
    max-wait: 1000
    initial-size: 10
    connection-init-sql: /* Module-Domain (local) deomo New Connection Pool Create */ SELECT 1

```