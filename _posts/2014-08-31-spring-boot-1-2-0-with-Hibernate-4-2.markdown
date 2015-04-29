---
layout: post
title: "Spring Boot 1.2.0 with Hibernate 4.2.x"
description: ""
date: 2014-08-31 21:35
tags: spring boot hibernate autoconfiguration
comments: true
published: true
---

With the current changes in the Spring Boot 1.2.0 snapshot version, the autoconfiguration for Hibernate depends on classes
and packages which were changed in Hibernate 4.3. So with Hibernate 4.2 at the moment you will get NoClassDefFoundErrors
when using the Hibernate autoconfiguration (and, when my pull request is accepted, the autoconfiguration will be disabled
for Hibernate 4.2).

As a workaround, you can either create manually the whole Hibernate and JPA configuration beans, or copy and modify the source of the class
org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaAutoConfiguration.
The code, which relies on Hibernate 4.3 specific classes is at the moment solely contained in the method customizeVendorProperties:

{% highlight java %}
@Override
protected void customizeVendorProperties(Map<String, Object> vendorProperties) {
    super.customizeVendorProperties(vendorProperties);
    if (!vendorProperties.containsKey(JTA_PLATFORM)) {
        JtaTransactionManager jtaTransactionManager = getJtaTransactionManager();
        if (jtaTransactionManager != null) {
            vendorProperties.put(JTA_PLATFORM, new SpringJtaPlatform(
                    jtaTransactionManager));
        }
        else {
            vendorProperties.put(JTA_PLATFORM, NoJtaPlatform.INSTANCE);
        }
    }
}
{% endhighlight %}

If you have configured the JTA platform with the property spring.jpa.properties.hibernate.transaction.jta.platform, you can just
remove the complete method. Otherwise, create an instance of the JTA platform you need and put it into the vendorProperties map (but don't use
the class SpringJtaPlatform from Spring Boot, because it also depends on Hibernate 4.3)