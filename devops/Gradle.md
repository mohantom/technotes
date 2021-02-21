Gradle
========

Course: Gradle Fundamentals
## Introduction

- Build by convention
- Groovy DSL
- Supports dependencies
    - Ivy and Maven
- Supports multi-project builds
- Easily customizable
Gvm (groovy environment manager): not Windows friendly

Build.gradle
- Gradle build
This contains tasks, plugins, dependencies, but mostly tasks

```shell script
Apply plugin: 'java'
Task wrapper(type: Wrapper) {
	gradleVerion = '2.6'
}
```


## Gradle basics
### Tasks
Code that Gradle executes
Has a lifecycle
Has properties
Has 'actions'
Has dependencies
Define task
Project.task("task1")
Task("task2")
Task "task3"
Task Task4
Task4.description = "task 4 description".
Task3 << {println "this is task 3"}
Task3 << {println "another closure"}  // append action

	Gradle task3

```shell script
Task task6 {
	Description "task 6"
	dependsOn task5
	doFirst { println "task 6 – first" }
	doLast { println "this is task 6"}
}
Def projectVersion = "2.0"  // define local variable
Ext.projectVersion = "2.0"  // define global variable
```


mustRunAfter, shouldRunAfter
finalizedBy: inverted dependency
Note: tasks must be linked (define dependencies) to make mustRunAfter work
- Gradle --help


Typed tasks

```shell script
task copyImages(type: Copy) {
	exclude 'IMG_0052.jpg', 'IMG_0054.jpg'
    from 'src'
    into 'dest'
}
```

Def contentSpec = 
```shell script
task copyConfig(type: Copy) {
    include 'web.xml'
    from 'src'
    into 'config'
    expand ([
      resourceRefName: 'jdbc/JacketDB'
    ])
}
```


Building a java project
Maven
src/main/java
src/main/resources
src/test/java
src/test/resources
Gradle:

```shell script
sourceSets {
    main {
        java {
          srcDir'src/java'
        }
        resources {
          srcDir'src/resources'
        }
    }
}
```

-	Gradle daemon build
Multiple projects: 
	Settings.gradle, build.gradle

```shell script
Gradle tasks
Gradle run	// run program
Gradle run -Pargs="-f build.gradle -d build.hash" // generate build.hash
``` 

## Dependencies
`Gradle -q dependencies`
 
Compile 'junit:junit:4.12'
```shell script
repositories {
    mavenCentral()  // mavenLocal()
    maven{
      url "http://repo.mycompany.com/maven2"
    }
}

repositories {
  jcenter() // https
  url "http://jcenter.bintray.com/"
}
```


## Test
filtering
```shell script
test {
	filter {
		includeTestsMatching "com.foo.shouldCreateASession"
		includeTestsMatching "*shouldCreateASession"
	}
}
```


Integration test

Wrapper
Provides a specific version of gradle to the project
Continuous integration (CI) is very important, otherwise, at least nightly build.
Team City: build server from Jetbeans
