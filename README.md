# Настройка прокси-сервера для Telegram ![Fuck RKN!](https://img.shields.io/badge/Fuck-RKN-brightgreen.svg)

## Ubuntu 16.04

**Обновляем систему и устанавливаем необходимые пакеты:**

	sudo apt-get -y update && apt-get -y upgrade
	sudo apt-get install -y gcc build-essential libwrap0 libwrap0-dev libpam0g-dev make nano wget tar gzip ufw docker.io

**Загружаем и компилируем Dante:**

	cd /opt
	wget http://www.inet.no/dante/files/dante-1.4.2.tar.gz
	tar -xvf dante-1.4.2.tar.gz
	cd dante-1.4.2/
	mkdir /opt/dante
	./configure --prefix=/opt/dante
	make && make install
	rm /opt/dante-1.4.2.tar.gz
	rm -r /opt/dante-1.4.2/
	wget -c https://tlgrm.ninja/sockd.conf -O /etc/sockd.conf

**Узнаем сетевой интерфейс и вписываем его в конфиг, в большинстве случаев ничего менять не придется:**

	ifconfig
	nano /etc/sockd.conf

**Запускаем SOCKS-прокси:**

	/opt/dante/sbin/sockd -D -f /etc/sockd.conf

**Останавливаем SOCKS-прокси:**

	/usr/bin/pkill sockd
	
**Устанавливаем и запускаем MTProto-прокси:**

	docker run -d --net=host --name=mtproto-proxy --restart=always -v proxy-config:/data telegrammessenger/proxy:latest
	
**Получаем ссылку для настройки MTProto-прокси:**

	docker logs mtproto-proxy
	
**Останавливаем MTProto-прокси:**

	docker stop mtproto-proxy
	
**Закрываем на сервере все порты, кроме 22 (ssh), 1080 (SOCKS) и 443 (MTProto):**

	sudo ufw allow 1080/tcp
	sudo ufw allow 22/tcp
	sudo ufw allow 443/tcp

**Закрываем доступ для сетей Mail.ru (https://t.me/zatelecom/4773):**

	ufw deny from 5.61.16.0/21
	ufw deny from 5.61.232.0/21
	ufw deny from 79.137.157.0/24
	ufw deny from 79.137.174.0/23
	ufw deny from 79.137.183.0/24
	ufw deny from 94.100.176.0/20
	ufw deny from 95.163.32.0/19
	ufw deny from 95.163.212.0/22
	ufw deny from 95.163.216.0/22
	ufw deny from 95.163.248.0/21
	ufw deny from 128.140.168.0/21
	ufw deny from 178.22.88.0/21
	ufw deny from 178.237.16.0/20
	ufw deny from 178.237.29.0/24
	ufw deny from 185.5.136.0/22
	ufw deny from 185.16.148.0/22
	ufw deny from 185.16.244.0/23
	ufw deny from 185.16.246.0/24
	ufw deny from 185.16.247.0/24
	ufw deny from 188.93.56.0/21
	ufw deny from 194.186.63.0/24
	ufw deny from 195.211.20.0/22
	ufw deny from 195.218.168.0/24
	ufw deny from 217.20.144.0/20
	ufw deny from 217.69.128.0/20
	sudo ufw enable
	
Прокси-сервер для Telegram с поддержкой SOCKS и MTProto запущен, вы восхитительны!
