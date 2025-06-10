# Задание 1

Запустите два simple python сервера на своей виртуальной машине на разных портах

Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке

Настройте балансировку Round-robin на 4 уровне.

На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.
 
 ### Запросы 
 
![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/request)

### Config haproxy

![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/haproxy.png)

### Статистика

![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/stats.png)

# Задание 2

Запустите три simple python сервера на своей виртуальной машине на разных портах

Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4

HAproxy должен балансировать только тот http-трафик, который адресован домену example.local

На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.

### Запрос с доменным именем

![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/curl_task2.png)

### Запрос без доменного имени

![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/task2_without_fqns.png)

### Happroxy конфиг

![alt text](https://github.com/Padawan18/Disaster-recovery-and-Keepalived/blob/main/happroxy2.png)
