---
title: "Maven Plugin for DDL Generation"
layout: default
---

Introduction
------------

DDL Generator is a Maven plugin to generate DDL file from a Maven project using JPA/Hibernate. It has been created as a (very) partial replacement of the [Maven Hibernate3 Plugin](http://mojo.codehaus.org/maven-hibernate3/hibernate3-maven-plugin/) which is not working under Hibernate 4.


Features
--------

* Simple generation of DDL file as part of the Maven build processs.
* Support for entities dispatched on multiple PU by embedding [MultiConfigAwarePersistenceUnitManager](http://bitlingo.com/tag/jpa/).
* Support for any Hibernate dialect or naming strategy.


Usage
-----

### Goals

The plugin has one goal: `generate`. It takes the following mandatory parameters:

* `ddlFile`: destination ddl file.
* `dialect`: full class name of the dialect to use for the generation.
* `persistenceUnitName`: name of the persistence unit.

And the following optional parameters:

* `defaultSchema`: the schema to use if an explicit schema naming is required in the DDL file.
* `namingStrategy`: the class name of the naming strategy to use if the default one is not ok.
* `persistenceXmlLocations`: a list of persistence unit definition files.
* `useNewGenerator`: set to `true` is the new hibernate id generator should be used.


### Configuration

The following configuration needs to be inserted in the `pom.xml` file:

{% highlight xml %}
<plugin>
    <groupId>net.ggtools.maven</groupId>
    <artifactId>ddlgenerator-maven-plugin</artifactId>
    <version>0.1</version>
    <executions>
        <execution>
            <goals>
                <goal>generate</goal>
            </goals>
            <phase>prepare-package</phase>
            <configuration>
                <ddlFile>${project.build.directory}/sql/schema.sql</ddlFile>
                <!--<defaultSchema></defaultSchema>-->
                <dialect>org.hibernate.dialect.H2Dialect</dialect>
                <!--<namingStrategy></namingStrategy>-->
                <persistenceUnitName>MultiPU</persistenceUnitName>
                <persistenceXmlLocations>
                    <param>classpath*:/META-INF/persistence.xml</param>
                    <param>classpath*:/META-INF/persistence-*.xml</param>
                </persistenceXmlLocations>
            </configuration>
        </execution>
    </executions>
</plugin>
{% endhighlight %}

Source and Issue tracking
-------------------------

The source repository and issue tracking is hosted on [GitHub](https://github.com/ggtools/DDLGenerator).


History
-------

* **0.1**: First public release.
