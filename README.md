3proxy installation and configuration for Telegram Proxy
===

	sudo apt-get install -y build-essential nano wget tar gzip ufw
	cd ~
	wget --no-check-certificate https://github.com/z3APA3A/3proxy/archive/0.8.11.tar.gz
	tar xzf 0.8.11.tar.gz
	cd ~/3proxy-0.8.11
	sudo make -f Makefile.Linux
	sudo mkdir /etc/3proxy
	cd ~/3proxy-0.8.11/src
	sudo cp 3proxy /usr/bin/
	sudo adduser --system --no-create-home --disabled-login --group proxy3
	cd /etc/3proxy/
	sudo wget https://tvoridob.ro/tgproxy/3proxy.cfg
	id proxy3	//запоминаем setgid и setuid
	cat /etc/resolv.conf	//запоминаем неймсервера
	sudo nano /etc/3proxy/3proxy.cfg	//вписываем в конфиг setgid, setuid и неймсервера
	sudo chown proxy3:proxy3 -R /etc/3proxy
	sudo chown proxy3:proxy3 /usr/bin/3proxy
	sudo chmod 444 /etc/3proxy/3proxy.cfg
	cd /etc/init.d/ 
	sudo wget https://tvoridob.ro/tgproxy/3proxyinit
	sudo chmod +x /etc/init.d/3proxyinit
	sudo update-rc.d 3proxyinit defaults
	sudo /etc/init.d/3proxyinit start
	sudo ufw allow 1080/tcp
	sudo ufw allow 22/tcp
	sudo ufw enable
	rm ~/0.8.11.tar.gz
	sudo rm -r ~/3proxy-0.8.11
	
![Fuck RKN!](https://img.shields.io/badge/fuck-RKN-brightgreen.svg)
