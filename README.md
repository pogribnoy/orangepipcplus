#### Монитор ресурсов
```
armbianmonitor -m
```

#### Настройка проца
```
h3consumption
```

#### Список разделов
```
fdisk -l
```

#### Список дисков
```
df -h
```

#### Размеры разделов
```
free -m
```

#### Разбивка USB HDD
```
fdisk /dev/sda
swap: 1Gb
/home: 130Gb
/var: 10Gb
/tmp: 10Gb
```

#### Форматирование новых разделов
```
mkfs.ext4 /dev/sda2
mkfs.ext4 /dev/sda3
mkfs.ext4 /dev/sda4
```

#### Узнать UUID разделов
```
blkid
```

#### Узнать PID приложения
```
ps axu | grep fanctrl
```

#### Посмотреть, чем используется каталог
```
fuser -cu /tmp
```

#### Фоновые задачи
```
jobs - список
fg [номер задачи] - активировать (foreground)
```

#### Список установленных пакетов
apt list --installed

#### Типовые команды nmap: https://www.shellhacks.com/ru/20-nmap-examples/

#### Перенос /home на новый разделов
1. Добавить в /etc/fstab строки (не заработало, т.к. скорее всего инициализация диска происходит после загрузки):
```
/dev/sda2 /home ext4 defaults,rw 0 1
/dev/sda3 /var ext4 defaults,rw 0 1
/dev/sda4 /tmp ext4 defaults,rw 0 1
```
или строки с UUID (не заработало, т.к. скорее всего инициализация диска происходит после загрузки):
```
UUID=e8d13448-33f9-4192-b325-bc6df5cf4df6 /home ext4 defaults,rw 0 1
```
или в /etc/rc.local строки:
```
mount /dev/sda2 /media/home
mount /dev/sda3 /media/var
mount /dev/sda4 /media/tmp
```
2. Копирование содержимого системных каталогов
```
cp -pdRv /home/* /mnt/new_home
```

#### Перенос SWAP на другой разделов

#### Редактирование подключенной периферии
```
bin2fex /boot/script.bin script.fex
fex2bin script.fex /boot/bin/orangepipcplus.bin
reboot
```

### Установка Samba (шаринг папок)
```
apt install samba
```
http://dmitrysnotes.ru/raspberry-pi-3-organizaciya-setevogo-dostupa-k-fajlam-cherez-samba

### Установка MiniDLNA (раздача медиа-контента)
```
apt install minidlna
```
http://olorg.ru/page/prokachivaem-raspberry-pi-ustanovka-dlna-servera
В файл /etc/sysctl.conf добавить строки
```
#MiniDLNA warning fix:
fs.inotify.max_user_watches = 100000
```

### Установка transmission-daemon (torrent-качалка)
```
apt install transmission-daemon
```
Перезагрузка сервиса без перетирания настроек: invoke-rc.d transmission-daemon reload
Файлы настроек: 
```
/etc/transmission-daemon/settings.json
/root/.config/transmission-daemon/settings.json (этот работает)
```
В настроках должно быть:
```
"watch-dir": "/home/share", 
"watch-dir-enabled": true
"incomplete-dir": "/home/share/incomplete",	
"incomplete-dir-enabled": true,
```
В файл /etc/sysctl.conf добавить строки (для устранения ошибки с выделением памяти):
```
net.core.rmem_max = 4194304
net.core.wmem_max = 1048576
```

### Радиостанции онлайн
http://onradios.ru/

TV32 84-A4-66-47-37-D4 192.168.0.107
TV48 C4-57-6E-76-87-D6 192.168.0.109

### Номиналы сопротивлений:
10
22
47
100
150
200
220
270
330
470
510
680
1k
2k
2k2
3k3
4k7
5k1
6k8
10k
20k
47k
51k
68k
100k
220k
300k
470k
680k
1M
