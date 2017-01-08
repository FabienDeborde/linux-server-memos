#Lynis

- Install Lynis
   >cd /tmp<br>
   >wget https://cisofy.com/files/lynis-2.4.0.tar.gz<br>
   >tar xvfz lynis-2.4.0.tar.gz<br>
   >sudo mv lynis /usr/local/<br>
   >sudo ln -s /usr/local/lynis/lynis /usr/local/bin/lynis<br>

- Check for updates
    - *lynis update info*

- Check system
    - *sudo lynis audit system*
    - audit report in */var/log/lynis.log*

- Add a cronjob
    - *sudo cron -e*
    - *00 3 * * * /usr/local/bin/lynis --quick 2>&1 | mail -s "lynis output of my server" email@mydomain.com*
