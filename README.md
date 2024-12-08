# Adondevamos

++ Note: This project is still WIP ++

Adondevamos is a website to create a list of places (itineraty) to share with a couple of friends and then they can vote of with place they want to go and share all data as a trip to help people to create their own itineray version of others 

* [High Level Architecture](#high-level-architecture)
* [Programming Language](#programming-language)
* [Application Framework](#application-framework)
* [Build](#build)
* [Continuous Integration (CI)](#continuous-integration)
* [Continuous Delivery (CD)](#continuous-delivery)
* [Continuous Deployment (CD)](#continuous-deployment)
* [Infrastructure As Code](#infrastructure-as-code)
* [Deploymemt](#deploymemt)
    * [Docker](#docker)
    * [Kubernetes](#kubernetes)
* [API Documentation](#api-documentation)
* [Projects](#projects)
* [Documentation of project](#projects)
* [Artifacts](#artifacts)
* [APIS](#apis)
* [Documentation of project](#projects)

### <a name="high-level-architecture"></a>High Level Architecture


### <a name="programming-language"></a>Programming Language

- Java 17

### <a name="application-framework"></a>Application Framework

- Spring Boot 2.0+
### <a name="projects"></a>Projects
This website is composed by some individual systems created by myself `@moysakuma` 

`Adondevamos.io`

DNS name of this project, public and production stage of this project

`Adondevamos.io/dev`

DNS name of this project to test, public and dev stage of this project

`Adondevamosweb`

HTML project, interfaces, interacts with users, html project, TBD

`Adondevamosback`

A rest full api which manage all APIS calls and microservice to run and manage `Adondevamos.io`

`Adondevamosbd`

A database connected to `Adondevamosback`, all necesary info about website is here.


### <a name="apis"></a>APIS

- /AkumaNo/Trip

Api who manage info about trips

`MSTrips.jar`

A java springboot project to manage trips info

`TripsBD`

A bd project to manage trips info


- /AkumaNo/Users

Api who manage info about users

`MSUsers.jar`

A java springboot project to manage users info

`UsersBD`

A bd project to manage users info


- /AkumaNo/Site

Api who manage info about sites

`MSSite.jar`

A java springboot project to manage sites info

`SiteBD`

A bd project to manage sites info


- /AkumaNo/Place

Api who manage info about places

`MSPlace.jar`

A java springboot project to manage place info

`PlaceBD`

A bd project to manage place info


### <a name="Endpoints"></a>Endpoints
`/AkumaNo/Place`

A bd project to manage place info

### <a name="build"></a>Build

Both Maven and Gradle are supported. However, Maven is currently the main build system used for this project to manage the release.

__Maven__  
Maven wrapper is used so that no need to install Maven on your machine beforehand. Lets maven wrapper take care of maven.

__Gradle__  
Just like Maven, Gradle offers the Gradle wrapper is used so that no need to install Gradle on your machine beforehand.

### <a name="continous-integration"></a>Continuous Integration (CI)

See `Jenkinsfile` which is a config file for defining build settings on Jenkins 2.0+ (with the use of Pipelines).

Only Jenkins 2.0+ is supported.

### <a name="continous-delivery"></a>Continuous Delivery (CD)

Every commit/merge is a RC (Release Candidate).

See `Jenkinsfile`'s section on Continous Delivery.

### <a name="continous-deployment"></a>Continuous Deployment (CD)

Mainly it is about the automated deployment from a testing environment (Staging) onto live Production.
Normally, or historically, this would be a manual process done by the Operations Team (Ops).

See `Jenkinsfile`'s section on Continous Deployment.

CD is facilitated by the shell script `deploy.sh` which you can use and edit to define the steps and behaviours for
doing the deployment. In Jenkins pipeline, we have a sanity check stage which governs or acts as a gate prior for the software
to be deloyed onto Production. (Artifact/Pipeline promotion).

### <a name="infrastructure-as-code"></a>Infrastructure As Code

To implement IAC, Terraform is used. You can place your terraform files in the `terraform` directory.
This template assumes the project will be deployed onto the Cloud or to any other infrastructure that is supported by Terraform.

If deploying to a bare metal physical server machine or to Virtual Machines, one might decide to use a configuration management tool such as Ansible, Puppet, or Chef a like to automate the provisioning of the infrastructure instead. Currently this template does not offer support for this. As normally, these deployment methods normally reside in a separate source code repository hence this subject matter is out of the scope of this template project.

### <a name="deploymemt"></a>Deploymemt

#### <a name="docker"></a>Docker

See `Dockerfile` in the root of the project directory.

Building a Docker container

```bash
./mvnw clean package
```

or execute Docker directly:

```bash
docker build -t microservices-template:1.0.0-SNAPSHOT .
```

#### <a name="kubernetes"></a>Kubernetes

Using an container orchestration framework to manage the containers. This template project is opinionated towards Kubernetes. It is to note that other container orchestration platforms exists (Docker Swarm, Nomad with Consul, Apache Mesos on DC/OS etc).

```bash
kubectl apply -f deployment/microservices-template.yml
```

### <a name="api-documentation"></a>API Documentation

Use of Swagger to document our microservice's API REST endpoints.

Access Swagger on:

```
http://{microservices-template-service-url}:{port}/swagger-ui.html
```


`Version: Alpha`