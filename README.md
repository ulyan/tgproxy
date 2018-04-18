# Dante Proxy installation for Telegram Messenger

## Ubuntu 16.04

	sudo apt-get -y update && apt-get -y upgrade
	sudo apt-get install -y gcc build-essential libwrap0 libwrap0-dev libpam0g-dev make nano wget tar gzip ufw
	cd /opt
	wget http://www.inet.no/dante/files/dante-1.4.2.tar.gz
	tar -xvf dante-1.4.2.tar.gz
	cd dante-1.4.2/
	mkdir /opt/dante
	./configure --prefix=/opt/dante
	make && make install
	/opt/dante/sbin/sockd -v //проверка установки и версии
	wget -c http://tvoridob.ro/tgproxy/sockd.conf -O /etc/sockd.conf
	ifconfig //запомните адрес сетевого интерфейса
	nano /etc/sockd.conf //вместо eth0 впишите сетевой интерфейс, возможно в external придется вписать внешний IP сервера
	/opt/dante/sbin/sockd -D -f /etc/sockd.conf -D //запуск Dante, выключается командой /usr/bin/pkill sockd
	sudo ufw allow 1080/tcp
	sudo ufw allow 22/tcp
	sudo ufw enable
	rm /opt/dante-1.4.2.tar.gz
	sudo rm -r /opt/dante-1.4.2/

Dante enabled and working at YOUR.SERVER.IP:1080

![Fuck RKN!](https://img.shields.io/badge/Fuck-RKN-brightgreen.svg)
