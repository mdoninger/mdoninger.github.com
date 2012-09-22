---
layout: page
title: Debug an enterprise app with GWT in JBoss and IntelliJ IDEA
date: '2012-08-31'
description:
group: javaee
---

Based on the great article from the Guys from [4th Line](http://4thline.org/articles/JBoss%20AS7%20plays%20nice%20with%20GWT%20and%20IntelliJ.html), which saved me some hours of try and error,
this is a small tutorial, how you can configure IntelliJ IDEA and JBoss to deploy your Enterprise application and run the GWT dev mode to debug the GWT part of that application.

# Application structure #

My sample application has some EJB modules and the GWT module, which are packaged as an EAR file.
