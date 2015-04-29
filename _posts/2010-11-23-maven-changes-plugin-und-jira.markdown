--- 
layout: post
name: maven-changes-plugin-und-jira
title: maven-changes-plugin und Jira-Announcements
time: 2010-11-23 22:10:00 +01:00
comments: true
published: false
---
Möchte man mit maven-changes-plugin automatisch Jira-Announcements erzeugen und per Mail versenden lassen, könnte es sein, dass man den Fehler "401" beim Downloaden der Jira-Issues erhält. Dies ist dann der Fall, wenn man sich in der Jira-Instanz nicht mit den Maven-Konfigurationsparametern jiraUser und jiraPassword, sondern webUser und webPassword anmelden muss (bei meinem Arbeitgeber der Fall, da die Jira-User gegen LDAP authentifiziert werden und die Authentifizierung vom Application Server übernommen wird). Desweiteren werden Parameter die unter "filter" angegeben werden, ignoriert, sodass maven-changes-plugin nicht die Query benutzt, die man eigentlich wollte.  
Das Goal announcement-generate unterstützt diese Authentifizierung und die filter-Konfiguration noch nicht, wie ich in <a href="http://jira.codehaus.org/browse/MCHANGES-206">diesem Bug</a> bereits beschrieben habe. Dort habe ich auch bereits einen Patch angehängt, evtl. wird er in den Trunk aufgenommen und beim nächsten Release dann veröffentlicht.  
  
  
*Update*: Mittlerweile wurde das Release 2.4 veröffentlicht, in dem auch die oben beschriebenen Bugfixes vorhanden sind.
