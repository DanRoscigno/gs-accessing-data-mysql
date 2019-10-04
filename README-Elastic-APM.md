This is a fork of the sample application "Accessing data with MySQL" from Pivotal's getting started
series.  The URL is:

https://spring.io/guides/gs/accessing-data-mysql/

To instrument the application for Elastic APM (https://elastic.co/products/apm ) you can follow these steps:

 - Clone this fork
 - Deploy the Elastic Stack using Elasticsearch Service in Elastic Cloud, or follow the instructions at https://elastic.co/start
 - Follow the instructions in Kibana Home (stylized **K** in upper left corner) -> Add Data -> APM -> Java
    **Note**: The details below are for a Spring app using Maven and mwnc
 - Copy your APM Server URL and token from the cloud console
 - edit the environment file /complete/environment and set the values
 - source the environment file
 - run ./mvnw spring-boot:run
 - Open Kibana and then the APM application in the left nav bar
