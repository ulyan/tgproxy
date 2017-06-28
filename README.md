sudo apt-get install -y build-essential nano wget tar gzip ufw
cd ~
wget --no-check-certificate https://github.com/z3APA3A/3proxy/archive/0.8.10.tar.gz
tar xzf 0.8.10.tar.gz
cd ~/3proxy-0.8.10
sudo make -f Makefile.Linux
sudo mkdir /etc/3proxy
cd ~/3proxy-0.8.10/src
sudo cp 3proxy /usr/bin/
sudo adduser --system --no-create-home --disabled-login --group proxy3
id proxy3
sudo nano /etc/3proxy/3proxy.cfg
sudo chown proxy3:proxy3 -R /etc/3proxy
sudo chown proxy3:proxy3 /usr/bin/3proxy
sudo chmod 444 /etc/3proxy/3proxy.cfg

    daemon
    setgid XXX
    setuid XXX
    nserver *.*.*.*
    nserver *.*.*.*
    nscache 65536
    log /dev/null
    auth none
    timeouts 1 5 30 60 180 1800 15 60
    allow * * 149.154.160.0/20 443 CONNECT * *
    allow * * 91.108.4.0/22 443 CONNECT * *
    allow * * 91.108.56.0/22 443 CONNECT * *
    allow * * 91.108.8.0/22 443 CONNECT * *
    socks -p1080

sudo nano /etc/init.d/3proxyinit

    #!/bin/sh
    #
    ### BEGIN INIT INFO
    # Provides: 3Proxy
    # Required-Start: $remote_fs $syslog
    # Required-Stop: $remote_fs $syslog
    # Default-Start: 2 3 4 5
    # Default-Stop: 0 1 6
    # Short-Description: Initialize 3proxy server
    # Description: starts 3proxy
    ### END INIT INFO
    
    case "$1" in
     start)
     echo Starting 3Proxy
    
     /usr/bin/3proxy /etc/3proxy/3proxy.cfg
     ;;
    
     stop)
     echo Stopping 3Proxy
     /usr/bin/killall 3proxy
     ;;
    
     restart|reload)
     echo Reloading 3Proxy
     /usr/bin/killall -s USR1 3proxy
     ;;
     *)
     echo Usage: \$0 "{start|stop|restart}"
     exit 1
    esac
    exit 0
    
sudo chmod +x /etc/init.d/3proxyinit
sudo update-rc.d 3proxyinit defaults
sudo /etc/init.d/3proxyinit start
sudo ufw allow 1080/tcp
sudo ufw enable
rm ~/0.8.10.tar.gz
sudo rm -r ~/3proxy-0.8.10
