01)
Добавить переменную $EXTRA_OPTS

vagrant@vagrant:~$ cat /etc/systemd/system/node_exporter.service 
[Unit]
Description=Prometheus Node Exporter
Wants=network-online.target
After=network-online.target
[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter $EXTRA_OPTS
[Install]
WantedBy=multi-user.target

vagrant@vagrant:~$ cat /etc/default/node_exporter
EXTRA_OPTS="--collector.disable-defaults --collector.cpu --collector.meminfo --collector.filesystem --collector.netdev"

systemctl daemon-reload
systemctl enable node_exporter
systemctl start node_exporter
systemctl status node_exporter

Сервис стартует и перезапускается корректно

2)
CPU:
    node_cpu_seconds_total{cpu="0",mode="idle"} 2238.49
    node_cpu_seconds_total{cpu="0",mode="system"} 16.72
    node_cpu_seconds_total{cpu="0",mode="user"} 6.86
    process_cpu_seconds_total
    
Memory:
    node_memory_MemAvailable_bytes 
    node_memory_MemFree_bytes
    
Disk:
    node_disk_io_time_seconds_total{device="sda"} 
    node_disk_read_bytes_total{device="sda"} 
    node_disk_read_time_seconds_total{device="sda"} 
    node_disk_write_time_seconds_total{device="sda"}
    
Network:
    node_network_receive_errs_total{device="eth0"} 
    node_network_receive_bytes_total{device="eth0"} 
    node_network_transmit_bytes_total{device="eth0"}
    node_network_transmit_errs_total{device="eth0"}
3)
после проделанной операции получилось зайти на локалхост
http://localhost:19999/#menu_system;theme=slate

4) Да

vagrant@vagrant:~$ dmesg |grep virtualiz
[    0.003243] CPU MTRRs all blank - virtualized system.
[    0.090015] Booting paravirtualized kernel on KVM
[    6.469126] systemd[1]: Detected virtualization oracle.

на хостовой машине 
anton@anton-Extensa-2520G:~/devops_netology$ dmesg |grep virtualiz
[    0.024329] Booting paravirtualized kernel on bare hardware


5)
vagrant@vagrant:~$ /sbin/sysctl -n fs.nr_open
1048576
Это максимальное число открытых дескрипторов для ядра ,
для пользователя задать больше этого числа нельзя.
Число задается кратное 1024, 1024*1024. 

vagrant@vagrant:~$ cat /proc/sys/fs/file-max
9223372036854775807
мягкий лимит
vagrant@vagrant:~$ ulimit -Sn
1024
жесткий лимит на пользователя
vagrant@vagrant:~$ ulimit -Hn
1048576
Оба ulimit -n не могут превысить системный fs.nr_open


6)
sudo unshare -f --pid --mount-proc sleep 1h
root@vagrant:~# ps aux | grep sleep
root        1808  0.0  0.0   5476   584 pts/0    S    20:26   0:00 sleep 1h
root@vagrant:~# sudo nsenter --target 1808 --pid --mount
root@vagrant:/# ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   5476   584 pts/0    S    20:26   0:00 sleep 1h
root           2  0.0  0.4   7236  4100 pts/0    S    20:27   0:00 -bash
root          13  0.0  0.3   8892  3436 pts/0    R+   20:27   0:00 ps aux

7)
:(){ :|:& };: = это функция, которая порождает себя n-раз, до исчерпания ресурссов системы.
Ограничение максимального числа задач.
По умолчанию TaskMax равен 33%, его можно увеличить в файле /usr/lib/systemd/system/user-.slice.d/10-defaults.conf
