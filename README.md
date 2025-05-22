#**Задание 1
Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Команды:

1.wget https://repo.zabbix.com/zabbix/7.2/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.2+ubuntu24.04_all.deb

2.dpkg -i zabbix-release_latest_7.2+ubuntu24.04_all.deb

3.apt update

4.apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent

5.sudo -u postgres createuser --pwprompt zabbix

6.sudo -u postgres createdb -O zabbix zabbix

7.zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

8.nano /etc/zabbox/zabbix_server.conf

9.DBPassword=password

10.systemctl restart zabbix-server zabbix-agent apache2
 
11.systemctl enable zabbix-server zabbix-agent apache2


![ 1](https://github.com/Padawan18/zabbix/blob/main/Рисунок1.png)

#**Задание 2
Установите Zabbix Agent на два хоста.
Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Команды:
1. wget https://repo.zabbix.com/zabbix/7.2/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.2+ubuntu24.04_all.deb

2. dpkg -i zabbix-release_latest_7.2+ubuntu24.04_all.deb
 
3. apt update
 
4. apt install zabbix-agent
 
5. nano /etc/zabbix/zabbix_agentd.conf

6. systemctl restart zabbix-agent
 
7. systemctl enable zabbix-agent
 
![ указание активного сервера zabbix](https://github.com/Padawan18/zabbix/blob/main/Рисунок2.png)

 ![указание серверов](https://github.com/Padawan18/zabbix/blob/main/Рисунок3.png )
   
 ![проверка статуса агента](https://github.com/Padawan18/zabbix/blob/main/Рисунок4.png)
  
  ![логи заббикс агента]( https://github.com/Padawan18/zabbix/blob/main/Рисунок5.png)
  
  ![список хостов](  https://github.com/Padawan18/zabbix/blob/main/Рисунок6.png)
 



 


