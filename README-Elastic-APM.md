This is a fork of the sample application "Accessing data with MySQL" from Pivotal's getting started
series.  The URL is:

https://spring.io/guides/gs/accessing-data-mysql/

To instrument the application for Elastic APM (https://elastic.co/products/apm ) you can follow these steps:

 - Clone this fork
 - Deploy the Elastic Stack using Elasticsearch Service in Elastic Cloud, or follow the instructions at https://elastic.co/start
 - install MySQL
 - Create a DB and user 

    **Note** Connect to mysql as root
    ```
    mysql> create database db_example; -- Creates the new database
    Query OK, 1 row affected (0.01 sec)

    mysql> create user 'springuser'@'%' identified by 'ThePassword'; -- Creates the user
    Query OK, 0 rows affected (0.00 sec)

    mysql> grant all on db_example.* to 'springuser'@'%'; -- Gives all privileges to the new user on the newly created database
    Query OK, 0 rows affected (0.00 sec)
    ```
 - Follow the instructions in Kibana Home (stylized **K** in upper left corner) -> Add Data -> APM -> Java

    **Note**: You can use curl to download the APM agent jar:
    `curl -Lo elastic-apm-agent.jar https://search.maven.org/remotecontent?filepath=co/elastic/apm/elastic-apm-agent/1.10.0/elastic-apm-agent-1.10.0.jar`

 - Copy your APM Server URL and token from the cloud console

    **Note**: The details below are for a Spring app using Maven and mwnc
 - edit the environment file /complete/environment and set the values
 - source the environment file
 - make sure that the MySQL password for user springboot and the value in `complete/src/main/resources/application.properties` match
 - run ./mvnw spring-boot:run
 - Open Kibana and then the APM application in the left nav bar
