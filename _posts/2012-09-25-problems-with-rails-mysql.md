---
layout: post
title: "Problems with Rails and MySQL on Windows"
description: ""
date: 2012-09-25 15:40
category: 
tags: rails mysql windows
comments:true
published: true
---
{% include JB/setup %}

If you want to create a Rails application with MySQL on Windows, you may face the following problems (which i had). I hope, this
post helps you.

First when starting the application, i got the message "no libmysql.dll found". This can be resolved by copying libmysql.dll
from your MySQL installation to the ${rubyinstallation}/bin directory.

But then i got another problem: "Incorrect MySQL client library version! This gem was compiled for 6.0.0 but the client library is 5.5.27."
I installed all my gems with bundler, so i didn't get a very important message from gem:

  >You've installed the binary version of mysql2.
  >It was built using MySQL Connector/C version 6.0.2.
  >It's recommended to use the exact same version to avoid potential issues.
  >
  >At the time of building this gem, the necessary DLL files where available
  >in the following download:
  >
  >http://dev.mysql.com/get/Downloads/Connector-C/mysql-connector-c-noinstall-6.0.2-win32.zip/from/pick
  >
  >And put lib\libmysql.dll file in your Ruby bin directory, for example C:\Ruby\bin
