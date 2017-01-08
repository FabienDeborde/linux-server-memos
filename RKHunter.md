#RKHunter

- Install RKHunter
    - *sudo apt install rkhunter*
- Check version
    - *sudo rkhunter --versioncheck*
- Update data files
    -*sudo rkhunter --update*
- Set baseline file properties
    - *sudo rkhunter --propupd*
- Perform initial run
    - *sudo rkhunter -c --enable all --disable none*
    - *will produce errors, press Enter to continue*
- Alternative way to check the log, displays only warnings
    - *sudo rkhunter -c --enable all --disable none --rwo*
- Edit rkhunter config file (in etc/rkhunter.conf)
    - *MAIL-ON-WARNING="email@mydomain.com"*
    - *MAIL_CMD=mail -s "[rkhunter] Warnings found for ${HOST_NAME}"*
    - *SCRIPTWHITELIST="/usr/sbin/adduser"<br/>
SCRIPTWHITELIST="/usr/bin/ldd"<br/>
SCRIPTWHITELIST="/usr/bin/unhide.rb"<br/>
SCRIPTWHITELIST="/bin/which"*<br/>
    - *ALLOWDEVFILE="/dev/.udev/rules.d/root.rules"*
    - *ALLOWHIDDENDIR="/dev/.udev"*
    - *ALLOWHIDDENFILE="/dev/.blkid.tab"<br/>
ALLOWHIDDENFILE="/dev/.blkid.tab.old"<br/>
ALLOWHIDDENFILE="/dev/.initramfs"*<br/>
    - *ALLOW_SSH_ROOT_USER=yes*
- Check if the config is valid
    - *sudo rkhunter -C* (if it's ok there is no output at all)
- Rerun the test to see if there is any warnings
    - *sudo rkhunter -c --enable all --disable none --rwo*
- Update file properties
    - *sudo rkhunter --propupd*
- Create a cron job
    - backup existing cron file: *sudo crontab -l > crontab.bak*
    - edit crontab: *sudo crontab -e*
    - add: *15 04 * * * /usr/bin/rkhunter --cronjob --update --quiet*

- Update RKHunter after software change
    - **sudo rkhunter --propupd**
