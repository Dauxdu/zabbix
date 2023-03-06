c:\zabbix\zabbix_agentd.exe -c c:\zabbix\zabbix_agentd.conf -i

netsh advfirewall firewall add rule name="Zabbix Agent" dir=in action=allow localport=10050-10051 protocol=TCP enable=yes

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
