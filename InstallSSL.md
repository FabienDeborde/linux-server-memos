#Install an SSL Certificate

- Create a new CSR key
    - *openssl req -new -newkey rsa:2048 -nodes -keyout mydomain.com.key -out mydomain.com.csr*
    - *copy the key somwhere safer than Home, like /etc/ssl/*
- Request new key from your CA
- Install it
    - *Create a file (example.com.chained.crt) in your ssl folder*
    - *Copy example.com.crt and example.com.ca-bundle*
    - *Delete the last block (corresponding to the **AddTrust External CA Root**)* (In COMODO case)
- Add stronger DHE parameter
    - In your cert directory: *openssl dhparam -out dhparam.pem 4096*
- Config the server block
    - *This is the full config file, containing SSL, DHparam, HSTS, OCSP, custom error and redirect to the https://www version of the website*
     >server {<br/>
    >listen 443 ssl http2;<br/>
    >listen [::]:443 ssl http2;<br/>
>
   >root /var/www/example.com/html;<br/>
>
    >index index.html;<br/>
   >
    >server\_name www.example.com;<br/>
>
    >\# certs sent to the client in SERVER HELLO are concatenated in ssl\_certificate<br/>
    >ssl\_certificate /etc/ssl/example.com/www.example.com.chained.crt;<br/>
    >ssl\_certificate\_key /etc/ssl/example.com/example.com.key;<br/>
    >ssl\_session\_timeout 1d;<br/>
    >ssl\_session\_cache shared:SSL:10m;<br/>
    >ssl\_session_tickets off;<br/>
>
     >\# Diffie-Hellman parameter for DHE ciphersuites, recommended 2048 bits<br/>
    >ssl\_dhparam /etc/ssl/dhparam.pem;<br/>
>
    >\# intermediate configuration. tweak to your needs.<br/>
   >ssl\_protocols TLSv1 TLSv1.1 TLSv1.2;<br/>
    >ssl\_ciphers 'EECDH+AESGCM:EDH+AESGCM:ECDHE-RSA-AES128-GCM-SHA256:AES256+EECDH:DHE-RSA-AES128-GCM-SHA256:AES256+EDH:ECDHE-RSA->AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128->SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3->SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3->SHA:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4';
    >ssl\_prefer\_server\_ciphers on;<br/>
>
    >\# HSTS (ngx\_http\_headers\_module is required) (15768000 seconds = 6 months)<br/>
    >add\_header Strict-Transport-Security max-age=15768000;<br/>
>
    >\# OCSP Stapling ---<br/>
    >\# fetch OCSP records from URL in ssl\_certificate and cache them<br/>
    >ssl\_stapling on;<br/>
    >ssl\_stapling\_verify on;<br/>
>
    >\# verify chain of trust of OCSP response using Root CA and Intermediate certs<br/>
    >ssl\_trusted\_certificate /etc/ssl/example.com/www.example.com.ocsp-cert.crt;<br/>
>
    >\# Custom 404 page (add hide 401/403 error under 404 error)<br/>
    >error\_page 401 403 404 /404.html;<br/>
>
   >access\_log /var/log/nginx/nginx.vhost-example.com.access.log;<br/>
   >error\_log /var/log/nginx/nginx.vhost-example.com.error.log;<br/>
>
    >location / {<br/>
      >\# First attempt to serve request as file, then<br/>
      >\# as directory, then fall back to displaying a 404.<br/>
      >try_files $uri $uri/ =404;<br/>
    >}<br/>
>}<br/>
>
>server {<br/>
  >listen [::]:80;<br/>
  >listen 80;<br/>
  >server\_name www.example.com;<br/>
  >return 301 https://www.example.com$request_uri;<br/>
>}
>
>server {<br/>
  >listen [::]:80;<br/>
  >listen 80;<br/>
  >listen [::]:443 ssl http2;<br/>
  >listen 443 ssl http2;<br/>
  >server\_name example.com;<br/>
  >return 301 $scheme://www.example.com$request_uri;<br/>
>}<br/>

-----------------------------
- Check <https://www.digitalocean.com/community/tutorials/how-to-install-an-ssl-certificate-from-a-commercial-certificate-authority>, <https://raymii.org/s/tutorials/Strong_SSL_Security_On_nginx.html> and <https://mozilla.github.io/server-side-tls/ssl-config-generator/>
- Test on <https://www.ssllabs.com/ssltest/>
