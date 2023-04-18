# Upgrading Bold Reports to latest version

This section explains how to upgrade Bold Reports to latest version in your Docker. You can refer to the features and enhancements from this [Release Notes](https://www.boldreports.com/release-history/embedded-reporting).


## Backup the existing data
Before upgrading the Bold Reports to latest version, make sure to take the backup of the following items.

* Files and folders from the shared location, which you have mounted to the deployments by volume.

* Database backup - Take a backup of Database, to restore incase if the upgrade was not successful or if applications are not working properly after the upgrade.


## Proceeding with upgrade
Bold Reports updates the database schema of your current version to the latest version. The upgrade process will retain all the resources and settings from the previous deployment.

You can download the latest docker-compose file and default.conf from this [docker-compose](https://raw.githubusercontent.com/ranganathan-arumugam/bold-reports-docker/v5.1.20/deploy/multiple-container/docker-compose.yml)
[default.conf](https://raw.githubusercontent.com/ranganathan-arumugam/bold-reports-docker/v5.1.20/deploy/multiple-container/default.conf) and use the below command to down the containers from where you deploy the docker compose file.

```sh
docker-compose down
```

Copy the latest downloaded files and replace in the exisitng deployed folder then give the values in required fields which is already done for existing Bold Reports Application.

And run the below command to upgrade Bold Reports.

```sh
docker-compose up -d
```