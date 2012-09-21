--- 
layout: post
name: remote-debugging-mit-eclipse-und-tomcat_17
title: Remote Debugging mit Eclipse und Tomcat
time: 2011-02-17 00:15:00 +01:00
comments: true
published: false
---
Tomcat wird mit der Datei "catalina.bat" bzw. "catalina.sh" und den Argumenten "jdpa start" gestartet. Damit wird auf Port 8000 ein Socket bereitgestellt. In Eclipse muss nun eine Debug Configuration vom Typ "Remote Java Application" angelegt werden. Die Standardeinstellungen können dabei so belassen werden.<br />Zum Debuggen muss vorher das Projekt wie gewohnt deployed werden, danach kann in Eclipse der Debug-Modus mit der entsprechenden Konfiguration aufgerufen werden. Das weitere Vorgehen entspricht dem lokalen Debuggen (Breakpoints, Variablen etc.)
