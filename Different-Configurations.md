## Hikari - Config

- Zero-overhead Production ready JDBC() Pool. Light-weight.
### Why is Hikari CP so fast while comparing to other JDBC Pool's like tomcat?
- 

```
spring.datasource.hikari.minimumIdle=10
spring.datasource.hikari.maximumPoolSize=50
spring.datasource.hikari.idleTimeout=15000
spring.datasource.hikari.poolName=SpringBootJPAHikariCP
spring.datasource.hikari.maxLifetime=1800000
spring.datasource.hikari.connectionTimeout=15000
spring.datasource.hikari.leak-detection-threshold=20000
```

### maximumPoolSize
- used to define maximum number of DB connections allowed in Connection Pool
- Default is set to 10 by HikariCP
> set is based on maximum number of concurrent requests you DB can handle.

### minimumIdle
- represents the minimum number of Idle Connections that pool maintins.
- Default is same as maximumPoolSize
> if new connections are expensive to create putting this number to a higher value is advised.

### idleTimeout
- defines the maximum amount of run Time (in milli-seconds) that an idle Connection can sit in the Pool after which it is removed.
- Default value is 600,000 ms (10 minutes)
> connections sitting idle for too long can become a resource wastage.

### maxLifetime
- represents the maximum lifetime(in milliseconds) of a connection in the pool.
- Default value sits at 1,800,000 (30 minutes).
> needed to prevent a connection to live indefinitely.

### connectionTimeout
- max time(in milliseconds) a pool waits for a connection to become available before throwing an Exception.
- Default value is 30,000 ms (30 seconds).
