5) ОЗУ: 1024 МБ Процессор 2 ядра Видеопамять: 4 МБ Сеть: NAT

6) Что бы добавить оперативной памяти и ресурсов процессора, необходимо добавить в файл Vagrantfile в общий блок конфига строчки кода config.vm.provider "virtualbox" do |v| v.memory = 1024 v.cpus = 2 end

7) HISTFILESIZE 1155 line HISTSIZE 1176 line ignoreboth — не записывать команду, которая начинается с пробела, либо команду, которая дублирует предыдущую

8) {} - зарезервированные слова, список команд в отличии от "(...)" исполнятся в текущем инстансе, используется в различных условных циклах, условных операторах, или ограничивает тело функции. Line 343

9)touch {000001..100000}.txt - создаст в текущей директории соответсвющее число фалов, 300000 - создать не удасться, это слишком дилинный список аргументов

10) проверяет условие у -d /tmp и возвращает ее статус (0 или 1)

11) vagrant@vagrant:$ mkdir /tmp/new_path_dir/ vagrant@vagrant:$ cp /bin/bash /tmp/new_path_dir/ vagrant@vagrant:$ type -a bash bash is /usr/bin/bash bash is /bin/bash vagrant@vagrant:$ PATH=/tmp/new_path_dir/:$PATH vagrant@vagrant:~$ type -a bash bash is /tmp/new_path_dir/bash bash is /usr/bin/bash bash is /bin/bash

Возвращает 1, True.

12) at - команда запускается в указанное время batch - запускается когда уровень загрузки системы снизится ниже 1.5

13) vagrant suspend
