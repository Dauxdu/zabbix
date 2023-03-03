c:\zabbix\zabbix_agentd.exe -c c:\zabbix\zabbix_agentd.conf -i

netsh advfirewall firewall add rule name="Zabbix Agent" dir=in action=allow localport=10050-10051 protocol=TCP enable=yes
