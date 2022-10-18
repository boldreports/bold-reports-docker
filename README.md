<a href="https://www.boldreports.com"><img alt="boldreports" width="400" src="https://www.boldreports.com/wp-content/uploads/2019/08/bold-reports-logo.svg"></a>
<br/>
<br/>

# What is Bold Reports

Bold Reports Enterprise Reporting is a business intelligence report management tool, built by Syncfusion for creating, managing, and distributing pixel-perfect paginated RDL reports behind your organization’s firewall.

Enterprise Reporting help us to analyse, explain and report business information in our day-to-day life.

# Docker compose:<br/>
* Bold Reports in multiple container image.

## Start multiple container Bold Reports with `docker-compose`
Bold Reports now comes with multiple images for each of the services in it to run on docker-compose which is mainly for the purpose of production environment to scale services within Bold Reports.  Please refer to [this guide](docs/multiple-container.md) to get know about the multiple images and compose details to deploy Bold Reports in an advanced docker compose environment.



## Environment variables for configuring `Application startup` in backend using `docker-compose`
The below Environment variables are optional. If not provided a manual Application Startup configuration is needed.

| Name                          |Required| Description   | 
| -------------                 |----------| ------------- |
|`BOLD_SERVICES_HOSTING_ENVIRONMENT`|Yes|docker|
|`BOLD_SERVICES_DB_TYPE`|Yes|Type of database server can be used for configuring the Bold Reports.<br/><br />The following DB types are accepted:<br />1. mssql – Microsoft SQL Server<br />2. postgresql – PostgreSQL Server<br />3. mysql – MySQL Server|
|`BOLD_SERVICES_DB_HOST`|Yes|Name of the Database Server|
|`BOLD_SERVICES_DB_PORT`|No|The system will use the following default port numbers based on the database server type.<br />PostgrSQL – 5234<br />MySQL -3306<br /><br />Please specify the port number for your database server if it is configured on a different port.<br /><br />For MS SQL Server, this parameter is not necessary.|
|`BOLD_SERVICES_DB_USER`|Yes|Username for the database server|
|`BOLD_SERVICES_DB_PASSWORD`|Yes|The database user's password|
|`BOLD_SERVICES_DB_NAME`|No|If the database name is not specified, the system will create a new database called bold services.<br /><br />If you specify a database name, it should already exist on the server.|
|`BOLD_SERVICES_POSTGRESQL_MAINTENANCE_DB`|No|For PostgreSQL DB Servers, this is an optional parameter.<br />The system will use the database name `postgres` by default.<br />If your database server uses a different default database, please provide it here.|
|`BOLD_SERVICES_DB_ADDITIONAL_PARAMETERS`|No|If your database server requires additional connection string parameters, include them here.<br /><br />Connection string parameters can be found in the official document.<br />My SQL: https://dev.mysql.com/doc/connector-net/en/connector-net-8-0-connection-options.html<br />PostgreSQL: https://www.npgsql.org/doc/connection-string-parameters.html<br />MS SQL: https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring<br /><br /><b>Note:</b> A semicolon(;) should be used to separate multiple parameters.|
|`BOLD_SERVICES_USER_EMAIL`|Yes|It should be a valid email.|
|`BOLD_SERVICES_USER_PASSWORD`|Yes|It should meet our password requirements.|


## Environment variables used in id-ums 
Add environment variables in id-ums service for application startup in backend.If we use the below environment variables, we don't need manual Application Startup Configuration.


```sh
    id-ums:
    container_name: id_ums_container
    image: gcr.io/boldreports/bold-ums:4.1.78
    restart: on-failure
    environment: 
       - BOLD_SERVICES_HOSTING_ENVIRONMENT=docker
       - BOLD_SERVICES_DB_TYPE=postgresql
       - BOLD_SERVICES_DB_HOST=testhostname
       - BOLD_SERVICES_DB_PORT=testportnumber
       - BOLD_SERVICES_DB_USER=testuser
       - BOLD_SERVICES_DB_PASSWORD=testpassword
       - BOLD_SERVICES_DB_NAME=testdbname
       - BOLD_SERVICES_POSTGRESQL_MAINTENANCE_DB=testmaintenancedbname
       - BOLD_SERVICES_USER_EMAIL=testemail@test.com
       - BOLD_SERVICES_USER_PASSWORD=TestPassword@123
  ```
