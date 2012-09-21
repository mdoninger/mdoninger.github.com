---
layout: post
title: "Write Groovy scripts for Jenkins with code completion"
date: 2011-11-07 17:30
comments: true
categories:
published: false
---

In the Jenkins instance of my company we have now over 80 jobs. Sometimes i have to configure the same thing in many jobs, and the easiest thing for that is a Groovy script.
To execute Groovy scripts, you just have to go to "Manage Jenkins" and then "Script console". But there is one problem with the script console: Do you always remember all methods of all classes in Jenkins and its plugins? I do not, and i don't always want to read all Javadocs. So my thought was, how can i use the features like code completion in my favourite IDE, Eclipse, to write the Groovy scripts.  
All you need is Eclipse with the m2e and the Groovy plugin. Now create a new Maven project (i called mine "jenkinsgroovy") and add at least jenkins-core and the plugins you need as dependency in the pom.xml. Your pom.xml should look like this to start:

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	 <modelVersion>4.0.0</modelVersion>
	 <groupId>jenkinsgroovy</groupId>
	 <artifactId>jenkinsgroovy</artifactId>
	 <version>0.0.1-SNAPSHOT</version>
	 
	 <dependencies>
	  <dependency>
	   <groupId>org.jenkins-ci.main</groupId>
	   <artifactId>jenkins-core</artifactId>
	   <version>1.437</version>
	  </dependency>
	  <dependency>
	   <groupId>org.jenkins-ci.main</groupId>
	   <artifactId>maven-plugin</artifactId>
	   <version>1.437</version>
	  </dependency>
	 </dependencies>
	</project>

To add the Groovy compiler and libraries to that project, you have to make a right click on the project, choose "Configure" and then "Convert to Groovy project". Now you can simply create Groovy scripts (i created them in the folder src/main/java), and for example refer to Jenkins.instance with code completion.
Everytime you need classes of new plugins, just add the plugins in your pom.xml and all dependencies are automatically downloaded.
