--- 
layout: post
name: tomcat-unter-ubuntu-und-socket-bind
title: "Tomcat unter Ubuntu und \"Socket bind failed: [98] Address already in use\""
time: 2011-01-01 23:08:00 +01:00
comments: true
published: true
---
Ich hatte ewig Probleme, Tomcat 6 unter Ubuntu mit aktiviertem SSL (unter Verwendung von OpenSSL und APR) zum Laufen zu bringen. 
Die Fehlermeldungen im Log lauteten immer "java.lang.Exception: Socket bind failed: [98] Address already in use". Problemlösungen 
in den verschiedensten Blogs und Foren halfen nicht (Deaktivierung von IPv6 etc.).  
Letztendlich lag das Problem darin, dass das ServerKey-File für mein SSL-Zertifikat im Unterordner /etc/ssl/private lag, der nur von root gelesen werden kann. Da Tomcat ja nicht 
als root ausgeführt wird, konnte dieser letztlich das Key-File nicht lesen. Abhilfe hat das Verschieben in einen lesbaren Ordner gebracht.

