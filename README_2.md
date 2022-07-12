1) CD -> chdir("/tmp")

2) 
openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3

stat("/home/vagrant/.magic.mgc", 0x7ffe5564c7b0) = -1 ENOENT (No such file or directory)
stat("/home/vagrant/.magic", 0x7ffe5564c7b0) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/magic.mgc", O_RDONLY) = -1 ENOENT (No such file or directory)
stat("/etc/magic", {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
openat(AT_FDCWD, "/etc/magic", O_RDONLY) = 3

3) vagrant@vagrant:~$ echo '' >/proc/1126/fd/4


4) Зомби процессы не занимают ресурсы в ОС
но блокируют записи в таблице процессов

5) root@vagrant:~# /usr/sbin/opensnoop-bpfcc
PID    COMM               FD ERR PATH
820    vminfo              5   0 /var/run/utmp
631    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
631    dbus-daemon        20   0 /usr/share/dbus-1/system-services
631    dbus-daemon        -1   2 /lib/dbus-1/system-services
631    dbus-daemon        20   0 /var/lib/snapd/dbus-1/system-services/

6) системный вызов uname()

Part of the utsname information is also accessible  via  /proc/sys/ker‐
       nel/{ostype, hostname, osrelease, version, domainname}.

7) 
&& -  условный оператор, 
а ;  - разделитель последовательных команд

test -d /tmp/some_dir && echo Hi  echo  отработает при успешном завершении test

8) -e прерывает выполнение исполнения при ошибке любой команды кроме последней в последовательности 
-x вывод трейса простых команд 
-u неустановленные/не заданные параметры и переменные считаются как ошибки, с выводом в stderr текста ошибки и выполнит завершение неинтерактивного вызова
-o pipefail возвращает код возврата набора/последовательности команд, ненулевой при последней команды или 0 для успешного выполнения команд.

для сценария, повышает деталезацию вывода ошибоки и завершит сценарий при наличии ошибок, на любом этапе выполнения сценария, кроме последней завершающей команды

9) часто встречающийся S (interruptible sleep (waiting for an event to complete)

Дополнительные символы к основной букве выводят расширенную информацию о процессе (приоритет процесса, имеет заблокированные страницы в памяти и др.)
