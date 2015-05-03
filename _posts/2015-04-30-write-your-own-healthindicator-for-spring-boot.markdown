---
layout: post
title: "Write Your Own HealthIndicator for Spring Boot"
date: 2015-04-30T09:14:18+02:00
published: false
---

Spring Boot provides a very convenient module for all things of monitoring, called _Spring Boot Actuator_.
You can include this module in your Spring Boot application with the following Maven coordinates:

`
<dependency>
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-actuator</artifactId>  
    <version>1.2.3.RELEASE</version>  
</dependency>
`

The actuator module provides various REST endpoints, where you can query different runtime aspects of your application.
For the whole list, please see the Spring Boot documentation.

One particular endpoint is quite helpful for automatic monitoring: The health endpoint is in the default configuration 
reachable under _{your.application.url}/health_ and provides you with a short status overview (default UP and DOWN).

But the information published through this endpoint can easily be extended to provide any custom information you want.
For this you just have to implement the interface **org.springframework.boot.actuate.health.HealthIndicator**. The interface provides the method _health()_ with a return type 
of **Health**.