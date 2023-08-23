
Step 1 : save below content as subdomain.host.conf (app.sivabharathy.conf) app-siva.conf
in directory /etc/apache2/sites-available

```bash
<VirtualHost *:80>
	
	ServerName cdn.sivabharathy.in

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/html

    ProxyRequests On
    ProxyPass / "http://154.49.243.252:3000/"
    ProxyPassReverse / "http://154.49.243.252:3000/"

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined


    RewriteEngine on
    RewriteCond %{SERVER_NAME} =cdn.sivabharathy.in
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```

Step 2 : run below command ro link to sites-enabled 

```
sudo ln -s /etc/apache2/sites-available/cdn-siva.conf /etc/apache2/sites-enabled/
```

Step 3 : 

// command to generate ssl for sub domains 
```
sudo certbot --apache -d cdn.sivabharathy.in
```

Step 4 :
```
sudo service apache2 restart
```
