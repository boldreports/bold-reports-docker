# How to use host path as persistent volume for Bold Reports deployment?

You can store the application data on your host machine to make the Bold Reports container a stateful application. The Bold Reports application will read and write the data on your host machine. In the following section, we will learn how to use the host path as a persistent volume for Bold Reports deployment.

1. When deploying the Bold Reports application using Docker or Docker compose, you can pass the host path as a persistent volume. Here is an example using the Docker command.
   ```sh
   docker run --name boldreports -p 80:80 -p 443:443 \
   -e APP_URL=<app_url> \
   -v <host_path_for_appdata_files>:/application/app_data \
   -v <host_path_for_nginx_config>:/etc/nginx/sites-available \
   -d syncfusion/boldreports:<tag>
   ```

   **Persisting application app_data**

   Replace the `<host_path_for_appdata_files>` value with a directory path from your host machine in the advanced docker run command.

   ```sh
   **For example**
   **Windows:** `-v D:/boldreports/nginx:/etc/nginx/sites-available`
   **Linux:** `-v /home/boldreports/nginx:/etc/nginx/sites-available`
   ```
   **Nginx configuration**</br>
   Replace the `<host_path_for_nginx_config>` value with a directory path from your host machine in the advanced docker run command.

   **For example**</br>
   **Windows:** `-v D:/boldreports/nginx:/etc/nginx/sites-available`</br>
   **Linux:** `-v /home/boldreports/nginx:/etc/nginx/sites-available`

   **Example:**
   ```sh
   docker run --name boldreports -p 80:80 -p 443:443 \
   -e APP_URL=https://example.com \
   -v D:/boldreports/app_data:/application/app_data \
   -v D:/boldreports/nginx:/etc/nginx/sites-available \
   -d syncfusion/boldreports:6.15.11
   ```

2. After running the command, access the Bold Reports App by entering `APP_URL` in a browser. At this point, Bold Reports should be running in `<app_url>` (as appropriate)
   ![docker-startup](../docs/images/docker-startup.png)
   > **Note:** The BoldReports site is not immediately available because the containers are still being initialized and may take a couple of minutes for the first load.

**Application Startup**

Configure the Bold Reports On-Premise application startup to use the application. Please refer the following link for more details on configuring the application startup.