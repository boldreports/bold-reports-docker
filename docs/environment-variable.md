# Environment variables and their usage

Bold Reports supports the following environment variables. You can find the name of the environment variable and its usage below.
| Name               | Required    | Description |
| -------------      | -------------       | ------------- |
|`APP_URL`           | No <br /><br />Needed when configuring with domain or IP     | Domain or IP address with http/https protocol.<br />Domain or IP address with http/https protocol.For example,<br />`http://<public_DNS_address>`<br />`http://<public_ip_address>`<br /><br />The default APP_URL is `http://localhost`<br /><br /><b>Note</b>*If you are using the IP address for the Base URL, ensure you are using the public IP of the machine instead of internal IP or local IP address. Applications can communicate with each other using the public IP alone. Host machine IP will not be accessible inside the application container.<br />*For linux depoyment the default APP_URL is http://localhost or http://172.17.0.1 <br />*You can provide the HTTP or HTTPS scheme for APP_BASE_URL value.<br />Please refer to this section for [SSL Termination](ssl-termination.md).|
|`OPTIONAL_LIBS`      | No                                                           | 	These are the client libraries used in Bold Reports by default.<br /><br />`mongodb,mysql,influxdb,snowflake,oracle,clickhouse,google`<br /><br />Please refer [Consent to deploy client libraries] Libraries section to know more.|









## Environment variables for configuring `Application startup` in backend using `docker-compose` and `podman-compose`
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

