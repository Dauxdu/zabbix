#### Install zabbix

wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
apt update 

apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent

wget https://repo.mysql.com/mysql-apt-config_0.8.24-1_all.deb
dpkg -i mysql-apt-config_0.8.24-1_all.deb
apt update
apt install mysql-server

mysql -u root -p

create database zabbix character set utf8mb4 collate utf8mb4_bin;
create user zabbix@localhost identified by 'Dimmed6';
grant all privileges on zabbix.* to zabbix@localhost;
flush privileges;
set global log_bin_trust_function_creators = 1;
quit;

zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -u zabbix -p zabbix 

mysql -uroot -p
set global log_bin_trust_function_creators = 0;
quit; 

Отредактируйте файл /etc/zabbix/zabbix_server.conf 
DBPassword=Dimmed6

systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2

sudo apt install -y locales
sudo locale-gen en_US.UTF-8

#### Windows agent config

c:\zabbix\zabbix_agentd.exe -c c:\zabbix\zabbix_agentd.conf -i

netsh advfirewall firewall add rule name="Zabbix Agent" dir=in action=allow localport=10050-10051 protocol=TCP enable=yes


#### Linux temperature
UserParameter=cpu-t.core.package,sensors coretemp-isa-00000 | grep 'Package' | awk -F'[:+°]' | cut -c17-20
UserParameter=cpu-t.core0,sensors coretemp-isa-00000 | grep 'Core 0:' | cut -c17-20

https://sevo44.ru/monitoring-temperatury-v-zabbix/
https://sevo44.ru/zabbix-agent-ustanovka-i-nastrojka/#_zabbix_get
https://sevo44.ru/monitoring-temperatury-v-zabbix/#zabbix_server_work

sensors -u coretemp-isa-0000
nano /etc/sensors.d/*file*
chip "coretemp-isa-0000"
  label temp2 "Core 0"
  label temp3 "Core 1"
  label temp11 "Core 2"
  label temp12 "Core 3"
