## spring-boot-maven-failsafe-integration-test

1- Purpose : Create a new maven profile named "integration-test" to execute integration tests separately from standard maven build process. <br/>
2- Reason : Integration tests are slow and takes longer time to complete when compared to unit tests. <br/>
3- To run integration tests from console run the following maven command : <br/>
NOT : Execute maven command from where the pom.xml is located in the project directory. <br/>
<pre> 
$ mvn clean install -X -P integration-test -Dspring.profiles.active=test <br/>
</pre>
4- failsafe-reports can be accessed from the application directory : "target/failsafe-reports" <br/>

### Tech Stack
Java 11 <br/>
H2 Database Engine <br/>
spring boot <br/>
spring data jpa <br/>
spring web <br/>
hibernate <br/>
logback <br/>
maven <br/>
maven-failsafe-plugin <br/>
junit <br/>
springfox-swagger-ui <br/>
datasource-proxy <br/>
Docker <br/>
<br/>

### Docker build run steps
NOT : Execute docker commands from where the DockerFile is located. <br/>
<pre>
$ docker system prune <br/>
$ docker build . --tag demo  <br/>
$ docker run -p 8080:8080 -e "SPRING_PROFILES_ACTIVE=dev" demo:latest <br/>
</pre>

## API OPERATIONS
### Save store with products successfully to database

Method : HTTP.POST <br/>
URL : http://localhost:8080/customer-info/store/save <br/>

Request : 
<pre>
curl --location --request POST 'http://localhost:8080/customer-info/store/save' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "jeans_store",
  "products": [
    {
      "name": "prod1"
    },
    {
      "name": "prod2"
    },
    {
      "name": "prod3"
    }
  ]
}'
</pre><br/>

Response : 

HTTP response code 200 <br/>
<pre>
{
    "id": 1,
    "name": "jeans_store",
    "products": [
        {
            "id": 1,
            "name": "prod3"
        },
        {
            "id": 2,
            "name": "prod1"
        },
        {
            "id": 3,
            "name": "prod2"
        }
    ]
}
</pre>


### List Store saved to database

Method : HTTP.GET <br/>
URL : http://localhost:8080/customer-info/store/list <br/>

Request : 
<pre>
curl --location --request GET 'http://localhost:8080/customer-info/store/list'
</pre><br/>

Response : 

HTTP response code 200 <br/>
<pre>
[
    {
        "id": 1,
        "name": "jeans_store",
        "products": [
            {
                "id": 1,
                "name": "prod3"
            },
            {
                "id": 2,
                "name": "prod1"
            },
            {
                "id": 3,
                "name": "prod2"
            }
        ]
    }
]
</pre><br/>
