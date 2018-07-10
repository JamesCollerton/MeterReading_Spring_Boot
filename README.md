[![Build Status](https://travis-ci.com/JamesCollerton/MeterReading_Spring_Boot.svg?branch=master)](https://travis-ci.com/JamesCollerton/MeterReading_Spring_Boot)

# Meter Reading API #

This is a meter reading API I did as a project to learn API design in Spring Boot, it can accept and present readings at various URIs. The tech stack includes:

* Spring Boot: Used to implement project.
* Spring Data: Handles DB interaction.
* Lombok: Simplifies data objects.
* H2: Embedded database for production and testing.
* Swagger: API documentation.
* Aspect Orientated Programming: Used for logging.
* Travis CI: Builds and testing.

## Design ##

### Accepting Meter Readings ###

This accepts meter readings of the schema:

```
 {
     "customerId": "identifier123",
     "serialNumber": "27263927192",
     "mpxn": "14582749",
     "read": [
         {"type": "ANYTIME", "registerId": "387373", "value": "2729"},
         {"type": "NIGHT", "registerId": "387373", "value": "2892"}
     ],
     "readDate": "2017-11-20T16:19:48+00:00Z"
 }
```

to `POST` requests at URI `/meter-read`.

### Presenting Meter Readings ###

This will present meter readings from the URI `/meter-read` given a `GET` request, and takes two parameters:

* Customer Id: The customer Id to search for.
* Serial Number: The serial number to search for.

It will then return all meter readings currently stored in the database matching those criteria.

## AOP Logging ##

Aspect orientated logging has been employed in order to log all method calls in the program. Additionally extra logging has been set up around certain calls with a timer, the idea being that this would be written up into Elasticsearch for analysis of process times in Kibana.

## H2 DB ##

An H2 DB was used for development, testing and as this is a prototype, for production. It can be accessed at `http://localhost:8080/h2-console` using database `jdbc:h2:mem:testdb`.

## Swagger ##

Swagger was used to document and for trying out the API. On running the application it can be accessed using `http://localhost:8080/swagger-ui.html`.

## Travis CI ##

Travis CI was used as a build and deployment tool (despite not deploying anywhere). It will automatically build and test the project on each update.
