3proxy installation and configuration for Telegram Proxy
===

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
	cd /etc/3proxy/
	sudo wget https://tvoridob.ro/tgproxy/3proxy.cfg
	sudo chown proxy3:proxy3 -R /etc/3proxy
	sudo chown proxy3:proxy3 /usr/bin/3proxy
	sudo chmod 444 /etc/3proxy/3proxy.cfg
	cd /etc/init.d/ 
	sudo wget https://tvoridob.ro/tgproxy/3proxyinit
	sudo chmod +x /etc/init.d/3proxyinit
	sudo update-rc.d 3proxyinit defaults
	sudo /etc/init.d/3proxyinit start
	sudo ufw allow 1080/tcp
	sudo ufw enable
	rm ~/0.8.10.tar.gz
	sudo rm -r ~/3proxy-0.8.10
	
