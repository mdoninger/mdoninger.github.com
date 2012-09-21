--- 
layout: post
title: Distributed transactions with Spring
published: false
---
This is the first article of my blog series "Distributed transactions with Spring and Atomikos TransactionEssentials". 
In this series i will explain with some examples, how to get distributed transactions working in a Java SE application 
with Spring and Atomikos TransactionEssentials.

## Basics about distributed transactions

A distributed transaction spans a couple of resources, such as databases or message queues. Sun developed the Java Transaction API to provide 
a framework for such transactions. The JTA is part of the Java Enterprise specification, so all Application Servers can handle distributed transactions.
If you want to use JTA in a Java SE application, you need a transaction manager, which implements the JTA. 
Examples are [Bitronix Transaction Manager](http://docs.codehaus.org/display/BTM/Home), [Atomikos TransactionEssentials](http://www.atomikos.com/) 
or [JOTM](http://jotm.ow2.org).

In this example i will use Atomikos TransactionEssentials.

## Databases

For distributed transactions to work, the JDBC drivers have to provide an XA-compliant datasource implementation. XA is a standard defined by The Open Group
to standardize distributed transaction processing. Atomikos provided a list of [compatible databases](http://www.atomikos.com/Documentation/SupportedJdbcVendors) 
on their websites. Although they don't mention Apache Derby there, Derby provides an XADataSource which works with Atomikos and distributed transactions, so i 
use this database for my test projects.
