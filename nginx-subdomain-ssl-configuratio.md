



```
sudo nano /etc/nginx/sites-available/sivabharathy.in
```

```
server {
    listen 80;
    listen [::]:80;

    server_name sivabharathy.in;

    location / {
        # Configuration for handling requests goes here
        # You may need to proxy requests to a backend or define other directives
        # For static files, you might use root or alias directives
    }

    # Additional configurations can be added here
}
```

```
sudo ln -s /etc/nginx/sites-available/sivabharathy.in /etc/nginx/sites-enabled/
```


To configure Nginx for a subdomain, you need to create a server block that defines how Nginx should handle requests for that subdomain. Here's a basic example:

Assuming your subdomain is `sub.example.com`, follow these steps:

1. **Create a Configuration File:**

   Create a new Nginx configuration file for your subdomain. You can use the following command to create a new file:

   ```bash
   sudo nano /etc/nginx/sites-available/sub.example.com
   ```

   Replace `sub.example.com` with your actual subdomain.

2. **Configure the Server Block:**

   Add the following basic configuration to your file:

   ```nginx
   server {
       listen 80;
       listen [::]:80;

       server_name sub.example.com;

       location / {
           # Configuration for handling requests goes here
           # You may need to proxy requests to a backend or define other directives
           # For static files, you might use root or alias directives
       }

       # Additional configurations can be added here
   }
   ```

   Customize the `server_name` directive with your subdomain. You may need to add additional configuration depending on your application, such as proxy settings for a backend server or SSL configurations if you are using HTTPS.

3. **Enable the Configuration:**

   Create a symbolic link to enable the configuration:

   ```bash
   sudo ln -s /etc/nginx/sites-available/sub.example.com /etc/nginx/sites-enabled/
   ```

4. **Test Nginx Configuration:**

   Check if the Nginx configuration syntax is correct:

   ```bash
   sudo nginx -t
   ```

   If there are no syntax errors, reload Nginx to apply the changes:

   ```bash
   sudo systemctl reload nginx
   ```

Now, your Nginx server is configured to handle requests for your subdomain. Ensure that your subdomain points to the correct server IP address, and you should be able to access your subdomain through a web browser.

Remember to replace `sub.example.com` with your actual subdomain and customize the server block according to your application's needs. If you plan to use SSL, you would need to include SSL-related directives in the server block and obtain an SSL certificate.







To configure a subdomain with Let's Encrypt on Nginx, you'll need to follow these general steps. Please note that specific details may vary depending on your server configuration, operating system, and Nginx version.

### Prerequisites:

1. **Nginx Installed**: Ensure that Nginx is installed on your server.

2. **Domain and Subdomain Setup**: Make sure your domain and subdomain are properly configured and pointing to your server's IP address.

### Steps:

1. **Install Certbot**:

   ```bash
   sudo apt update
   sudo apt install certbot
   ```

   For other operating systems, you can refer to the official Certbot documentation: [Certbot - Installation](https://certbot.eff.org/lets-encrypt/ubuntufocal-nginx).

2. **Obtain SSL Certificate**:

   Run Certbot to obtain an SSL certificate for your subdomain:

   ```bash
   sudo certbot --nginx -d sivabharathy.in
   ```

   Follow the prompts to set up the certificate. Certbot will automatically configure Nginx for you.

3. **Automatic Renewal**:

   Certificates obtained from Let's Encrypt expire after 90 days. Ensure automatic renewal is set up:

   ```bash
   sudo certbot renew --dry-run
   ```

   This command tests the renewal process. If it works without errors, you can set up a cron job to run it regularly. Add the following to your crontab:

   ```bash
   sudo crontab -e
   ```

   Add the following line to run the renewal check daily:

   ```bash
   0 0 * * * /usr/bin/certbot renew --quiet
   ```

   Save and exit the editor.

4. **Nginx Configuration**:

   Ensure that your Nginx server block (usually found in `/etc/nginx/sites-available/yourdomain.com`) includes the SSL configuration:

   ```nginx
   server {
       listen 443 ssl;
       server_name subdomain.yourdomain.com;

       ssl_certificate /etc/letsencrypt/live/subdomain.yourdomain.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/subdomain.yourdomain.com/privkey.pem;
       include /etc/letsencrypt/options-ssl-nginx.conf;
       ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

       # Additional SSL configurations (e.g., TLS versions, ciphers) can be added here

       location / {
           # Nginx configuration for your subdomain
       }
   }
   ```

   Make sure to adjust the file paths and server_name according to your setup.

5. **Reload Nginx**:

   After modifying the Nginx configuration, reload Nginx to apply the changes:

   ```bash
   sudo service nginx reload
   ```

Now your subdomain should be accessible over HTTPS. Ensure that you replace "subdomain.yourdomain.com" with your actual subdomain and domain. Adjust the paths and configurations based on your server's setup and Nginx version.
