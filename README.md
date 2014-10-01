# Welcome to the Monitoring and Alerting Client project
The [SmarterApp](http://smarterapp.org) Monitoring and Alerting Client aggregates Logging, Metrics, and Notifications. Log entries and notifications can be searched and managed through a central UI.

## License ##
This project is licensed under the [AIR Open Source License v1.0](http://www.smarterapp.org/documents/American_Institutes_for_Research_Open_Source_Software_License.pdf).

## Getting Involved ##
We would be happy to receive feedback on its capabilities, problems, or future enhancements:

* For general questions or discussions, please use the [Forum](http://forum.opentestsystem.org/viewforum.php?f=6).
* Use the **Issues** link to file bugs or enhancement requests.
* Feel free to **Fork** this project and develop your changes!

### Client Modules
There are three modules that make up the client:

* The Client Interfaces module contains the interface classes for the client, AOP advice and point cuts, and bootstrap initialization.
* The Null Client module is a client implementation that sends all messages to the local logging subsystem (SLF4J).
* The Integrated Client sends all messages to the advertised REST endpoints from the REST module.

In order to use one of the client implementations:

* Add the Maven dependencies to the POM of the project that is using Monitoring and Alerting.

```
<dependency>
	<groupId>org.opentestsystem.shared</groupId>
	<artifactId>monitoring-alerting.client-null-impl</artifactId>
	<version>${sb11-mna-client.version}</version>
</dependency>

<dependency>
	<groupId>org.opentestsystem.shared</groupId>
	<artifactId>monitoring-alerting.client</artifactId>
	<version> ${sb11-mna-client.version}</version>
</dependency>
```

* Add a context initializer class name to the web.xml.

```
<context-param>
    <param-name>contextInitializerClasses</param-name>
    <param-value>org.opentestsystem.shared.mna.client.listener.ClientSpringConfigurator</param-value>
</context-param>
```

* Add environment variables to application server startup.
	* ```-Dspring.profiles.active="mna.client.integration"```
		* Use ```mna.client.integration``` to use the fully integrated client
		* Use ```mna.client.null``` to use the null client

* logback.xml: MNA is built to work with logback configuration. So if your project is using log4j.xml or any other logging configuration, switch it to logback.xml and include ```logback-included-common-config.xml``` inside the logback configuration as shown below:
```
<configuration scan="true">
	<property scope="local" name="app.context.name" value="permission" />
	<property scope="local" name="app.base.package.name" value="org.opentestsystem.shared.shared.permissions" />
	<property scope="local" name="mna.appender.active" value="true" />
	<include resource="logback-included-common-config.xml" />
</configuration>
```

The PROGMAN setting “mna.logger.level” is used to control what is logged to the Monitoring and Alterting system.  For instance, if the logging level is set to “WARN,” log events at level WARN and ERROR are added to the log.  INFO, DEBUG, and TRACE events are not added to the log.  The default setting is “ERROR.”

Logging Levels:

* ALL - Turn on all logging levels
* TRACE
* DEBUG
* INFO
* WARN
* ERROR
* OFF - Turn off logging

## Build
These are the steps that should be taken in order to build all of the Monitoring and Alerting related artifacts.

### Pre-Dependencies
* Mongo 2.0 or higher
* Tomcat 6 or higher
* Maven (mvn) version 3.X or higher installed
* Java 7
* Access to sb11-shared-build repository
* Access to sb11-shared-code repository
* Access to sb11-rest-api-generator repository
* Access to sb11-program-management repository
* Access to sb11-monitoring-alerting repository

### Build order

* sb11-shared-build
* sb11-shared-code
* sb11-rest-api-generator
* sb11-monitoring-alerting-client

Additional instructions are located in the [repository](external_release_docs/installation).