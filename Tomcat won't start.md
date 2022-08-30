[[Classic Errors]]

# Tomccat won't start

## Tags:
#job, #errors

---

## Log

```
`31 09:08:02,859  WARN  [main] o.s.b.w.s.c.AnnotationConfigServletWebServerApplicationContext - Exception encountered during context initialization - cancelling refresh attempt: org.springframework.context.ApplicationContextException: Unable to start web server; nested exception is org.springframework.boot.web.server.WebServerException: Unable to start embedded Tomcat`

`2022-03-31 09:08:02,870  INFO  [main] c.h.h.HazelcastCacheRegionFactory - Shutting down HazelcastCacheRegionFactory`

`2022-03-31 09:08:02,870  WARN  [main] c.h.h.i.IHazelcastInstanceFactory - hibernate.cache.hazelcast.shutdown_on_session_factory_close property is set to 'false'. Leaving current HazelcastInstance active! (Warning: Do not disable Hazelcast hazelcast.shutdownhook.enabled property!)`

`2022-03-31 09:08:02,891  INFO  [main] com.hazelcast.core.LifecycleService - [127.0.0.1]:5701 [GoGlobalLocal] [3.12] [127.0.0.1]:5701 is SHUTTING_DOWN`

`2022-03-31 09:08:02,905  INFO  [hz.GoGlobal.cached.thread-6] c.h.i.p.impl.MigrationManager - [127.0.0.1]:5701 [GoGlobalLocal] [3.12] Shutdown request of Member [127.0.0.1]:5701 - d5999e3b-64f5-4118-91c1-a79b186a2566 this is handled`

`2022-03-31 09:08:02,916  INFO  [main] com.hazelcast.instance.Node - [127.0.0.1]:5701 [GoGlobalLocal] [3.12] Shutting down connection manager...`

`2022-03-31 09:08:02,918  INFO  [main] com.hazelcast.instance.Node - [127.0.0.1]:5701 [GoGlobalLocal] [3.12] Shutting down node engine...`

`2022-03-31 09:08:02,942  INFO  [main] com.hazelcast.instance.NodeExtension - [127.0.0.1]:5701 [GoGlobalLocal] [3.12] Destroying node NodeExtension.`

`2022-03-31 09:08:02,942  INFO  [main] com.hazelcast.instance.Node - [127.0.0.1]:5701 [GoGlobalLocal] [3.12] Hazelcast Shutdown is completed in 41 ms.`

`2022-03-31 09:08:02,942  INFO  [main] com.hazelcast.core.LifecycleService - [127.0.0.1]:5701 [GoGlobalLocal] [3.12] [127.0.0.1]:5701 is SHUTDOWN`

`2022-03-31 09:08:03,067  ERROR [main] o.s.boot.SpringApplication - Application run failed`

`org.springframework.context.ApplicationContextException: Unable to start web server; nested exception is org.springframework.boot.web.server.WebServerException: Unable to start embedded Tomcat`

`at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.onRefresh(ServletWebServerApplicationContext.java:162)`

`at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:577)`

`at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:144)`

`at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:782)`

`at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:774)`

`at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:439)`

`at org.springframework.boot.SpringApplication.run(SpringApplication.java:339)`

`at org.springframework.boot.builder.SpringApplicationBuilder.run(SpringApplicationBuilder.java:144)`

`at com.gp.GoGlobalApplication.main(GoGlobalApplication.java:29)`

`Caused by: org.springframework.boot.web.server.WebServerException: Unable to start embedded Tomcat`

`at org.springframework.boot.web.embedded.tomcat.TomcatWebServer.initialize(TomcatWebServer.java:142)`

`at org.springframework.boot.web.embedded.tomcat.TomcatWebServer.<init>(TomcatWebServer.java:104)`

`at org.springframework.boot.web.embedded.tomcat.TomcatServletWebServerFactory.getTomcatWebServer(TomcatServletWebServerFactory.java:450)`

`at org.springframework.boot.web.embedded.tomcat.TomcatServletWebServerFactory.getWebServer(TomcatServletWebServerFactory.java:199)`

`at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.createWebServer(ServletWebServerApplicationContext.java:181)`

`at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.onRefresh(ServletWebServerApplicationContext.java:159)`

`... 8 common frames omitted`
```
