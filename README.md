# Remoting JMX

A project to provide the integration required to expose JMX over Remoting 3 connections.

Issues with this library are tracked in the following Jira location: -

  https://issues.jboss.org/browse/REMJMX

The following branches are currently in use:

 * 3.0.x - Shared by JBoss EAP 7.4 and JBoss EAP 8.0
 * 3.1.x - Used by WildFly until WildFly 37, used to maintain JBoss EAP 8.0
 * 3.2.x - Upstream development and maintenance branch

When submitting PRs please submit to most relevant branch only,
as maintenance releases are prepared we will also merge to the
upstream branches.

## Building

This project requires Java 17 as a minimum as well as Apache
Maven and can be built with the following command:

    mvn install



