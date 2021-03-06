# Camunda Platform
Camunda Platform is an open-source workflow and decision automation platform. Camunda Platform ships with tools for creating workflow and decision models, operating deployed models in production, and allowing users to execute workflow tasks assigned to them. To know more, visit [Camunda Site](https://camunda.com/)
<br />
By default, Camunda comes with an embedded database called H2. Camunda supports major databases through JDBC drivers, namely Oracle, DB2, MySQL, MariaDB and PostgreSQL. However, in this project we have kept the scope limited to H2 and PostgreSQL.<br />
Camunda creates a bunch of tables on startup. Refer to [Camunda Database Schema](https://docs.camunda.org/manual/7.16/user-guide/process-engine/database/database-schema/) to know more.

## Pre-requisites
The following dependencies need to be present and configured in your system:
* Java 11 or higher
* Maven
* Java IDE (such as Eclipse), if you want to modify the code further
* PostgreSQL (local or container-based)
* Docker [Optional], if PostgreSQL is container-based

## How to Build and Run
Follow these steps:
1. Clone [this repo](https://github.com/darkhorse1998/Camunda.git). It is suggested that you clone the entire repo and then move on to individual modules.
2. Open the cloned repo and change directory into the camunda-engine by ```cd camunda-platform-setup```
3. Build a JAR by ```mvn clean package```
4. Depending on your database usage preferrence, run the JAR using coressponding profile. By default, H2 database will be used. Checkout the **Configuration** section for more details.
5. By default, camunda-engine will run on port 8080. Make sure the port is not pre-occupied and is functioning properly. You can also tweak the port settings later.

## Configurations
* Database: To configure Camunda Platform according to the desired database, use the following inside the `camunda-platform-setup` directory:
    * H2-database (default): ```java -jar target/camunda-engine-1.0.0-SNAPSHOT.jar --spring.profiles.active=h2``` or simply ```java -jar target/camunda-engine-1.0.0-SNAPSHOT.jar```
    * PosgresSQL: ```java -jar target/camunda-engine-1.0.0-SNAPSHOT.jar --spring.profiles.active=postgres```<br />
**Note**: By default, the properties have been configured to look for PostgreSQL on ```localhost:5432```. If you have configured PostgreSQL differently (say, cloud deployment) or in some different port, you need to execute the **custom-postgres** profile:<br />

```
java -jar target/camunda-engine-1.0.0-SNAPSHOT.jar --spring.profiles.active=custom-postgres --spring.datasource.url=jdbc:postgresql://<postgres-host>:<postgres-port>/<database-name> --spring.datasource.username=<username> --spring.datasource.password=<password>
```
Replace:<br />
**postgres-host** with the hostname on which postgres is running<br />
**postgres-port** with the port on which postgres is running<br />
**database-name** with the database name in PostgreSQL in which Camunda tables need to be created<br />
**username** with the username of the PostgreSQL user<br />
**password** with the password of the PostgreSQL user

* Server Port: Server port can be configured using the ```--server.port=<port>``` command.<br />
Example: ```java -jar target/camunda-engine-1.0.0-SNAPSHOT.jar --server.port=8081```
<br />

Endnote: The JAR name may vary if you have customised the build in the pom.xml