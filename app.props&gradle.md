# Gradle :

## gradle.build file  

#### 1. Build Script Block :
```
buildscript {
    dependencies {
        classpath files('libs/abc-0.0.8-SNAPSHOT.jar')
    }
    repositories {
        mavenLocal()
        mavenCentral()
    }
}
```
- Configures gradle's own class-path
- If the gradle require any external JAR's you put them here

#### 2. Plugins Block :
```
plugins {
    id 'java' // enables java compilation and packagin tasks
    id 'org.springframework.boot' version '3.3.6' // Enables Spring-Boot gradle plugin
    id 'io.spring.dependency-management' version '1.1.7' // consistent version managment across dependencies
    id 'jacoco'
}
```

#### 3. Jacoco Test Reports : 
```
tasks.jacocoTestReport {
	outputs.upToDateWhen { false }
	dependsOn test
	reports {
		xml.required.set(true)
		xml.outputLocation.set(file("build/abc/jacocoTestReport.xml"))
		html.required.set(true)
	}
}
```
- Always generate report
- standard enterprise reporting

#### 4. Java ToolChain :
```
java {
	toolchain {
		languageVersion = JavaLanguageVersion.of(21)
	}
}
```
- it ensure that the Java version used is always 21 even if the developer has older version installed

#### 5. Configurations :
```
configurations {
	compileOnly {
		extendsFrom annotationProcessor
	}
}
```
- ensure lombok works correctly as lombok is an annotationProcessor
- must only run in compile time & not included in the final JAR

#### 6. Repositories :
```
repositories {
    mavenCentral()
    mavenLocal()
}
```
- Dependency lookup Order 1. Local repository and 2. Maven Central

#### 7. Dependencies Section :
```
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-undertow' // undertow server replacing Tomcat
	implementation 'org.springframework.boot:spring-boot-starter-amqp' // RabbitMQ messaging
	implementation 'org.springframework.boot:spring-boot-starter-validation' // Jakarta Validation
	implementation 'org.springframework.boot:spring-boot-starter-actuator' // Actuator for health endPoints
	modules {
		module("org.springframework.boot:spring-boot-starter-tomcat") {
			replacedBy("org.springframework.boot:spring-boot-starter-undertow")
		}
	}
  // replaces tomcat inbuilt servlet with undertow
}
```
- 























