---
layout: post
title: "Problems with Rails and MySQL on Windows"
description: ""
date: 2012-09-25 15:40
tags: rails mysql windows
comments: true
published: true
---

If you want to create a Rails application with MySQL on Windows, you may face the following problems (which i had). I hope, this
post helps you.

First when starting the application, i got the message "no libmysql.dll found". This can be resolved by copying libmysql.dll
from your MySQL installation to the ${rubyinstallation}/bin directory.

But then i got another problem: "Incorrect MySQL client library version! This gem was compiled for 6.0.0 but the client library is 5.5.27."
I installed all my gems with bundler, so i didn't get a very important message from gem:
<div class="well">
  You've installed the binary version of mysql2.<br/>
  It was built using MySQL Connector/C version 6.0.2.<br/>
  It's recommended to use the exact same version to avoid potential issues.<br/>
<br/>
  At the time of building this gem, the necessary DLL files where available<br/>
  in the following download:<br/>
<br/>
  http://dev.mysql.com/get/Downloads/Connector-C/mysql-connector-c-noinstall-6.0.2-win32.zip/from/pick<br/>
<br/>
  And put lib\libmysql.dll file in your Ruby bin directory, for example C:\Ruby\bin
</div>

The solution is here to download the zip and copy the libmysql.dll file from there. Then the access to MySQL from the Rails
application should work.