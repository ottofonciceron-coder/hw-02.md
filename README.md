# Домашнее задание к занятию "Система мониторинга Zabbix" - Марчук Кирилл



### Задание 1 устанавить  Zabbix Server c веб-интерфейсом


1. `Установил PostgreSQL`
2. `Установил Zabbix Server и Zabbix Web Server`
3. `Проверил что всё работает и заходит на zabbix server`


```
sudo apt update
sudo apt install postgresql

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-
release_6.0-4%2Bdebian11_all.deb 
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-
scripts nano -y

su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD
'\'123456789\'';"'

su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf

sudo systemctl restart zabbix-server apache2 # zabbix-agent
sudo systemctl enable zabbix-server apache2 # zabbix-agent
```


![Диагностика сервера zabbix](https://github.com/ottofonciceron-coder/hw-02.md/blob/main/проверка%20zabbix.png)
![Завершение установки и вход](https://github.com/ottofonciceron-coder/hw-02.md/blob/main/zabbixinst.png)

---

### Задание 2 Установка Zabbix Agent на два хоста.



1. `Установил Zabbix Agent на 2 вирт.машины`
2. `Добавил Zabbix Server в список разрешенных серверов своих Zabbix Agentов`
3. `Добавил Zabbix Agentов в раздел Configuration > Hosts своегоZabbix Servera`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `В разделе Latest Data начали появляться данные с добавленных агентов`
6. 

```
wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
sudo dpkg -i zabbix-release_6.4-1+debian11_all.deb
sudo apt update
sudo apt install zabbix-agent -y
sudo nano /etc/zabbix/zabbix_agentd.conf  # редактирование Server, ServerActive, Hostname
sudo systemctl enable zabbix-agent
sudo systemctl restart zabbix-agent
sudo systemctl status zabbix-agent
```


![HOSTS](https://github.com/ottofonciceron-coder/hw-02.md/blob/main/Configuration%20%20Hosts.png)
![логи zabbix agent](https://github.com/ottofonciceron-coder/hw-02.md/blob/main/zabbix%20agent.png)
![Monitoring Latest data 1](https://github.com/ottofonciceron-coder/hw-02.md/blob/main/Monitoring%20%20Latest%20data%201.png)
![Monitoring  Latest data 2](https://github.com/ottofonciceron-coder/hw-02.md/blob/main/Monitoring%20%20Latest%20data%202.png)

---

