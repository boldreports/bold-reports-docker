## Run single container `Bold Reports` via `docker-compose`

 This quick-start guide demonstrates how to use Compose to set up and run Bold Reports. Before starting, make sure you have installed [Compose](https://docs.docker.com/compose/install/)

### Define the Project

  1. Create an empty project directory.<br/>
  You can name the directory something easy for you to remember. This directory is the context for your application image.<br/>
  This project directory should contains a `docker-compose.yml` file which is complete in itself for a good starter BoldReports project.
  
  2. Download the configuration files [here](/deploy/single-container/). This directory includes docker-compose YML file and configuration file for Nginx.

      > **Tip:**
        You can use either a `.yml` or `.yaml` extension for this file. They both works well.
      
  3.  Change into your project directory.
  For example, if you named your directory `my_boldreports`

      ```sh
      $  cd my_boldreports/
      ```

  4. Create a docker-compose.yml file that starts your `BoldReports`  and a separate `PostgreSQL` instance with volume mounts for data persistence:

```sh
services:
  boldreports:
   image: syncfusion/boldreports
   restart: always
   ports:
     - 8090:80
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

  5. You can also change the Port number other than `8090`

  6. Allocate a directory in your host machine to store the shared folders for applications’ usage. Replace the directory path with `<host_path_boldreports_data>` and `<host_path_db_data>` in **docker-compose.yml** file.

       For example, <br><b>Windows:</b> `device: 'D:/boldreports/boldreports_data'` and `device: 'D:/boldreports/db_data'` <br><b>Linux:</b> `device: '/var/boldreports/boldreports_data'` and `device: '/var/boldreports/db_data'`

      > **Note:**
      > The docker volumes `boldreports_data` and `db_data` persists data of Bold Reports and PostgreSQL respectively. [Learn more about docker volumes](https://docs.docker.com/storage/volumes/)

### Build the project

Now, run `docker-compose up -d` from your project directory.
<br />

This runs `docker-compose up` in detached mode, pulls the needed Docker images, and starts the boldreports and database containers, as shown in the example below.
```sh
docker-compose up -d

Creating network "my_boldreports_boldreports" with the default driver
Creating volume "my_boldreports_boldreports_data" with local driver
Creating volume "my_boldreports_db_data" with local driver
Pulling db (postgres:)...
latest: Pulling from library/postgres
7d63c13d9b9b: Pull complete
cad0f9d5f5fe: Pull complete
<...>
Digest:sha256:db927beee892dd02fbe963559f29a7867708747934812a80f83bff406a0d54fd
Status: Downloaded newer image for postgres:latest
Creating my_boldreports_boldreports_1 ... done
Creating my_boldreports_db_1     ... done
```
### Bring up Bold Reports in a web browser

Now, access the Bold Reports application by entering the URL as `http://localhost:8090` or `http://host-ip:8090` in the browser. When opening this URL in the browser, it will display the License page within a few seconds. The default port number mentioned in the compose file is 8090. If you are making changes to the port number, then you need to use that port number for accessing the Bold Reports application.

> **Note:**
> The Bold Reports site is not immediately available on port 8090 because the containers are still being initialized and may take a couple of minutes for the first load.

### Application Startup

Configure the Bold Reports On-Premise application startup to use the application. Please refer the following link for more details on configuring the application startup.

https://help.boldreports.com/enterprise-reporting/administrator-guide/application-startup/

> **Note:**
> To use the above configured PostgreSQL server in Bold Reports please use `pgdb` as the PostgreSQL server name.

### Shutdown and cleanup

The command `docker-compose down` removes the containers and default network, but preserves the volumes of Bold Reports and PostgreSQL. <br /><br />
The command `docker-compose down --volumes` removes the containers, default network, and all the volumes.

