# How to deploy Bold Reports and configure startup manually?

In the following section, we will deploy a single container Bold Reports application using Docker Compose and manually configure the application startup.

## Bold Reports Deployment:

1. Download docker compose file using the following command.
   ```sh
   curl -o docker-compose.yml "https://raw.githubusercontent.com/boldreports/bold-reports-docker/master/deploy/single-container/docker-compose.yml"
   ```
2. Open the docker compose file and fill the mandatory field - APP_URL

   ![docker-compose-database-detail](/docs/images/single-container-app-url.png)

   **APP_URL Guidance:**
   * Provide the HTTP scheme for APP_BASE_URL value. For example,<br />
     `http://example.com`<br />
     `http://<public_ip_address>:8085`
   * For `Windows` and `MacOS` use either http://host.docker.internal. Docker Desktop provides `host.docker.internal` and gateway.docker.internal DNS for communication between docker applications and host machine. Please make sure that the host.docker.internal DNS has your IPv4 address mapped in your hosts file on Windows(C:\Windows\System32\drivers\etc\hosts).
   * For `Linux` use the Machine Public IP address as the value for APP_URL with the HTTP scheme.

3. Run docker compose up command.
   ```sh
   docker-compose up -d
   ```
   ![docker-compose-up](./images/docker-compose-up.png)
   > **Note:** The docker volumes boldreports_data persists data of Bold Reports. [Learn more about docker volumes](https://docs.docker.com/storage/volumes/)
4. After running the command, access the Bold Reports App by entering `APP_URL` in a browser. At this point, Bold Reports should be running in `<app_url>:8085` (as appropriate)

   ![docker-startup](../docs/images/docker-startup.png)
   > **Note:** The BoldReports site is not immediately available on port 8085 because the containers are still being initialized and may take a couple of minutes for the first load.

### Application Startup

Configure the Bold Reports On-Premise application startup to use the application. Please refer the following link for more details on configuring the application startup.

https://help.boldreports.com/enterprise-reporting/administrator-guide/application-startup/

### Shutdown and Cleanup

The command `docker-compose down` removes the containers and default network, but preserves the volumes of Bold Reports and PostgreSQL.

The command `docker-compose down --volumes` removes the containers, default network, and all the volumes.