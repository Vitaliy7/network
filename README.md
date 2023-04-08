# network
## Домашнее задание по теме _Архитектура сетей_
> Дано  
> Vagrantfile с начальным построением сети

> inetRouter  
> centralRouter  
> centralServer  

> Планируемая архитектура  

> Сеть office1  
192.168.2.0/26 - dev  
192.168.2.64/26 - test servers  
192.168.2.128/26 - managers  
192.168.2.192/26 - office hardware 

> Сеть office2  
192.168.1.0/25 - dev  
192.168.1.128/26 - test servers  
192.168.1.192/26 - office hardware 

> Сеть central  
192.168.0.0/28 - directors  
192.168.0.32/28 - office hardware  
192.168.0.64/26 - wifi  

> Итого должны получится следующие сервера  
> * inetRouter
> * centralRouter
> * office1Router
> * office2Router
> * centralServer
> * office1Server
> * office2Server  

> Теоретическая часть  

> Найти свободные подсети  
Посчитать сколько узлов в каждой подсети, включая свободные  
Указать broadcast адрес для каждой подсети  
Проверить нет ли ошибок при разбиении   

> Практическая часть  

> Соединить офисы в сеть согласно схеме и настроить роутинг  
Все сервера и роутеры должны ходить в инет через inetRouter  
Все сервера должны видеть друг друга  
У всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи  
При нехватке сетевых интервейсов добавить по несколько адресов на интерфейс  

### Решение ДЗ. 
#### Теоретическая часть.  
Для расчета сетей воспользуемся встроенной утилитой _ipcalc_:  
![](https://github.com/Vitaliy7/network/blob/main/screenshots/central-wifi.png?raw=true)  

Делаем это для всех сетей:  
![](https://github.com/Vitaliy7/network/blob/main/screenshots/central_directors.png?raw=true)
![](https://github.com/Vitaliy7/network/blob/main/screenshots/central_office%20hardware.png?raw=true)
![](https://github.com/Vitaliy7/network/blob/main/screenshots/office1_dev.png?raw=true)  
![](https://github.com/Vitaliy7/network/blob/main/screenshots/office1_managers.png?raw=true)
![](https://github.com/Vitaliy7/network/blob/main/screenshots/office1_office%20hardware.png?raw=true)
![](https://github.com/Vitaliy7/network/blob/main/screenshots/office1_test%20servers.png?raw=true)
![](https://github.com/Vitaliy7/network/blob/main/screenshots/office2_dev.png?raw=true)
![](https://github.com/Vitaliy7/network/blob/main/screenshots/office2_office%20hardware.png?raw=true)
![](https://github.com/Vitaliy7/network/blob/main/screenshots/office2_test%20servers.png?raw=true)  

После выполнения расчета сетей видно, что есть свободные сети:  
192.168.0.16/28  
192.168.0.48/28  
192.168.0.128/25  
192.168.255.64/26  
192.168.255.32/27  
192.168.255.16/28  
192.168.255.8/29  
192.168.255.4/30  

#### Практическая часть.  

Выполняется согласно методички,при помощи _Vagrant+Ansible_. После развертывания виртуальных машин рекомендуется сделать перезагрузку _vagrant reload_.
