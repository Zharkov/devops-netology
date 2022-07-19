1) ifconfig, ip -br link show, netstat -i, nmcli device status, cat /proc/net/dev
ipconfig, ipscan

anton@anton-Extensa-2520G:~/devops_netology$ ip -br link show
lo               UNKNOWN        00:00:00:00:00:00 <LOOPBACK,UP,LOWER_UP> 
enp2s0           DOWN           a8:1e:84:43:5f:d9 <NO-CARRIER,BROADCAST,MULTICAST,UP> 
wlp3s0           UP             90:cd:b6:7a:d8:bf <BROADCAST,MULTICAST,UP,LOWER_UP> 

2) Neighbor Discovery Protocol, NDP
имеется пакет ndptool, команты monitor и send

3) используется технология VLAN. в Ubuntu имеется пакет vlan. 
Пример: vconfig add eth0 5 (добавить vlan с ID 5 для интерфейса eth0)

пример конфига:
auto eth0.100
iface eth0.100 inet static
address 192.168.1.200
netmask 255.255.255.0
vlan-raw-device eth0

4) Объединение сетевых интерфейсов bonding и teaming
имеется 6 режимов работы 

mode=0 (balance-rr)
Последовательно кидает пакеты, с первого по последний интерфейс.
mode=1 (active-backup)
Один из интерфейсов активен. Если активный интерфейс выходит из строя (link down и т.д.), другой интерфейс заменяет активный.
mode=2 (balance-xor)
Передачи распределяются между интерфейсами на основе формулы ((MAC-адрес источника) XOR (MAC-адрес получателя)) % число интерфейсов. Один и тот же интерфейс работает с определённым получателем. Режим даёт балансировку нагрузки и отказоустойчивость.
mode=3 (broadcast)
Все пакеты на все интерфейсы
mode=4 (802.3ad)
Link Agregation — IEEE 802.3ad, требует от коммутатора настройки.
mode=5 (balance-tlb)
Входящие пакеты принимаются только активным сетевым интерфейсом, исходящий распределяется в зависимости от текущей загрузки каждого интерфейса.
mode=6 (balance-alb)
Тоже самое что 5, только входящий трафик тоже распределяется между интерфейсами. Не требует настройки коммутатора, но интерфейсы должны уметь изменять MAC.

 Пример конфига:
auto bond0
iface bond0 inet static
    address 192.168.1.150
    netmask 255.255.255.0    
    gateway 192.168.1.1
    dns-nameservers 192.168.1.1 8.8.8.8
    dns-search domain.local
        slaves eth0 eth1
        bond_mode 0
        bond-miimon 100
        bond_downdelay 200
        bound_updelay 200

5)
8 адресов
32 подсети
диапазон адресов в первой подсети будет 10.10.10.1-10.10.10.6, где 10.10.10.7 широковещательный

6)
nton@anton-Extensa-2520G:~/devops_netology$ ipcalc -b 100.64.0.0/10 -s 50
Address:   100.64.0.0           
Netmask:   255.192.0.0 = 10     
Wildcard:  0.63.255.255         
=>
Network:   100.64.0.0/10        
HostMin:   100.64.0.1           
HostMax:   100.127.255.254      
Broadcast: 100.127.255.255      
Hosts/Net: 4194302               Class A

1. Requested size: 50 hosts
Netmask:   255.255.255.192 = 26 
Network:   100.64.0.0/26        
HostMin:   100.64.0.1           
HostMax:   100.64.0.62          
Broadcast: 100.64.0.63          
Hosts/Net: 62                    Class A

маска будет /26

7) 

Linux
проверить таблицу: ip neigh
очистить кеш: ip neigh flush
удалить IP: ip neigh delete <IP> dev <INTERFACE>

Windows
проверить таблицу: arp -a
очистить кеш: arg -d *
удалить IP: agr -d <IP>

