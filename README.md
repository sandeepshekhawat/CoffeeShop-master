# Coffeshop Locations REST API service 

This project is to create a RESTful API services for loading Coffee Shop locations from a CSV file (id, name, address, latitude, longitude) and support CRUD operations, find a nearest Coffee Shop location given a valid address   

## Getting Started

These instructions will get you a copy of the project, compile and run on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software, and how to install them

```
 Java 1.8+
 Apache Maven 3.3.3 and above
 Rest API Client (example: Google Chrome Browser extension Postman) or curl utility installed
```

```
Download JDK from Oracle website http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html
Download maven from http://maven.apache.org/download.cgi
To install mvnw  use the command  mvn -N io.takari:maven:wrapper
```

### Installing

Follow the instructions to download the source code, compile and run

After compilation, the packaged file is a self executable jar file, with all dependencies

```
git clone https://github.com/kishanraov/CoffeeShop.git
cd CoffeeShop
mvn clean package (or mvnw clean package) 
java  -jar target/coffeeshop-service-0.0.1-SNAPSHOT.jar --apikey=provide a google geocode api key  --csvfile=full path of locations.csv

(Note: If you do not have an api key, pass any random string (example: abc), the application still works, but the FindNearest api will not work)

The CSV file gets uploaded to cache. Whatever data you add or update will not be available once you restart the server. There is no persistence for the data.

The Tomcat web server runs on port 8080.
```


## Running the tests

  * To test the web server is up and running, run the following command.

```
  curl -XGET http://localhost:8080/hello
```
  If you get a response, the installation is complete.

  * To get a coffee shop with id=1, use the command: 

```
  curl -XGET http://localhost:8080/CoffeeShop/1
```

  * To create a new coffee shop location, use the command: 

```
  curl -H "Content-Type: application/json" -X POST "http://localhost:8080/CoffeeShop/" -d '{ "name": "My favorite Coffee Shop", "address": "San Francisco, CA","latitude":37.7749295,"longitude":-122.4194155 }'
```

  Note the response on the command line

```
  {"id":"57"} 
```

  * To update the above coffee shop name, use the command: 

```
  curl -H "Content-Type: application/json" -XPUT "http://localhost:8080/CoffeeShop/57" -d '{ "name": "The best Coffee Shop", "address": "San Francisco, CA","latitude":37.7749295,"longitude":-122.4194155 }'
```
  Observe the  name attribute has been modified in the output.

  * To delete the above Coffee Shop, use the command:  

```
  curl -H "Content-Type: application/json" -XDELETE "http://localhost:8080/CoffeeShop/57"
```

  Observe the response 

```
  {"status":"success"}
```

  * To find a nearest Coffee Shop by providing the from address, use the command: 

```
  curl -G "http://localhost:8080/CoffeeShop/FindNearest" --data-urlencode "address=535 Mission St., San Francisco, CA"
```

  Observe the response 

```
  {"name":"Red Door Coffee"}
``` 

## Built With

* [Eclipse](http://www.eclipse.org/downloads/) - The IDE used
* [Maven](https://maven.apache.org/) - Dependency Management
* [Google](https://github.com/googlemaps/google-maps-services-java/) - Google Geo Coding Api


## Authors

* ** Kishan Rao Verukonda** - *Initial work* 


## License

This project require license to run

