# Лабраторная работа - Настройка DHCPv6 

**Топология**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/%D0%A2%D0%BE%D0%BF%D0%BE%D0%BB%D0%B3%D0%B8%D1%8F.PNG)  
**Таблица адресации**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/%D0%A2%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0.PNG)  
### Задачи  
**Часть 1. Создание сети и настройка основных параметров устройства**  
**Часть 2. Проверка назначения адреса SLAAC от R1**  
**Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1**  
**Часть 4. Настройка и проверка состояния DHCPv6 сервера на R1**  
**Часть 5. Настройка и проверка DHCPv6 Relay на R2**  
Часть 1. Создание сети и настройка основных параметров устройства
#### Часть 1. Создание сети и настройка основных параметров устройства  
В первой части лабораторной работы мне предстоит создать топологию сети и настроить базовые параметры для узлов ПК и коммутаторов.
**Шаг 1. Создаю сеть согласно топологии.**  
Подключаю устройства, как показано в топологии, и подсоединяю необходимые кабели. 
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/11.PNG) 
**Шаг 2. Настраиваю базовые параметры каждого коммутатора. (необязательно)**
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/12s1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/12s2.PNG)   
Шаг 3. Произведите базовую настройку маршрутизаторов.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/13r1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/13r2.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/13hr1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/13hr2.PNG)  
#### Часть 2. Проверка назначения адреса SLAAC от R1  
В части 2 я убеждаюсь, что узел PC-A получает адрес IPv6 с помощью метода SLAAC.  
Включаю PC-A и убеждаюсь, что сетевой адаптер настроен для автоматической настройки IPv6.  
Через несколько минут результаты команды ipconfig должны показать, что PC-A присвоил себе адрес из сети 2001:db8:1::/64.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/2.PNG)  
**Отвечаю на вопрос**  
Вопрос: Откуда взялась часть адреса с идентификатором хоста? 
Ответ:с MAC адреса устройства
#### Часть 3. Настройка и проверка сервера DHCPv6 на R1  
В части 3 выполняю настройку и проверку состояния DHCP-сервера на R1. Цель состоит в том, чтобы предоставить PC-A информацию о DNS-сервере и домене.  
**Шаг 1. Более подробно изучаю конфигурацию PC-A.**  
a.	Выполняю команду ipconfig /all на PC-A и смотрю на результат.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/31a.PNG)  
b.	Обращаю внимание, что основной DNS-суффикс отсутствует. Также обращаю внимание, что предоставленные адреса DNS-сервера являются адресами «локального сайта anycast», а не одноадресного адреса, как ожидалось.
**Шаг 2. Настраиваю R1 для предоставления DHCPv6 без состояния для PC-A.**  
a.	Создаю пул DHCP IPv6 на R1 с именем R1-STATELESS. В составе этого пула назначаю адрес DNS-сервера как 2001:db8:acad: :1, а имя домена — как stateless.com.  
Открываю окно конфигурации и ввожу команды  
`R1(config)# ipv6 dhcp pool R1-STATELESS`  
`R1(config-dhcp)# dns-server 2001:db8:acad::254`  
`R1(config-dhcp)# domain-name STATELESS.com` 
![](1)  
b.	Настраиваю интерфейс G0/0/1 на R1, чтобы предоставить флаг конфигурации OTHER для локальной сети R1 и указываю только что созданный пул DHCP в качестве ресурса DHCP для этого интерфейса.  
`R1(config)# interface g0/0/1`  
`R1(config-if)# ipv6 nd other-config-flag `  
`R1(config-if)# ipv6 dhcp server R1-STATELESS`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/32b.PNG)  
c.	Сохраняю текущую конфигурацию в файл загрузочной конфигурации.  
d.	Перезапускаю PC-A.  
e.	Проверяю вывод ipconfig /all и обращаю внимание на изменения.
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/32e.PNG)  
f.	Тестирую подключения с помощью пинга IP-адреса интерфейса G0/1 R2.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/32f.PNG)  
#### Часть 4. Настройка сервера DHCPv6 с сохранением состояния на R1  
В части 4 настраиваю R1 для ответа на запросы DHCPv6 от локальной сети на R2.  
a.	Создаю пул DHCPv6 на R1 для сети 2001:db8:acad:3:aaa::/80. Это предоставит адреса локальной сети, подключенной к интерфейсу G0/0/1 на R2. В составе пула задаю DNS-сервер 2001:db8:acad: :254 и задаю доменное имя STATEFUL.com.Ввожу команды  
`R1(config)# ipv6 dhcp pool R2-STATEFUL`  
`R1(config-dhcp)# address prefix 2001:db8:acad:3:aaa::/80`  
`R1(config-dhcp)# dns-server 2001:db8:acad::254`  
`R1(config-dhcp)# domain-name STATEFUL.com`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/4a.PNG)  
b.	Назначаю только что созданный пул DHCPv6 интерфейсу g0/0/0 на R1.Ввожу команды  
`R1(config)# interface g0/0/0`  
`R1(config-if)# ipv6 dhcp server R2-STATEFUL`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/4b.PNG)  
#### Часть 5. Настройка и проверка ретрансляции DHCPv6 на R2.
В части 5 настраиваю и проверяю ретрансляцию DHCPv6 на R2, позволяя PC-B получать адрес IPv6.  
**Шаг 1. Включаю PC-B и проверяю адрес SLAAC, который он генерирует.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/51.PNG)  
**Шаг 2. Настраиваю R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1.**  
a.	Настраиваю команду ipv6 dhcp relay на интерфейсе R2 G0/0/1, указав адрес назначения интерфейса G0/0/0 на R1. Также настраиваю команду managed-config-flag. Ввожу команды  
`R2 (конфигурация) # интерфейс g0/0/1`  
`R2(config-if)# ipv6 nd managed-config-flag`  
`R2(config-if)# ipv6 dhcp relay destination 2001:db8:acad:2::1 g0/0/0`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/52a.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/52aa.PNG)  
b.	Сохраняю конфигурацию.  
**Шаг 3. Попытка получить адрес IPv6 из DHCPv6 на PC-B.**  
a.	Перезапускаю PC-B.  
b.	Открываю командную строку на PC-B и выполняю команду ipconfig /all и проверяю выходные данные, чтобы увидеть результаты операции ретрансляции DHCPv6.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/53b.PNG)  
c.	Проверяю подключения с помощью пинга IP-адреса интерфейса R0 G0/0/1.
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/18.DHCPv4%2C%20SLAAC%2C%20and%20DHCPv6%20protocols/Pics/53c.PNG)  

