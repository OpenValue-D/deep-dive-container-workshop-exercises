# Description

This exercise shall demonstrate how to build your own jre distribution for running your application

# Exercises

## Task 1

Create an own jre

* Run `docker run azul/zulu-openjdk:21.0.4-jdk java --list-modules` to see all possible modules of a jdk
* Check Dockerfile and replace `ADD_MODULES_HERE` with `java.base,java.net.http,java.sql`
* Build image with `docker build -t my-jre .`
* Run `docker run --rm my-jre --list-modules` to see the modules included now in our own image
* Run `dive my-jre` to analyze the size and content of the image 

## Task 2

Create a jre based on a spring boot application

* Check Dockerfile.spring line 18 to see how a modules list is generated based on the spring boot app
* Check line 21 how this module list is used to build the jre
* Run `docker build -t mini-demo -f Dockerfile.spring .` to build the spring boot application
* Run `dive mini-demo` to analyze the size and content of the image ( ~85MB)
* Run `docker run --rm mini-demo` to see the application starting
* Ctrl-C to stop the application again
* Run `docker run --rm mini-demo --list-modules` to see the list of modules in the built jre