Maven
======

Course: Maven Fundamentals
Ant is maybe easier to learn, but it really is only beneficial as a scripting tool.
Maven: build and management tool
 
 
## cli
```shell script
<packaging> jar </packaging>
<scope> test </scope>
```

- Mvn clean
- Mvn compile	// compiles files, create .class files
- Mvn package    // create .jar file
- Mvn install 	// package, then install it in local repo
- Mvn deploy	// install, then copy to a corporate directory

Structure

    Src/main/java
    Src/main/resources
    Src/target
    Src/pom.xml

## Pom.xml
1.	Project
2.	Dependencies
a.	If 1.0-SNAPSHOT: in compile, it will check if new code is available
3.	Build: plugins, directory structure
<finalName> foo </finalName>
4.	Repositories: central maven repo

## Transitive dependencies
Scope: 
- Compile: default, available everywhere
- Provided: going to be provided where it is deployed
- Runtime: not needed for compilation, but needed for execution
Test:
System: 

## repository
Local repo: c:\Users\<yourname>\.m2\repository
http://repo.maven.apache.org/maven2
Corporate repository: Nexus, antifactory
Repo.springsource.org/libs-snapshot  (not available from Maven)
 

Snapshots, milestones, release candidate, release policies

## Plugins
Clean, compile, test, package, install, deploy
Phases
	Validate, compile, test, package, integration-test, verify, install, deploy
http://maven.apache.org/plugins/maven-compiler-plugin
default to Java1.5.
 

- Jar plugin
- Source plugin: to attach source code to jar
- Attach source code in verify phase (will not do it <= package phase)
- Javadoc plugin (similar to source plugin), tied to package phase, but often overridden to a later phase
 

Effective POM
All the info, settings

