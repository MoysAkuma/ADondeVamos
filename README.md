# Adondevamos

++ Note: This project is still WIP ++

Adondevamos is a website to create a list of places (itineraty) to share with a couple of friends and then they can vote of with place they want to go and share all data as a trip to help people to create their own itineray version of others 

* [High Level Architecture](#high-level-architecture)
* [Programming Language](#programming-language)
* [Application Framework](#application-framework)
* [Projects](#projects)
    * [ADondeVamos.io](#hosting)
    * [ADondeVamos.web](#web)
    * [ADondeVamos.back](#back)
    * [AkumaNo](#akumano)
        * [Trips](#trips)
        * [Users](#users)
        * [Places](#places)
        * [Sites](#sites)
* [APIS](#apis)
* [Entities](#Entities)
* [Endpoints](#Endpoints)
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
- React
- Nodejs

### <a name="projects"></a>Projects
This website is composed by some individual systems created by myself `@moysakuma` 

#### <a name="hosting"></a>Adondevamos.io

DNS name of this project, public and production stage of this project


#### <a name="web"></a>Adondevamos.web

HTML project, interfaces, interacts with users, html project, TBD

#### <a name="back"></a>Adondevamos.back

A rest full api which manage all APIS calls and microservice to run and manage 

#### <a name="bd"></a>Adondevamosbd

A database connected to `Adondevamos.back`, all necesary info about website is here.

#### <a name="akumano"></a>AkumaNo
An api gateway to access to several services

#### <a name="trips"></a>Trip

Api who manage info about trips
    
Path: '/trip/'

Complete Path:  'https://{HOST}/experience/trips/'

- MSTrips.jar

    A java springboot project to manage trips info

- TripsBD

    A bd project to manage trips info

#### <a name="users"></a>Users

Api who manage info about users

- MSUsers.jar
    
    A java springboot project to manage users info

- UsersBD

    A bd project to manage users info


#### <a name="site"></a>Site

Api who manage info about sites

- MSSite.jar

    A java springboot project to manage sites info

- SiteBD

    A bd project to manage sites info


#### <a name="place"></a>Place

Api who manage info about places

- MSPlace.jar

    A java springboot project to manage place info

- PlaceBD

    A bd project to manage place info

### <a name="Entities"></a>Entities
- Trip
    
    Origin: AkumaNoTrip
    Use in: [Adondevamos.io](#Adondevamos.io), [AkumaNoTrip](#AkumaNoTrip)
```
    {
        //number, unique id of trip inside this system and akumasoft
        "TripID":""
        //varchar(150), 
         ,"Name" : "string"
         //varchar(500), description about this trip
        ,"Description" : "string"
        //array object list, all dates of trip´s info
        ,"Dates" : [
        //json object, info about date, see `DateObject`
            ref Trip.Dates
            ]
        //array object list, all Ubication
        ,"Ubication" : [
        //json object, info about Ubication, see `UbicationObject`
            ref Trip.Ubications 
        ]
        //boolean
        ,"IsInternational":false,
        //array object list, all itinerary of trip´s info
        ,"Itinerary" : [
        //json object, Place info 
            {
                //number, unique id of trip inside this system and akumasoft,
                "PlaceID":0
                //array object list, all dates of place
                ,"Dates" : [
                //json object, info about date, see `DateObject`
                            {
                                //varchar(150) id objet type of Dates see `DateObject.DateTypeName`
                                "DateTypeName":"string"
                                //array object list, all captured date info 
                                ,{ 
                                    //Date in format DDMMYYYY
                                    "InitialDate":"00:00:00 00:00:00"
                                    //Date in format DDMMYYYY 
                                    ,"FinalDate":"00:00:00 00:00:00" 
                                } 
                            }
                ]
                //varchar(150)
                ,"PlaceDescription":"string"
                //json object, staticst info about votes and preferences and recomendations 
                "Staticts": {
                    //number, unique id of place statics data inside this system and akumasoft
                    "TypeID":0
                    //varchar(150), unique id of place statics data inside this system and akumasoft
                    ,"TypeIDName":"string"
                    //number, value statics data inside this system and akumasoft
                    ,"Value":0
                }
            }
        ],
        //array object list, list of users
        "MemberList":[
            ref Trip.Member
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
                                ,"Records": [
                                    ref Trip.Dates
                                ]
                            }
                ]
                
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

- User
    
    Origin: AkumaNoUser
    Use in: [Adondevamos.io](#Adondevamos.io), [AkumaNoTrip](#AkumaNoTrip)
```
    {
        //number, unique id of user inside this system and akumasoft
        "UserID":""
        //string, unique id of user inside this system and akumasoft
        ,"Tag" : "string"
        //string, Email of the user
        ,"Email" : "string"
        //string, first name of user
        ,"FirstName" : "string"
        //string, second name of user
        ,"SecondName" : "string"
        //string, last name of user
        ,"LastName" : "string"
        //string, second last name of user
        ,"SecondLastName" : "string"
        //json object array, list of social network tags
        ,"SocialNetWorkList": [
            {
                "Name":"string"
                ,"Tag":"string"
            }
        ]
        ,"Address":""
        ,"Ubication": ref User.Ubication
        ,"ContacInfo":{
            "Phone":"12345678910"
        }
    }
``` 
- Place
    
    Origin: Place
    Use in: [Adondevamos.io](#Adondevamos.io), [AkumaNoTrip](#AkumaNoTrip)
    ``` 
    {
        "PlaceID":0
        ,"Name":"string"
        ,"Descripcion":"string"
        ,FacilityList:[
            "Name":"string"
            ,"FacilityID":0
            ,"Logo":"string"
        ]

    }
    ``` 
- Sites
    
    Origin: AkumaNoSite
    Use in:
    ``` 
    {
        "SiteID":0
        ,"Name":"string"
        ,"Active":1
    }
    ``` 
- 

### <a name="Endpoints"></a>Endpoints
Microservices

MSTrip.jar
- '/CreateTrip'

    `Method POST` to create trip in system

    Request Body
    ```
    {
        ref Entities.Trip
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

- '/ReadTrip/{TripID}'

     `Method GET` to get all info about a trip

    Request Param Values
    
    ```
    TripID:long
    ```
    
    Response Body
    
    
    ```
    {
        "Info": ref Entities.Trip,
        "CreationInfo": ref Entities.CreationInfo
    }
    ```
- '/UpdateTrip/{TripID}'

    `Method PUT` to update trip info

    Request Param Values
    ```
    TripID:long
    ```
    Request Body
    ```
    {
        ref Entities.Trip,
        "UpdateInfo": ref Entities.UpdateInfo
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

- '/DeleteTrip/{TripID}'

     `Method DELETE` to delete trip

    Request Param Values
    
    ```
    TripID:long
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
    
    Request Param Values

    ```
    TripID:long
    ```
    
    Response Body
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Result":"A trip was found!"
            //TripID:long
            ,"UniqueKey":0 
            ,Data:{
               "Result": ref Entities.Trip
            }
        }
    }
    ```

- '/SearchTrip'

    `Method POST` to get a list of trips

    Request Body
    ```
    {
        "Filters" : {
            "TripID":null, //number, Filter search by this value
            ,"PlaceID":null, //number, Filter search by this value
            ,"InitialDate":null, //string, Filter search by this value
            ,"FinalDate":null, //string, Filter search by this value
            ,"CountryID":null, //number, Filter search by this value
            ,"StateID":null, //number, Filter search by this value
            ,"CityID":null, //number, Filter search by this value
        }
    }
    ```

    Response Body
    
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Result":"Search result success!"
            ,Data:{
               "Result": [ref Entities.Trip]
            }
        }
    }
    ```

MSUser.jar

- '/CreateUser'

    `Method POST` to create user


    Request Body
    ```
    {
        ref Entities.User
    }
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New User was Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/ReadUser/{UserID}'
    
    `Method GET` to read info about a user

    Request Param Values

    ```
    UserID:long
    ```

    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of read success"
            ,"Result":"User info was found with given id"
            ,"UniqueKey":0
            ,Data:{
               "Result": ref Entities.UserID
            }
        }
    }
    ```

- '/UpdateUser'
 `Method POST` to update user info


    Request Body
    ```
    {
        ref Entities.User
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"User was updated sucessfully"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/DeleteUser'
 `Method DELETE` to delete an user


    Request Param Values

    ```
    UserID:long
    ```
    
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of deletion success"
            ,"Result":"A user was deleted"
            ,"UniqueKey":0
        }
    }
    ```
- '/SearchTrip'
 
    `Method POST` to search trips with given filters


    Request Body
    ```
    {
        "Filters" : {
            "TripID":null, //number, Filter search by this value
            ,"PlaceID":null, //number, Filter search by this value
            ,"InitialDate":null, //string, Filter search by this value
            ,"FinalDate":null, //string, Filter search by this value
            ,"CountryID":null, //number, Filter search by this value
            ,"StateID":null, //number, Filter search by this value
            ,"CityID":null, //number, Filter search by this value
        }
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of searching success"
            ,"UniqueKey":0
            ,"Data": [ref Entities.Trips]
        }
    }
    ```

MSSites.jar

- '/CreateSite'

    `Method POST` to create a site

    Request Body
    ```
    {
        ref Entities.Site    
    }
    ```

   Response Body `200`

    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New site was Created"
            ,"UniqueKey":0
        }
    }
    ```
- '/ReadSite/{SiteID}'
 
    `Method GET` to read info about a site


    Request Param Values

    ```
    SiteID:long
    ```

   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
            ,"Result":"New site was Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/UpdateSite'
    
    `Method PUT` to update site info

    Request Body
    ```
    {
        ref Entities.Site
    }
    ```

    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of update success"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/DeleteSite/{SiteID}'
 
    `Method DELETE` to delete a site

    Request Param Values

    ```
    SiteID:long
    ```
   Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse": {
            "Message":"Process of deletion success"
        }
    }
    ```

MSPlaces.jar

- '/CreatePlace'
 
    `Method POST` to create trip

    Request Body
    ```
    {
        ref Entities.Place
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"New place was Created"
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
        ref Entities.Place
    }
    ```
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"Process of Creation success"
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
        ref Entities.Place
    }
    ```
    
    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"New place was Created"
            ,"UniqueKey":0
            ,"CompleteUrl":"string"
        }
    }
    ```
- '/DeletePlace/{PlaceID}'

    `Method Delete` to delete place

    Request Param Values

    ```
    PlaceID:long
    ```

    Response Body `200`
    ```
    {
        "StatusCode":200,
        "BodyResponse":{
            "Message":"New place was Created"
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