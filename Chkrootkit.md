#Chkrootkit

- Install chkrootkit
    - *sudo apt install chkrootkit*

- Check the system
    - *sudo chkrootkit*

- Set up a cron job
    - *sudo crontab -e"
    - *45 3 * * * /usr/sbin/chkrootkit 2>&1 | mail -s "chkrootkit output of my server" email@mydomain.com)*
