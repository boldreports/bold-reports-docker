<a href="https://www.boldreports.com"><img alt="boldreports" width="400" src="https://www.boldreports.com/wp-content/uploads/2019/08/bold-reports-logo.svg"></a>
<br/>
<br/>

[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/boldreports/bold-reports-docker?sort=semver)](https://github.com/boldreports/bold-reports-docker/releases)
[![Documentation](https://img.shields.io/badge/docs-help.boldreports.com-blue.svg)](https://help.boldreports.com/enterprise-reporting/)
[![File Issues](https://img.shields.io/badge/file_issues-boldreports_support-blue.svg)](https://www.boldreports.com/support)

# What is Bold Reports

Bold Reports Enterprise Reporting is a business intelligence report management tool built by Syncfusion for creating, managing, and distributing pixel-perfect paginated RDL reports behind your organization’s firewall.

Enterprise Reporting helps us to analyse, explain and report business information in our day-to-day life.

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
| `5.2.26_refresh_release`           | Ubuntu 20.04  (amd64)    | 18/07/2023 |
| `5.2.26_refresh_release_alpine`    | Alpine 3.13  (amd64)  | 18/07/2023 |
| `5.2.26_refresh_release_debian`     | Debian 10  (amd64,arm64)        | 18/07/2023 |
|`5.2.26_refresh_release_arm64`|Debian 10 (arm64)|18/07/2023 |
|`5.2.26_refresh_release_ubuntu_arm64`| Ubuntu 20.04  (arm64)        | 18/07/2023 |

Note: The tag `5.2.26_refresh_release_ubuntu_arm64` have some limitations where the data visualization will not be work in the exported reports.

# How to use this image

The above Bold Reports image can be deployed using Docker or Docker Compose. In the following section, we are going to start the Bold Reports application and a separate PostgreSQL instance with volume mounts for data persistence using Docker Compose.

  1. Download the Docker Compose file by using the following command.
  ```sh
  curl -o docker-compose.yml "https://raw.githubusercontent.com/boldreports/bold-reports-docker/main/deploy/single-container-pre-configured/docker-compose.yml"
  ```
  2. Open the Docker Compose file, fill the BOLD_SERVICES_UNLOCK_KEY value, and save it. You can refer to the KB document to obtain the offline Bold Reports unlock key.
    ![docker-compose-variable](docs/images/docker-compose-variable.png)
  
  3. Run the command below. This command will start the Bold Reports and Postgres SQL containers and display the Bold Reports logs to provide information about the installation status of the Bold Reports application.
     ```sh
     docker-compose up -d; docker-compose logs -f boldreports
     ```
     ![docker-compose-up](docs/images/docker-compose-up.png)

  4. Now, access the Bold Reports application by entering the URL as http://localhost:8085 or http://host-ip:8085 in the browser. When opening this URL in the browser, it will configure the application startup in the background and display the page below within a few seconds. The default port number mentioned in the compose file is 8085. If you are making changes to the port number, then you need to use that port number for accessing the Bold Reports application.
    ![docker-startup](docs/images/docker-startup.png)
  
# Upgrade Bold Reports

If you are upgrading Bold Reports to 5.3.8, please follow the steps in this [link](/docs/upgrade.md).

# How to Deploy Bold Reports using Advanced Configuration?

In this section, you will learn how to run the Bold Reports application using advanced configurations such as configuring Bold Reports using an existing DB server, using a host directory as a persistent volume, configuring startup manually, configuring an SSL certificate, and running a multi-container Reports application.

1. [How to deploy Bold Reports using existing DB server?](./docs/how-to-deploy-bold-reports-using-existing-db-server.md)
2. [How to deploy Bold Reports and configure startup manually?](./docs/how-to-deploy-bold-reports-and-configure-startup-manually.md)
3. [How to use host path as Persistent Volume?](./docs/how-to-use-host-path-as-persistent-volume-for-bold-reports-deployment.md)
4. [How to configure SSL for Bold Reports application?  ](./docs/FAQ/how-to-configure-ssl-for-docker-compose.md)
5. [How to start multiple containers Bold Reports with Docker Compose?](./docs/multiple-container.md)
6. [Bold Reports supported environment variables and their usage?](./docs/environment-variable.md)

# License

https://www.boldreports.com/terms-of-use/on-premise<br />

The images are provided for your convenience and may contain other software that is licensed differently (Linux system, Bash, etc. from the base distribution, along with any direct or indirect dependencies of the Bold Reports platform).

These pre-built images are provided for convenience and include all optional and additional libraries by default. These libraries may be subject to different licenses than the Bold Reports product.

If you want to install Bold Reports from scratch and precisely control which optional libraries are installed, please download the stand-alone product from boldreports.com. If you have any questions, please contact the Bold Reports team (https://www.boldreports.com/support).

It is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.

# FAQ

[How to configure SSL for Bold Reports Application in single container and multiple container?](https://github.com/boldreports/bold-reports-docker/blob/master/docs/FAQ/how-to-configure-ssl-for-docker-compose.md)
[How to reset the database for Bold Reports application in docker environment?](https://github.com/boldreports/bold-reports-docker/blob/master/docs/FAQ/how-to-configure-ssl-for-docker-compose.md)
[How to auto deploy multiple services Bold BI via docker-compose?](./docs/FAQ/how-to-auto-deploy-bold-reports-multiple-services-in-docker-compose.md)

