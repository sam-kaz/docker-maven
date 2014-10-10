docker-maven
============

Docker image with Maven, following Docker official images.


# Supported tags and respective Dockerfile links

* 3.2.3, 3.2, 3
* 3.2.3-onbuild, 3.2-onbuild, 3-onbuild

# What is Maven?

Apache Maven is a software project management and comprehension tool.
Based on the concept of a project object model (POM),
Maven can manage a project's build,
reporting and documentation from a central piece of information.


# How to use this image

## Create a Dockerfile in your Maven project

    FROM csanchez/maven:3.2-onbuild
    CMD ["do-something-with-built-packages"]

Put this file in the root of your project, next to the pom.xml.

This image includes multiple ONBUILD triggers which should be all you need to bootstrap most applications. The build will `COPY . /usr/src/app` and `RUN mvn install`.

You can then build and run the image:

    docker build -t my-maven .
    docker run -it --name my-maven-script my-maven


## Run a single Maven command

For many simple projects, you may find it inconvenient to write a complete `Dockerfile`.
In such cases, you can run a Maven project by using the Maven Docker image directly,
passing any Maven goals to `docker run`:

    docker run -it --rm --name my-maven-project -v "$(pwd)":/usr/src/mymaven -w /usr/src/mymaven csanchez/maven:3.2 clean install
