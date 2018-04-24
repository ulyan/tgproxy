# Настройка прокси-сервера Dante под Telegram ![Fuck RKN!](https://img.shields.io/badge/Fuck-RKN-brightgreen.svg)

## Ubuntu 16.04

**Обновляем систему и устанавливаем необходимые пакеты:**

	sudo apt-get -y update && apt-get -y upgrade
	sudo apt-get install -y gcc build-essential libwrap0 libwrap0-dev libpam0g-dev make nano wget tar gzip ufw

**Загружаем и компилируем Dante:**

	cd /opt
	wget http://www.inet.no/dante/files/dante-1.4.2.tar.gz
	tar -xvf dante-1.4.2.tar.gz
	cd dante-1.4.2/
	mkdir /opt/dante
	./configure --prefix=/opt/dante
	make && make install
	
**Загружаем конфиг для Telegram:**

	wget -c http://tvoridob.ro/tgproxy/sockd.conf -O /etc/sockd.conf

**Узнаем сетевой интерфейс и вписываем его в конфиг, в большинстве случаев ничего менять не придется:**

	ifconfig
	nano /etc/sockd.conf

**Запускаем прокси-сервер:**

	/opt/dante/sbin/sockd -D -f /etc/sockd.conf

**Останавливается он этой командой:**

	/usr/bin/pkill sockd
	
**Закрываем на сервере все порты кроме 22 (ssh) и 1080 (прокси):**

	sudo ufw allow 1080/tcp
	sudo ufw allow 22/tcp

**Закрываем доступ для сетей Mail.ru (https://t.me/zatelecom/4773):**

	sudo ufw deny proto tcp from 5.61.16.0/21 to any port 1080
	sudo ufw deny proto tcp from 5.61.232.0/21 to any port 1080 
	sudo ufw deny proto tcp from 79.137.157.0/24 to any port 1080
	sudo ufw deny proto tcp from 79.137.174.0/23 to any port 1080
	sudo ufw deny proto tcp from 79.137.183.0/24 to any port 1080
	sudo ufw deny proto tcp from 94.100.176.0/20 to any port 1080
	sudo ufw deny proto tcp from 95.163.32.0/19 to any port 1080
	sudo ufw deny proto tcp from 95.163.212.0/22 to any port 1080
	sudo ufw deny proto tcp from 95.163.216.0/22 to any port 1080
	sudo ufw deny proto tcp from 95.163.248.0/21 to any port 1080
	sudo ufw deny proto tcp from 128.140.168.0/21 to any port 1080
	sudo ufw deny proto tcp from 178.22.88.0/21 to any port 1080
	sudo ufw deny proto tcp from 178.237.16.0/20 to any port 1080
	sudo ufw deny proto tcp from 178.237.29.0/24 to any port 1080
	sudo ufw deny proto tcp from 185.5.136.0/22 to any port 1080
	sudo ufw deny proto tcp from 185.16.148.0/22 to any port 1080
	sudo ufw deny proto tcp from 185.16.244.0/23 to any port 1080
	sudo ufw deny proto tcp from 185.16.246.0/24 to any port 1080
	sudo ufw deny proto tcp from 185.16.247.0/24 to any port 1080
	sudo ufw deny proto tcp from 188.93.56.0/21 to any port 1080
	sudo ufw deny proto tcp from 194.186.63.0/24 to any port 1080
	sudo ufw deny proto tcp from 195.211.20.0/22 to any port 1080
	sudo ufw deny proto tcp from 195.218.168.0/24 to any port 1080
	sudo ufw deny proto tcp from 217.20.144.0/20 to any port 1080
	sudo ufw deny proto tcp from 217.69.128.0/20 to any port 1080
	sudo ufw deny proto tcp from 109.70.27.44 to any port 1080
	sudo ufw enable
	
**Убираемся за собой:**

	rm /opt/dante-1.4.2.tar.gz
	rm -r /opt/dante-1.4.2/

Прокси-сервер для Telegram запущен и работает на 1080 порту, вы восхитительны!
