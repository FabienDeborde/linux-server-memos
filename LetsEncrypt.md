#Install a free SSL Certificate (using Let's Encrypt)

- Install Let's Encrypt
    - *sudo apt-get install letsencrypt*

- Use Webroot Plugin (add to the server config in site-vailable)
    >location ~ /.well-known {<br>
    >           allow all;<br>
    >   }

- Request SSL certificate
    - *sudo letsencrypt certonly -a webroot --webroot-path=/var/www/html -d example.com -d www.example.com*
    - *Keys should be in  /etc/letsencrypt/live/* and contain:<br>
    >cert.pem: domain's certificate<br>
    >chain.pem: The Let's Encrypt chain certificate<br>
    >fullchain.pem: cert.pem and chain.pem combined<br>
    >privkey.pem: certificate's private key<br>
    - */etc/letsencrypt/live/ is a symlink to the most recent version of the keys in /etc/letsencrypt/archive/

- Renew the process
    - *sudo letsencrypt renew*  (won't update the key if less than 30 days away from expiration)
    - *sudo crontab -e*
        >30 2 \* \* 1 /usr/bin/letsencrypt renew >> /var/log/le-renew.log <br>
        >35 2 \* \* 1 /bin/systemctl reload nginx <br>

     - *Will run letsencrypt -auto renew every Monday at 2:30am and reload Nginx after*
     - *Pipe the result to a log in /var/log/le-renew.log*
