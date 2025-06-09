# Задание 1

Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.

На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)

Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).

Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.

На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.

 
![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/pic)

Файл   https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/finish.pkt

# Задание 2


Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.

Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах

Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.

Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого 
секцию vrrp_script

На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

### keepalive для главного серввера

```
vrrp_script check_web_server {
       script "./keepalive_script_for_nginx"
       interval 3
}
vrrp_instance VI_1 {
        state MASTER
        interface eth0
        virtual_router_id 15
        priority 255
        advert_int 1


        virtual_ipaddress {
              192.168.0.15/24
        }


        track_process {
                   check_web_server

                }
}

```

### Bash-скрипт

```
#!/bin/bash

if ! nc -z localhost 80; then
    exit 1
fi
if [ ! -f "/var/www/html/index.html" ]; then
    exit 1
fi

exit 0
```


### keepalive для резервного серввера
```
vrrp_instance VI_1 {
        state BACKUP
        interface eth0
        virtual_router_id 15
        priority 200
        advert_int 1


        virtual_ipaddress {
              192.168.0.15/24
        }
}
```
![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/serv1.png)


![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/serv2.png)

### nginx на основном сервере не запущен
![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/nginx.png)
