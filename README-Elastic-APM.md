This is a fork of the sample application "Accessing data with MySQL" from Pivotal's getting started
series.  The URL is:

https://spring.io/guides/gs/accessing-data-mysql/

To instrument the application for Elastic APM (https://elastic.co/products/apm ) you can follow these steps:

## Setup on Debian 9
```
sudo apt install default-jre
sudo apt install default-jdk
sudo apt install maven
sudo apt install git
git clone https://github.com/DanRoscigno/gs-accessing-data-mysql.git
```

## Setup MySQL
```
wget https://dev.mysql.com/get/mysql-apt-config_0.8.10-1_all.deb
sudo dpkg -i mysql-apt-config*
sudo apt update
sudo apt install mysql-server
sudo mysql
```

## Within MySQL
```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 2                                                                
Server version: 10.1.41-MariaDB-0+deb9u1 Debian 9.9                                            
                                                                                               
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.                           
                                                                                               
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.                 
                                                                                               
MariaDB [(none)]> create database db_example;                                                  
Query OK, 1 row affected (0.00 sec)
                                                                                               
MariaDB [(none)]> create user 'springuser'@'%' identified by 'ThePassword';                    
Query OK, 0 rows affected (0.00 sec)
                                                                                               
MariaDB [(none)]> grant all on db_example.* to 'springuser'@'%';                               
Query OK, 0 rows affected (0.00 sec)
                                                                                               
MariaDB [(none)]> quit                                                                         
Bye     
```

## Configure the APM environment vars
```
cd gs-accessing-data-mysql/complete
vi environment 
```

## Download the APM agent JAR
```
curl -Lo elastic-apm-agent.jar https://search.maven.org/remotecontent?filepath=co/elastic/apm/elastic-apm-agent/1.10.0/elastic-apm-agent-1.10.0.jar
```

### The environment vars come directly from the Add APM page in Kibana
Open up Kibana Home and then click on Add APM
Switch to the Java tab
Copy the APM Server URL and Secret Token.  Specify the Application name yourself:
```
export ELASTIC_APM_SERVER_URL=https://yadayadayada.apm.us-central1.gcp.cloud.es.io:443

export ELASTIC_APM_SECRET_TOKEN=AbcdefGHIjklabc

export ELASTIC_APM_SERVICE_NAME=Spring-MySQL
```

## Start the application
```
source ./environment 
./mvnw spring-boot:run
```

## Exercise the app

Open a new terminal and access the API
```
curl localhost:8080/demo/add -d name=First -d email=dan@example.com
```
