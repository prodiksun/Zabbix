# Zabbix-Monitoring-GPU

Для чего делается.
У меня сервер с виртуализацией Proxmox, в сервере стоит видеокарта, которая прокинута в ВМ с Windows и вот как раз ее и нужно мониторить.

Необходима запущенная программа Open Hardware Monitor в системе.
https://openhardwaremonitor.org/

В zabbix_agentd.conf

UserParameter=system.sensor[*],powershell.exe C:\OpenHardwareMonitor\system-sensor.ps1 $1 $2 $3 $4

Возможно потребуется в конфиге добавить параметры:

 UnsafeUserParameters=1
 Timeout=15
 AllowKey=system.run[*]

Получение всех датчиков: 

(Get-WmiObject -Namespace Root\OpenHardwareMonitor -Class sensor ) | ft Identifier,name,SensorType,Value

Чтобы скрипт запускался необходимо в powershell под администратором выполнить команду  Set-ExecutionPolicy RemoteSigned с ответом Y.

Дашборд можно сделать по своим желаниям, у меня так для удобства.

![image](https://user-images.githubusercontent.com/47965173/207835388-09bedcc3-956a-43d1-9666-ebaab814c130.png)

