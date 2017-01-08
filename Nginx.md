# Nginx

## Basic commands

*To stop your web server:* <br>
**sudo systemctl stop nginx**

*To start the web server when it is stopped:* <br>
**sudo systemctl start nginx**

*To stop and then start the service again:* <br>
**sudo systemctl restart nginx**

*If you are simply making configuration changes, Nginx can often reload without dropping connections:* <br>
**sudo systemctl reload nginx** <br/>
or **nginx -s reload**

*By default, Nginx is configured to start automatically when the server boots. You can disable this behavior:* <br>
**sudo systemctl disable nginx**

*To re-enable the service to start up at boot:* <br>
**sudo systemctl enable nginx**

*To  check the server status:* <br>
**systemctl status nginx**

*Another way to check the server status:* <br>
**ps -aux | grep nginx**

*To  check Nginx version and compiled modules:* <br>
**sudo nginx -v**

*To  check there is no syntax error in config files:* <br>
**sudo nginx -t**

*To  upgrade Nginx:* <br>
**sudo service nginx upgrade**<br/>
*(This upgrade command will start Nginx with the new upgraded binaries along with the old Nginx version. It will also move the listening sockets to the new binary files and then shut down the old binaries. This will result in a zero downtime upgrade.)*



##Content

**/var/www/html**: The actual web content, which by default only consists of the default Nginx page you saw earlier, is served out of the /var/www/html directory. This can be changed by altering Nginx configuration files.

##Server Configuration

**/etc/nginx**: The nginx configuration directory. All of the Nginx configuration files reside here.

**/etc/nginx/nginx.conf**: The main Nginx configuration file. This can be modified to make changes to the Nginx global configuraiton.

**/etc/nginx/sites-available**: The directory where per-site "server blocks" can be stored. Nginx will not use the configuration files found in this directory unless they are linked to the sites-enabled directory (see below). Typically, all server block configuration is done in this directory, and then enabled by linking to the other directory.

**/etc/nginx/sites-enabled/**: The directory where enabled per-site "server blocks" are stored. Typically, these are created by linking to configuration files found in the sites-available directory. <br>
    - *symlink from sites-available* : **sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/**

**/etc/nginx/snippets**: This directory contains configuration fragments that can be included elsewhere in the Nginx configuration. Potentially repeatable configuration segments are good candidates for refactoring into snippets.

##Server Logs

**/var/log/nginx/access.log**: Every request to your web server is recorded in this log file unless Nginx is configured to do otherwise.

**/var/log/nginx/error.log**: Any Nginx errors will be recorded in this log.

##Secure Nginx

*Hide Info in Nginx Header: Comment out in nginx.conf*<br>
**server_tokens off;**

*Change the 4xx (client-side) error pages: add in a server block config*<br>
**error_page 401 403 404 /404.html;**

*Config SSL*<br>
    - **sudo mkdir /etc/ssl/** (dir for our SSL certificates)

##Password Protection

*Create a user*<br>
**sudo sh -c "echo -n 'username:' >> /etc/nginx/.htpasswd"**

*Create a password using OpenSSL*<br>
**sudo sh -c "openssl passwd -apr1 >> /etc/nginx/.htpasswd"**

*Configure Nginx to use this password by adding these 2 lines in the server block config file*<br>
    - *(place these 2 lines either inside the location / { } part to secure only a part of the site or inside the server { } to secure everything )*
>auth\_basic "Restricted Content";<br>
>auth\_basic\_user\_file /etc/nginx/.htpasswd;

*Restart Nginx*<br>
**sudo nginx -s reload**
