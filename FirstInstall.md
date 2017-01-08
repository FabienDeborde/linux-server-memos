#Droplet (Ubuntu Server) First Install

- Connect to the server:
    <br> **~# ssh root@droplet-ip**

- Change root pwd :
    <br> **~# passwd**

- Update server:
    <br> **~# apt-get update && apt-get upgrade -y**

- Update timezone / time settings:
   <br> **~# dpkg-reconfigure tzdata && apt-get install ntp -y**<br>
   <br> *If there is a "setting locale failed" message, open the /etc/default/locale and add*
        >LANG="en_US.UTF-8" <br>
        >LC_ALL="en_US.UTF-8"<br>
        >LANGUAGE="en_US.UTF-8"<br>

- Add user:
    <br> **~# adduser *username***
- Give sudo access:
    <br> **~# usermod -aG sudo *username***

- *(Create a new SSH key on your local machine: ssh-keygen)*

- Copy it to the server (using Linux built-in application):
    - From your local machine
    - Application >> Passwords and Keys >> Secure Shell / Open SSH Keys
    - Right click on the key >> Configure key for Secure Shell
    - Enter Droplet IP and login name >> Set Up
    - (*make the file permissions 600*)

- Disable Password Authentication<br>
    change **/etc/ssh/sshd_config: PasswordAuthentication no**

- Reload SSH daemon<br>
    **sudo systemctl reload sshd**

- Connect to the machine:<br>
    **ssh 'username@droplet-ip'**

- Install firewall and fail2ban<br>
    **sudo apt-get install ufw fail2ban iptables-persistent -y**
    - Make sure UFW allow SSH<br>
        **sudo ufw allow OpenSSH**
    - Enable ufw<br>
        **sudo ufw enable**
    - Check ufw status:<br>
        **sudo ufw status**
    - Configure Fail2ban <br>
        check <https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04>
        check <https://www.digitalocean.com/community/tutorials/how-to-protect-an-nginx-server-with-fail2ban-on-ubuntu-14-04>
    - Reload Fail2ban<br>
        **sudo service fail2ban reload**<br>
        *Need to install iptables-persistent to save rules after reboot*<br/>
        (*use **sudo dpkg-reconfigure iptables-persistent** to save the new rules*)

- Install mailutils (with Postfix, easier to config)<br>
     - **sudo apt-get install mailutils**<br>
     - *Config postfix main.cf*<br>
     - *Check if hostname / hosts / mailname are correctly configured (careful of the droplet name, need a FQDN for the Droplet name)*<br>
     - *Add MX records, TXT records (SPF and DKIM)*<br>
     - *Check if the mail is classified as spam: <https://www.mail-tester.com/>*

- Maintain server updated :
    - Install unattended-upgrades<br>
      **sudo apt-get install unattended-upgrades** (so we don't have to apt-get update && apt-get upgrade && apt-get dist-upgrade every week)<br>
        (https://help.ubuntu.com/14.04/serverguide/automatic-updates.html)
    - Configure unattended-upgrades<br>
      **sudo dpkg-reconfigure unattended-upgrades  # answer yes**<br>
      modify unattended-upgrades config files (/etc/apt/apt.conf.d)
    - *Check /var/log/unattended-upgrades/ to see if it's working*<br>

- Secure the server:
    - Install Tripwire
    - Install Chkrootkit
    - Install Lynis
    - Install RKHunter

- When all config is done add to sshd_config
    - **AllowUsers yourusername**
    - **PermitRootLogin no**
