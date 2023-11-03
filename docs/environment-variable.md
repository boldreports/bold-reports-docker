# Environment variables and their usage

Bold Reports supports the following environment variables. You can find the name of the environment variable and its usage below.
| Name               | Required    | Description |
| -------------      | -------------       | ------------- |
|`APP_URL`                          | No <br /><br />Needed when configuring with domain or IP     | Domain or IP address with http/https protocol.<br />For example,<br />`http://<public_DNS_address>`<br />`http://<public_ip_address>`<br /><br />The default APP_URL is `http://localhost`<br /><br /><b>Note</b><br />* If you are using the IP address for the Base URL, ensure you are using the public IP of the machine instead of internal IP or local IP address. Applications can communicate with each other using the public IP alone. Host machine IP will not be accessible inside the application container.<br />* For linux depoyment the default APP_URL is http://localhost or http://172.17.0.1 <br />* You can provide the HTTP or HTTPS scheme for APP_BASE_URL value.<br />Please refer to this section for [SSL Termination](ssl-termination.md).|
|`OPTIONAL_LIBS`                    | No                                                           | 	These are the client libraries used in Bold Reports by default.<br /><br />`mongodb,mysql,influxdb,snowflake,oracle,clickhouse,google`<br /><br />Please refer [Consent to deploy client libraries](../docs/consent-to-deploy-client-libraries.md) Libraries section to know more.|
|`<host_path_for_appdata_files>`    | No                                                            | Persistent volume path for the Bold Reports application data|
|`<host_path_for_nginx_config>`     | No                                                            |Persistent volume path for the Nginx configuration|

## Environment variables for configuring `Application Startup` in backend

The following Environment variables are optional. If not provided, a manual Application Startup configuration is needed.
| Name               | Required    | Description |
| -------------      | -------------       | ------------- |
|`BOLD_SERVICES_HOSTING_ENVIRONMENT`          | Yes         | docker|
|`BOLD_SERVICES_UNLOCK_KEY`                   | Yes         | License key for activating Bold Reports. Please refer to [this document](https://support.boldreports.com/kb/article/13271/how-do-i-get-my-offline-license-key-from-our-bold-reports-account-page) to download the key.<br />If you don't have the download key option, please create a support ticket [here](https://support.boldreports.com/support/tickets/create).|
|`BOLD_SERVICES_DB_TYPE`                      | Yes         | Type of database server can be used for configuring Bold Reports.<br /><br />The following DB types are accepted:<br />1. mssql – Microsoft SQL Server/Azure SQL Database<br />2. postgresql – PostgreSQL Server<br />3. mysql – MySQL/MariaDB Server|
|`BOLD_SERVICES_DB_HOST`                      | Yes         | Name of the Database Server|
|`BOLD_SERVICES_DB_PORT`                      | No          | 	The system will use the following default port numbers based on the database server type.<br />PostgrSQL – 5234<br />MySQL -3306<br /><br />Please specify the port number for your database server if it is configured on a different port.<br /><br />For MS SQL Server, this parameter is not necessary.|
|`BOLD_SERVICES_DB_USER`                      | Yes         | Username for the database server
|`BOLD_SERVICES_DB_PASSWORD`                  | Yes         | The database user's password|
|`BOLD_SERVICES_DB_NAME`                      | No          | If the database name is not specified, the system will create a new database called bold services.<br /><br />If you specify a database name, it should already exist on the server.|
|`BOLD_SERVICES_POSTGRESQL_MAINTENANCE_DB`    | Yes         | For PostgreSQL DB Servers, this is an optional parameter.<br />The system will use the database name `postgres` by default.<br />If your database server uses a different default database, please provide it here.|
|`BOLD_SERVICES_DB_ADDITIONAL_PARAMETERS`     | No          | If your database server requires additional connection string parameters, include them here.<br /><br />Connection string parameters can be found in the official document.<br />My SQL: https://dev.mysql.com/doc/connector-net/en/connector-net-8-0-connection-options.html<br />PostgreSQL: https://www.npgsql.org/doc/connection-string-parameters.html<br />MS SQL: https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring<br /><br /><b>Note:</b> A semicolon(;) should be used to separate multiple parameters.|
|`BOLD_SERVICES_USER_EMAIL`                   | Yes         | It should be a valid email.|
|`BOLD_SERVICES_USER_PASSWORD`                | Yes         | It should meet our password requirements.<br /><br /><b>Note:</b>Password must meet the following requirements. It must contain at least 6 characters, 1 uppercase character, 1 lowercase character, 1 numeric character, 1 special character|
|`BOLD_SERVICES_USE_SITE_IDENTIFIER`          | No          | 	The variable is optional, and the default value is <b>TRUE</b>.<br />By default, all sites in Bold Reports require a site identifier, which differentiates sites on the same domain. That is https://example.com/reporting/site/{site_identifier}<br />You can ignore the site identifier by setting the value as <b>FALSE</b>. If the site identifier is disabled, each site requires a unique domain.|

## Environment variables for configuring `Branding` in backend

The following environment variables are optional. If they are not provided, Bold Reports will use the default configured values.

| Name               | Description    |
| -------------      | -------------       |
| BOLD_SERVICES_BRANDING_MAIN_LOGO       | This is the header logo for the application, and the preferred image size is 40 x 40 pixels.|
| BOLD_SERVICES_BRANDING_LOGIN_LOGO      | This is the login logo for the application, and the preferred image size is 200 x 40 pixels.|
| BOLD_SERVICES_BRANDING_EMAIL_LOGO      | This is an email logo, and the preferred image size is 200 x 40 pixels.|
BOLD_SERVICES_BRANDING_FAVICON           | This is a favicon, and the preferred image size is 40 x 40 pixels.|
| BOLD_SERVICES_BRANDING_FOOTER_LOGO     | This is powered by the logo, and the preferred size is 100 x 25 pixels.<br /><br /><b>Note:</b><br />* All branding variables are accepted as URL.<br />* <b>Ex:</b> https://example.com/loginlogo.jpg.<br />* <b>Image type:</b> png, svg, jpg, jpeg.<br/>* If you want to use custom branding, provide the value for all branding variables. If all variable values are given, the application will use the branding images, otherwise, it will take the default logos.|
| BOLD_SERVICES_SITE_NAME                | This is organization name.<br/>If the value is not given, the site will be deployed using the default name.|
| BOLD_SERVICES_SITE_IDENTIFIER          | This is site identifier, and it will be the part of the application URL.<br />If the value is not given, the site will be deployed using the default value.