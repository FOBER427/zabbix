# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Хомяков Антон`

### Задание 1

Установка Zabbix Server, Frontend, Agent2 и PostgreSQL 15:

```
wget https://repo.zabbix.com/zabbix/7.2/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.2+debian12_all.deb
sudo dpkg -i zabbix-release_latest_7.2+debian12_all.deb
sudo apt update

sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent2

sudo apt install postgresql

sudo systemctl is-active postgresql

sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix

zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

sudo sed 's/old_string/new_string/g' file_name

sudo sed -i '/# DBPassword=/a DBPassword=zbxdb' /etc/zabbix/zabbix_server.conf

sudo systemctl restart zabbix-server zabbix-agent2 apache2
sudo systemctl enable zabbix-server zabbix-agent2 apache2
```

Экран настройки в Web UI Zabbix:
![Скриншот 1](/images/1.png)

Экран после входа со стандартными Credentials Admin/zabbix:
![Скриншот 2](/images/2.png)

---

### Задание 2

# Zabbix Agent Setup – Homework

## Configuration > Hosts
![Configuration - Hosts](images/1.png)

## Monitoring > Latest data
![Monitoring - Latest Data](images/2.png)

## Agent metrics overview
![Agent Metrics](images/3.png)

## Zabbix Agent Log
![Zabbix Agent Log](images/4.png)

## Second Host – Configuration > Hosts
![Second Host - Configuration](images/5.png)

## Second Host – Latest Data
![Second Host - Latest Data](images/6.png)

## Second Host – Metrics
![Second Host - Metrics](images/7.png)

## Second Host – Zabbix Agent Log
![Second Host - Agent Log](images/8.png)


Список команд для установки и конфигурирования Zabbix Agent:
```
wget https://repo.zabbix.com/zabbix/7.2/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.2+debian12_all.deb
sudo dpkg -i zabbix-release_latest_7.2+debian12_all.deb
sudo apt update

sudo apt install zabbix-agent

sudo sed -i 's/Server=127.0.0.1/Server=192.168.56.112/g' /etc/zabbix/zabbix_agentd.conf
sudo sed -i 's/ServerActive=127.0.0.1/ServerActive=192.168.56.113/g' /etc/zabbix/zabbix_agentd.conf
sudo sed -i 's/Hostname=Zabbix server/Hostname=zbx-host01/g' /etc/zabbix/zabbix_agentd.conf

sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
```
