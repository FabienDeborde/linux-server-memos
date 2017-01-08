#Netdata server monitoring

- Install the dependencies
    - *sudo apt-get install zlib1g-dev uuid-dev libmnl-dev gcc make autoconf autoconf-archive autogen automake pkg-config curl*
    - *sudo apt-get install python python-yaml python-mysqldb python-psycopg2 nodejs lm-sensors netcat*
- Clone from GitHub
    - *git clone https://github.com/firehol/netdata.git --depth=1 ~/netdata*
- Install the app using its installer
    - *cd ~/netdata*
    - *sudo ./netdata-installer.sh*

    - Useful output:

    > Installer Output<br>
    > It will be installed at these locations:
    >  - the daemon    at /usr/sbin/netdata
    >  - config files  at /etc/netdata
    >  - web files     at /usr/share/netdata
    >  - plugins       at /usr/libexec/netdata
    >  - cache files   at /var/cache/netdata
    >  - db files      at /var/lib/netdata
    >  - log files     at /var/log/netdata
    >  - pid file      at /var/run<br>
    > <br>
    >
    >By default netdata listens on all IPs on port 19999, so you can access it with:<br>
    >*http://this.machine.ip:19999/*<br>
    >To stop netdata, just kill it, with:<br>
    >**killall netdata**<br>
    >To start it, just run it:<br>
    >**/usr/sbin/netdata**<br>
    >Uninstall script generated: ./netdata-uninstaller.sh<br>
    >Update script generated   : ./netdata-updater.sh<br>

- Add rule in UFW
    - *sudo ufw allow 19999/tcp*
- Access Dashboard
    - *http://your_server_ip:19999/*
- Configure memory usage
    - *Edit /etc/netdata/netdata.conf*
    - *Change history value (28800 seconds => 8h, ~120MB RAM / 86400 seconds => 24h, ~360MB RAM)*
- Enable Kernel Sampe-page Merging
    - *Edit /etc/rc.local*
    - *Add before the exit 0: <br>
        echo 1 > /sys/kernel/mm/ksm/run <br>
        echo 1000 > /sys/kernel/mm/ksm/sleep_millisecs*
- Restart netdata
    - *sudo systemctl restart netdata*
- Hide netdata behind nginx (need a server already set up)
    - add at the top of the server config file<br>
    >upstream netdata-backend {<br>
    >server 127.0.0.1:19999;<br>
    >keepalive 64;<br>
    >}<br>

    - add under the location block<br>
    >location /netdata {<br>
    >    return 301 /netdata/;<br>
    >}<br>
    ><br>
    >location ~ /netdata/(?<ndpath>.*) {<br>
        >proxy_redirect off;<br>
        >proxy_set_header Host $host;<br>
    ><br>
        >proxy_set_header X-Forwarded-Host $host;<br>
        >proxy_set_header X-Forwarded-Server $host;<br>
        >proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;<br>
        >proxy_http_version 1.1;<br>
        >proxy_pass_request_headers on;<br>
        >proxy_set_header Connection "keep-alive";<br>
        >proxy_store off;<br>
        >proxy_pass http://netdata/$ndpath$is_args$args;<br>
    ><br>
        >gzip on;<br>
        >gzip_proxied any;<br>
        >gzip_types *;<br>
    >}<br>

    - Change the netada.conf to hide behind nginx and stop displaying data on myipaddress:19999: uncomment and change<br>
      >bind to = 127.0.0.1

- Using the Dashboard
    - *Drag left/right on graph to see different time*
    - *Hold **Shift** and scroll in or out to narrow or widen the time markers*
    - *Double click to reset the chart*
    - *If there is an update (top menu/update), install it via sudo ~/netdata/netdata-updater.sh*
