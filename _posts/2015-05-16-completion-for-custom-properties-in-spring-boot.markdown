---
layout: post
title: "Code completion for custom properties in Spring Boot"
date: 2015-05-16T12:00:00+02:00
published: true
---

All three major IDEs (IntelliJ IDEA, Eclipse and Netbeans) provide either plugins or built-in features for code completion
in application.properties files in a Spring Boot project:

![](/images/codecompletionproperties2.png)

Besides completion, you also see, that all properties are typed (and validated), and if present a Javadoc is shown.

Fortunately this feature can also be used for custom defined properties. There are 2 prerequisites for that:

- You have to use classes annotated with `@ConfigurationProperties` which holds fields that are mapped to your properties
- You have to add the `spring-boot-configuration-processor` plugin as dependency to your project

## Part 1: `@ConfigurationProperties` ##

Spring Boot provides the annotation `@ConfigurationProperties` which can be used on classes, that hold the property values
at runtime.


    @ConfigurationProperties(prefix = "hornetq_health")
    @Getter
    @Setter
    public class HornetQHealthConfigurationProperties {

        /**
         * Threshold per queue name.
         */
        private Map<String, Integer> thresholds;

        private Integer count;

        private List<String> list;
    }

The property name is generated from the prefix attribute plus the field names, in this case there are three properties available:

- hornetq_health.thresholds
- hornetq_health.count
- hornetq_health.list

Javadoc must be on the field, not on the getter or setter to take effect.

## Part 2: Configure the `spring-boot-configuration-processor` plugin

To activate the plugin, just add it as optional dependency in your POM:

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-configuration-processor</artifactId>
        <optional>true</optional>
    </dependency>

If you recompile (or make) the project, the plugin will create a JSON file in the path *target/classes/META-INF/spring-configuration-metadata-json*.
The file contains a list of all properties with type and Javadoc information and will be evaluated by the IDE plugins.

![](/images/codecompletionproperties1.png)

## Enable mapping of the configuration properties ##

There are two ways to enable the population of the configuration properties classes

- Add the annotation `@EnableConfigurationProperties` on one of your configuration classes
- Add the annotation `(@EnableConfigurationProperties(HornetQHealthConfigurationProperties.class)` on the bean, where you inject the configuration properties class (replace the class name attribute with your own properties class)

## Download the example ##

You can clone the repository with an example from my Github account: [https://github.com/mdoninger/spring-boot-health-indicator-sample.git](https://github.com/mdoninger/spring-boot-health-indicator-sample.git)