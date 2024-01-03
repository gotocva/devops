To install Nginx on Ubuntu, you can use the package manager. Here are the steps to install Nginx on Ubuntu:

1. Update the package list to ensure you have the latest information about available packages:

   ```bash
   sudo apt update
   ```

2. Install Nginx:

   ```bash
   sudo apt install nginx
   ```

   During the installation, you may be prompted to confirm the installation by typing 'Y' and then pressing Enter.

3. Once the installation is complete, start the Nginx service:

   ```bash
   sudo systemctl start nginx
   ```

4. Enable Nginx to start on boot:

   ```bash
   sudo systemctl enable nginx
   ```

Now, Nginx is installed and running on your Ubuntu machine. You can verify the installation by opening a web browser and entering your server's IP address in the address bar. You should see the default Nginx welcome page.

If you encounter any issues, you can check the status of the Nginx service with the following command:

```bash
sudo systemctl status nginx
```

If you need to make changes to the default Nginx configuration, the configuration files are typically located in the `/etc/nginx` directory. The main configuration file is `nginx.conf`, and additional configuration files for sites are often found in the `sites-available` directory.

Feel free to customize the configuration based on your needs. After making changes, remember to restart the Nginx service to apply the modifications:

```bash
sudo systemctl restart nginx
```
