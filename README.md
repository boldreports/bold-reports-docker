<a href="https://www.boldreports.com"><img alt="boldreports" width="400" src="https://www.boldreports.com/wp-content/uploads/2019/08/bold-reports-logo.svg"></a>
<br/>
<br/>

[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/boldreports/bold-reports-docker?sort=semver)](https://github.com/boldreports/bold-reports-docker/releases)
[![Documentation](https://img.shields.io/badge/docs-help.boldreports.com-blue.svg)](https://help.boldreports.com/enterprise-reporting/)
[![File Issues](https://img.shields.io/badge/file_issues-boldreports_support-blue.svg)](https://www.boldreports.com/support)

# What is Bold Reports

Bold Reports Enterprise Reporting is a business intelligence report management tool, built by Syncfusion for creating, managing, and distributing pixel-perfect paginated RDL reports behind your organization’s firewall.

Enterprise Reporting help us to analyse, explain and report business information in our day-to-day life.

## Deployment Prerequisites

### Hardware requirements

The following hardware requirements are necessary to run the Bold Reports solution:

* Operating System: You can use the Bold Reports Docker and Podman on the following operating systems: 
  * Windows
  * Ubuntu 20.04 LTS
  * Cent OS 7
  * Mac
  * Red Hat Enterprise Linux (RHEL)
  * Alpine Linux
* CPU: 4-core.
* Memory: 16 GB RAM.
* Disk Space: 8 GB or more.

### Software requirements

The following software requirements are necessary to run the Bold Reports Enterprise edition:

* Database: Microsoft SQL Server 2012+ | PostgreSQL | MySQL
* Application: Docker, Podman
* Web Browser: Microsoft Edge, Mozilla Firefox, and Chrome

# Supported tags

| Tags               | OS Version    | Last Modified |
| -------------      | ------------- | ------------- |
| `4.2.85`           | Ubuntu 20.04  (amd64)    | 10/03/2023 |
| `4.2.85_alpine`    | Alpine 3.13  (amd64)  | 10/03/2023 |
| `4.2.85_debian`     | Debian 10  (amd64,arm64)        | 10/03/2023 |
|`4.2.85_arm64`|Debian 10 (arm64)|10/03/2023 |
|`4.2.85_ubuntu_arm64`| Ubuntu 20.04  (arm64)        | 10/03/2023 |

Note: The tag `4.2.85_ubuntu_arm64` have some limitations where the data visualization will not be work in the exported reports.

# How to use this image
## Start a Bold Reports instance
<br />
To quickly get started, run the following command to run Bold Reports on your host machine. With this command, you would be able to access the instance from the host without the container’s IP address and the standard port mappings.<br/><br/>

```sh
docker run --name boldreports -p 80:80 -d syncfusion/boldreports
```

After running the command, you can access the Bold Reports App by entering `http://localhost` or `http://host-ip` in a browser. To know more about application startups, refer [here](#application-startup).

## Advanced command


```sh
docker run --name boldreports -p 80:80 -p 443:443 \
     -e APP_URL=<app_base_url> \
     -e OPTIONAL_LIBS=<optional_library_names> \
     -v <host_path_for_appdata_files>:/application/app_data \
     -v <host_path_for_nginx_config>:/etc/nginx/sites-available \
     -d syncfusion/boldreports:<tag>
```
### Example for Advanced docker run command

```sh
docker run --name boldreports -p 80:80 -p 443:443 \
     -e APP_URL=https://example.com \
     -e OPTIONAL_LIBS=mysql,oracle,postgresql \
     -v D:/boldreports/app_data:/application/app_data \
     -v D:/boldreports/nginx:/etc/nginx/sites-available \
     -d syncfusion/boldreports:6.2.7
``` 

Bold Reports accepts the following environment variables from the command line.
| Name                          |Required| Description   | 
| -------------                 |----------| ------------- | 
| `APP_URL`                     |No <br /><br /><br /> Needed when configuring with domain or IP| Domain or IP address with http/https protocol.<br/>For example, <br/>`http://<public_DNS_address>`<br/>`http://<public_ip_address>` <br/><br/>The default APP_URL is `http://localhost`<br/><br/> <b>Note:</b><br/>•	If you are using the IP address for the Base URL, make sure you are using the public IP of the machine instead of internal IP or local IP address. Applications can communicate with each other using the public IP alone. Host machine IP will not be accessible inside the application container.<br/>• For linux depoyment the default APP_URL is http://localhost or http://172.17.0.1<br/>• You can provide the HTTP or HTTPS scheme for APP_BASE_URL value.<br/>• Please refer to this section for [SSL Termination](docs/SSL-Termination).|
|`OPTIONAL_LIBS`|No|	These are the client libraries used in Bold Reports by default.<br/><br/>`'mysql,oracle,postgresql'`<br/><br/>Please refer [Consent to deploy client libraries](docs/consent-to-deploy-client-libraries.md) Libraries section to know more.|
|`<host_path_for_appdata_files>` |No|Persistent volume path for Bold Reports application data|
|`<host_path_for_nginx_config>` |No|Persistent volume path for Nginx configuration|

<br />

### Persisting application data

You can store the application data in your host machine to make the Bold Reports container a stateful application. Bold Reports application will read and write the data in your host machine.
 
Replace the `<host_path_for_appdata_files>` value with a directory path from your host machine in the advanced docker run command.

> **For example**<br/>
> Windows: `-v D:/boldreports/app_data:/application/app_data`<br/>
> Linux: `-v /home/boldreports/app_data:/application/app_data`

### Nginx configuration

You can mount a host directory to the Bold Reports container for maintaining the Nginx configuration. You can also store SSL certificates in this directory and can configure Nginx with them.

Replace the `<host_path_for_nginx_config>` value with a directory path from your host machine in the advanced docker run command.

> **For example**<br/>
> Windows: `-v D:/boldreports/nginx:/etc/nginx/sites-available`<br/>
> Linux: `-v /home/boldreports/nginx:/etc/nginx/sites-available`

Once, the Bold Reports container started to run, you can check the directory in your host machine. The `boldreports-nginx-config` file will be generated there. You can configure the Nginx inside the container using this file.

## Application Startup

Configure the Bold Reports On-Premise application startup to use the application. Please refer to the following link, for more details on configuring the application startup.

https://help.boldreports.com/enterprise-reporting/administrator-guide/application-startup/

# Docker compose:<br/>
* [BoldReports in single container image](#start-single-container-bold-reports-with-docker-compose).

* [BoldReports in multiple container image](#start-multiple-containers-bold-reports-with-docker-compose).
## Start single container Bold Reports with `docker-compose`
You can use docker-compose to easily run Bold Reports in an isolated environment built with Docker containers. The image shown here is a single image containing multiple Bold Reports services targeted for simplifying evaluation and minimalistic production use cases.
<br/>
Create a docker-compose.yml file that starts your `Bold Reports` as well as a separate `PostgreSQL` instance with volume mounts for data persistence:

```sh
version: '3.5'

services:
  boldreports:
   image: syncfusion/boldreports
   restart: always
   ports:
     - 8085:80
   # environment:
     # - APP_URL=<app_base_url>
   networks:
     - boldreports
   volumes:
     - boldreports_data:/application/app_data
    
  pgdb:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: <Password>
    volumes:
      - db_data:/var/lib/postgresql/data/
    networks:
      - boldreports

networks:
  boldreports:
  
volumes:
  boldreports_data:
    driver: local
    driver_opts:
      type: 'none'
      o: 'bind'
      device: '<host_path_boldreports_data>'
  db_data:
    driver: local
    driver_opts:
      type: 'none'
      o: 'bind'
      device: '<host_path_db_data>'
  ```

> **Note:**
> The docker volumes `boldreports_data` and `db_data` persists data of Bold Reports and PostgreSQL, respectively. [Learn more about docker volumes](https://docs.docker.com/storage/volumes/)

Now, run `docker-compose up -d` from your project directory.<br/>
 Please refer to [this guide](docs/single-container.md) to deploy Bold Reports in a simplified docker-compose environment with single image.

## Start multiple containers Bold Reports with `docker-compose`
Bold Reports now comes with multiple images for each of the services in it to run on docker-compose which is mainly for the purpose of production environment to scale services within Bold Reports.  Please refer to [this guide](docs/multiple-container.md) to get know about the multiple images and compose details to deploy Bold Reports in an advanced docker compose environment.

# Podman compose:<br/>
* Bold Reports in multiple container image.

## Start multiple container Bold Reports with `podman-compose`
Bold Reports now comes with multiple images for each of the services in it to run on podman-compose which is mainly for the purpose of production environment to scale services within Bold Reports.  Please refer to [this guide](docs/multiple-container-podman.md) to get know about the multiple images and compose details to deploy Bold Reports in an advanced podman compose environment.



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


## Environment variables used in id-ums 
Add environment variables in id-ums service for application startup in backend.If we use the below environment variables, we don't need manual Application Startup Configuration.


```sh
    id-ums:
    container_name: id_ums_container
    image: gcr.io/boldreports/bold-ums:4.2.85
    restart: on-failure
    environment: 
       - BOLD_SERVICES_HOSTING_ENVIRONMENT=docker
       - BOLD_SERVICES_DB_TYPE=postgresql
       - BOLD_SERVICES_DB_HOST=testhostname
       - BOLD_SERVICES_DB_PORT=25060
       - BOLD_SERVICES_DB_USER=testuser
       - BOLD_SERVICES_DB_PASSWORD=testpassword
       - BOLD_SERVICES_DB_NAME=testdbname
       - BOLD_SERVICES_POSTGRESQL_MAINTENANCE_DB=defaultdb
       - BOLD_SERVICES_USER_EMAIL=testemail@test.com
       - BOLD_SERVICES_USER_PASSWORD=testpassword.
  ```

# License

https://www.boldreports.com/terms-of-use/on-premise<br />

The images are provided for your convenience and may contain other software that is licensed differently (Linux system, Bash, etc. from the base distribution, along with any direct or indirect dependencies of the Bold Reports platform).

These pre-built images are provided for convenience and include all optional and additional libraries by default. These libraries may be subject to different licenses than the Bold Reports product.

If you want to install Bold Reports from scratch and precisely control which optional libraries are installed, please download the stand-alone product from boldreports.com. If you have any questions, please contact the Bold Reports team (https://www.boldreports.com/support).

It is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.





