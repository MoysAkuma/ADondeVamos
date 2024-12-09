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
/AkumaNo/Trip
- '/CreateTrip'

    `Method POST` to create trip in system

    Request Body
    ```
    {
        "Name" : "string"//string, name of the trip
         ,"Description" : "string"//string, description of the trip
         ,"Dates" : List<{"Atribute":"JsonObject"}>//list of dates, view `Dates`
         "Name" : "string"//varchar(150), unique id of trip inside this system and akumasoft
        ,"Description" : "string"//varchar(500), description about this trip
        //array object list, all dates of trip´s info
        ,"Dates" : [
        //json object, info about date, see `DateObject`
                    {
                        "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                        //array object list, all captured date info 
                        ,{ 
                            "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                            ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                        } 
        }]
        //array object list, all itinerary of trip´s info
        ,"Itinerary" : [
        //json object, Place info 
            {
                "PlaceID":0//number, unique id of trip inside this system and akumasoft,
                //array object list, all dates of place
                ,"Dates" : [
                //json object, info about date, see `DateObject`
                            {
                                "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                                //array object list, all captured date info 
                                ,{ 
                                    "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                    ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                } 
                            }
                ]
                ,"PlaceDescription":"string"//varchar(150)
                //json object, staticst info about votes and preferences and recomendations 
                "Staticts": {
                    "TypeID":0//number, unique id of place statics data inside this system and akumasoft
                    ,"TypeIDName":"string"//varchar(150), unique id of place statics data inside this system and akumasoft
                    ,"Value":0//number, value statics data inside this system and akumasoft
                }
            }
        ],
        //array object list, list of users
        "MemberList":[
            {
                "UserID":0 //number, unique id of trip inside this system and akumasoft
                ,"UserTag":"string" //
                ,"Role":"string"
            }
        ]
    }
    ```
    
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```

    Response Unexpected
    
    ```
    {
        "StatusCode":500,
        "BodyResponse":{
            "Message":"Internal Server Error"
            ,"Result":"string"
            ,"Track":[]
        }
    }
    ```


- '/ReadTrip'

     `Method POST` to read all info about a trip

    Request Body
    
    ```
    {
        
    }
    ```
    
    Response Body
    
    
    ```
    {
       "TripID":""//number, unique id of trip inside this system and akumasoft
       ,"Name" : "string"//varchar(150), unique id of trip inside this system and akumasoft
        ,"Description" : "string"//string, description of the trip
        ,"Dates" : List<{"Atribute":"JsonObject"}>//list of dates, view `Dates`
        ,"Description" : "string"//varchar(500), description about this trip
        //array object list, all dates of trip´s info
        ,"Dates" : [
        //json object, info about date, see `DateObject`
            {
                "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                //array object list, all captured date info 
                ,{ 
                    "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                    ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                } 
            }
        ]
        //array object list, all itinerary of trip´s info
        ,"Itinerary" : [
        //json object, Place info 
            {
                "PlaceID":0//number, unique id of trip inside this system and akumasoft,
                //array object list, all dates of place
                ,"Dates" : [
                //json object, info about date, see `DateObject`
                            {
                                "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                                //array object list, all captured date info 
                                ,{ 
                                    "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                    ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                } 
                            }
                ]
                ,"PlaceDescription":"string"//varchar(150)
                //json object, staticst info about votes and preferences and recomendations 
                "Staticts": {
                    "TypeID":0//number, unique id of place statics data inside this system and akumasoft
                    ,"TypeIDName":"string"//varchar(150), unique id of place statics data inside this system and akumasoft
                    ,"Value":0//number, value statics data inside this system and akumasoft
                }
            }
        ],
        //array object list, list of users
        "MemberList":[
            {
                "UserID":0 //number, unique id of trip inside this system and akumasoft
                ,"UserTag":"string" //
                ,"Role":"string"
            }
        ]
    }
    ```
- '/UpdateTrip'

    `Method POST` to create trip

    Request Body
    ```
    {
        "TripID":""//number, unique id of trip inside this system and akumasoft
       ,"Name" : "string"//varchar(150), unique id of trip inside this system and akumasoft
        ,"Description" : "string"//string, description of the trip
        ,"Dates" : List<{"Atribute":"JsonObject"}>//list of dates, view `Dates`
        ,"Description" : "string"//varchar(500), description about this trip
        //array object list, all dates of trip´s info
        ,"Dates" : [
        //json object, info about date, see `DateObject`
            {
                "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                //array object list, all captured date info 
                ,{ 
                    "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                    ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                } 
            }
        ]
        //array object list, all itinerary of trip´s info
        ,"Itinerary" : [
        //json object, Place info 
            {
                "PlaceID":0//number, unique id of trip inside this system and akumasoft,
                //array object list, all dates of place
                ,"Dates" : [
                //json object, info about date, see `DateObject`
                            {
                                "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                                //array object list, all captured date info 
                                ,{ 
                                    "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                    ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                } 
                            }
                ]
                ,"PlaceDescription":"string"//varchar(150)
                //json object, staticst info about votes and preferences and recomendations 
                "Staticts": {
                    "TypeID":0//number, unique id of place statics data inside this system and akumasoft
                    ,"TypeIDName":"string"//varchar(150), unique id of place statics data inside this system and akumasoft
                    ,"Value":0//number, value statics data inside this system and akumasoft
                }
            }
        ],
        //array object list, list of users
        "MemberList":[
            {
                "UserID":0 //number, unique id of trip inside this system and akumasoft
                ,"UserTag":"string" //
                ,"Role":"string"
            }
        ]
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```

- '/DeleteTrip'

     `Method POST` to create trip

    Request Body
    ```
    {
        
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/GetTrip/{`TripID`}'
 `Method GET` to search all private information about a trip to show 

    Request Body
    ```

    ```
    Response Body
    ```
    {
        "TripID" : 0,//long, unique id of trip inside this system and akumasoft
        "Name" : "string"//varchar(150), unique id of trip inside this system and akumasoft
        ,"Description" : "string"//varchar(500), description about this trip
        //array object list, all dates of trip´s info
        ,"Dates" : [
        //json object, info about date, see `DateObject`
                    {
                        "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                        //array object list, all captured date info 
                        ,{ 
                            "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                            ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                        } 
        }]
        //array object list, all itinerary of trip´s info
        ,"Itinerary" : [
        //json object, Place info 
            {
                "PlaceID":0//number, unique id of trip inside this system and akumasoft,
                //array object list, all dates of place
                ,"Dates" : [
                //json object, info about date, see `DateObject`
                            {
                                "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                                //array object list, all captured date info 
                                ,{ 
                                    "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                    ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                } 
                            }
                ]
                ,"PlaceDescription":"string"//varchar(150)
                //json object, staticst info about votes and preferences and recomendations 
                "Staticts": {
                    "TypeID":0//number, unique id of place statics data inside this system and akumasoft
                    ,"TypeIDName":"string"//varchar(150), unique id of place statics data inside this system and akumasoft
                    ,"Value":0//number, value statics data inside this system and akumasoft
                }
            }
        ]
        //array object list, all Comments of trip
        ,"Comments" : [
        //json object, comment info 
            {
                "CommentID":0//number, unique id of comment inside this system and akumasoft
                ,"CommentObjectID":0//number
                ,"CommentObjectTypeID":0//number
                ,"CommentObjectSubTypeID":0//number
                ,"CommentObjectSubTypeTypeID":0//number
                ,"Parent":null//number, parent CommentID of comment see `CommentObject.Parent`
                //array object list, all dates of place
                ,"Content" : [
                //json object, info about date, see `DateObject`
                            {
                                "Title":"string"//varchar(150) titule of comment see `CommentObject.Title`
                                "Body":"string"//varchar(500) titule of comment see `CommentObject.Body`
                                //array object list, all captured date info 
                                ,{ 
                                    "CreatedDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                    ,"LastUpdateDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                }
                            }
                ]
                ,"PlaceDescription":"string"//varchar(150)
                //json object, staticst info about votes and preferences and recomendations 
                "Staticts": {
                    "TypeID":0//number, unique id of place statics data inside this system and akumasoft
                    ,"TypeIDName":"string"//varchar(150), unique id of place statics data inside this system and akumasoft
                    ,"Value":0//number, value statics data inside this system and akumasoft
                }
            }
        ]
    }
    ```

- '/SearchTrip'
 `Method POST` to create trip

    Request Body
    ```
    {
        "Filters" : {
            "TripID":null, //number, Filter search by this value
            ,"PlaceID":null, //number, Filter search by this value
            ,"InitialDate":null, //string, Filter search by this value
            ,"FinalDate":null, //string, Filter search by this value
            ,"CountryID":null, //number, Filter search by this value
        }
    }
    ```
    Response Body
    ```
    {
        [
            {
                "TripID" : 0,//long, unique id of trip inside this system and akumasoft
                "Name" : "string"//varchar(150), unique id of trip inside this system and akumasoft
                ,"Description" : "string"//varchar(500), description about this trip
                //array object list, all dates of trip´s info
                ,"Dates" : [
                //json object, info about date, see `DateObject`
                            {
                                "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                                //array object list, all captured date info 
                                ,{ 
                                    "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                    ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                } 
                }]
                //array object list, all itinerary of trip´s info
                ,"Itinerary" : [
                //json object, Place info 
                    {
                        "PlaceID":0//number, unique id of trip inside this system and akumasoft,
                        //array object list, all dates of place
                        ,"Dates" : [
                        //json object, info about date, see `DateObject`
                                    {
                                        "DateTypeName":"string"//varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                                        //array object list, all captured date info 
                                        ,{ 
                                            "InitialDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                            ,"FinalDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                        } 
                                    }
                        ]
                        ,"PlaceDescription":"string"//varchar(150)
                        //json object, staticst info about votes and preferences and recomendations 
                        "Staticts": {
                            "TypeID":0//number, unique id of place statics data inside this system and akumasoft
                            ,"TypeIDName":"string"//varchar(150), unique id of place statics data inside this system and akumasoft
                            ,"Value":0//number, value statics data inside this system and akumasoft
                        }
                    }
                ]
                //array object list, all Comments of trip
                ,"Comments" : [
                //json object, comment info 
                    {
                        "CommentID":0//number, unique id of comment inside this system and akumasoft
                        ,"CommentObjectID":0//number
                        ,"CommentObjectTypeID":0//number
                        ,"CommentObjectSubTypeID":0//number
                        ,"CommentObjectSubTypeTypeID":0//number
                        ,"Parent":null//number, parent CommentID of comment see `CommentObject.Parent`
                        //array object list, all dates of place
                        ,"Content" : [
                        //json object, info about date, see `DateObject`
                                    {
                                        "Title":"string"//varchar(150) titule of comment see `CommentObject.Title`
                                        "Body":"string"//varchar(500) titule of comment see `CommentObject.Body`
                                        //array object list, all captured date info 
                                        ,{ 
                                            "CreatedDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                            ,"LastUpdateDate":"00:00:00 00:00:00" //Date in format DDMMYYYY
                                        }
                                    }
                        ]
                        ,"PlaceDescription":"string"//varchar(150)
                        //json object, staticst info about votes and preferences and recomendations 
                        "Staticts": {
                            "TypeID":0//number, unique id of place statics data inside this system and akumasoft
                            ,"TypeIDName":"string"//varchar(150), unique id of place statics data inside this system and akumasoft
                            ,"Value":0//number, value statics data inside this system and akumasoft
                        }
                    }
                ]
        ]
    }
    }
    ```

`/AkumaNo/User`

- '/CreateUser'
 `Method POST` to create trip


    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/ReadUser'
 `Method POST` to create trip

    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/UpdateUser'
 `Method POST` to create trip


    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/DeleteUser'
 `Method POST` to create trip


    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/SearchTrip'
 `Method POST` to create trip


    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```

`/AkumaNo/Site`

- '/CreateSite'
 `Method POST` to create trip


    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/ReadSite'
 `Method POST` to create trip


    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/ReadSite'
 `Method POST` to create trip

    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/UpdateSite'
 `Method POST` to create trip


    Request Body
    ```
    {
        ,"atribute" : "property"//type, desc
    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/DeleteSite'
 `Method POST` to create trip

    Request Body
    ```
    {

    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```

`/AkumaNo/Place`

- '/CreatePlace'
 `Method POST` to create trip

    Request Body
    ```
    {

    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/ReadPlace'
 `Method POST` to create trip

    Request Body
    ```
    {

    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/UpdatePlace'
 `Method POST` to create trip

    Request Body
    ```
    {

    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/DeletePlace'
 `Method POST` to create trip

    Request Body
    ```
    {

    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New Trip Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```

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