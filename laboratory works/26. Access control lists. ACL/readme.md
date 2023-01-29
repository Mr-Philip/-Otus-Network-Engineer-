# Лабораторная работа. Настройка и проверка расширенных списков контроля доступа.
Топология  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/%D0%A2%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.PNG)  
Таблица адресации  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D1%8F.PNG)  
Таблица VLAN  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/%D0%B2%D0%BB%D0%B0%D0%BD.PNG)  
#### Задачи
**Часть 1. Создание сети и настройка основных параметров устройства**  
**Часть 2. Настройка и проверка списков расширенного контроля доступа**  
## Часть 1. Создание сети и настройка основных параметров устройства  
**Шаг 1. Создайте сеть согласно топологии.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/11.PNG)  
**Шаг 2. Произведите базовую настройку маршрутизаторов.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/12R1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/12R2.PNG)  
**Шаг 3. Настройте базовые параметры каждого коммутатора.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/13S1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/13S2.PNG)  
## Часть 2. Настройка сетей VLAN на коммутаторах.Часть 2. Настройка сетей VLAN на коммутаторах.
**Шаг 1. Создайте сети VLAN на коммутаторах.**  
a.	Создайте необходимые VLAN и назовите их на каждом коммутаторе из приведенной выше таблицы.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/21aS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/21aS2.PNG)  
b.	Настройте интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации.  
c.	Назначьте все неиспользуемые порты коммутатора VLAN Parking Lot, настройте их для статического режима доступа и административно деактивируйте их.
Примечание. Команда interface range полезна для выполнения этой задачи с помощью необходимого количества команд.   
**Шаг 2. Назначьте сети VLAN соответствующим интерфейсам коммутатора.**  
a.	Назначьте используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настройте их для режима статического доступа.  
b.	Выполните команду show vlan brief, чтобы убедиться, что сети VLAN назначены правильным интерфейсам.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/22bS1.PNG)  
![]([1](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/22bS2.PNG)  
## Часть 3. ·Настройте транки (магистральные каналы).  
**Шаг 1. Вручную настройте магистральный интерфейс F0/1.**  
a.	Измените режим порта коммутатора на интерфейсе F0/1, чтобы принудительно создать магистральную связь. Не забудьте сделать это на обоих коммутаторах.  
b.	В рамках конфигурации транка установите для native vlan значение 1000 на обоих коммутаторах. При настройке двух интерфейсов для разных собственных VLAN сообщения об ошибках могут отображаться временно.  
c.	В качестве другой части конфигурации транка укажите, что VLAN 10, 20, 30 и 1000 разрешены в транке.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/31abcS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/31abcS2.PNG)  
d.	Выполните команду show interfaces trunk для проверки портов магистрали, собственной VLAN и разрешенных VLAN через магистраль.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/31dS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/31dS2.PNG)  
**Шаг 2. Вручную настройте магистральный интерфейс F0/5 на коммутаторе S1.**  
a.	Настройте интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1. Это транк до маршрутизатора.  
b.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.  
c.	Используйте команду show interfaces trunk для проверки настроек транка.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/32abS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/32cS1.PNG)  
## Часть 4. Настройте маршрутизацию.  
**Шаг 1. Настройка маршрутизации между сетями VLAN на R1.**  
a.	Активируйте интерфейс G0/0/1 на маршрутизаторе.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/41aR1.PNG)    
b.	Настройте подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q. Убедитесь, что подинтерфейс для собственной VLAN не имеет назначенного IP-адреса. Включите описание для каждого подинтерфейса.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/41abR1.PNG)  
c.	Настройте интерфейс Loopback 1 на R1 с адресацией из приведенной выше таблицы.   
d.	С помощью команды show ip interface brief проверьте конфигурацию подынтерфейса.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/41dR1.PNG)  
![](1)  
**Шаг 2. Настройка интерфейса R2 g0/0/1 с использованием адреса из таблицы и маршрута по умолчанию с адресом следующего перехода 10.20.0.1**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/42R2.PNG)    
## Часть 5. Настройте удаленный доступ  
**Шаг 1. Настройте все сетевые устройства для базовой поддержки SSH.**  
a.	Создайте локального пользователя с именем пользователя SSHadmin и зашифрованным паролем $cisco123!  
b.	Используйте ccna-lab.com в качестве доменного имени.   
c.	Генерируйте криптоключи с помощью 1024 битного модуля.  
d.	Настройте первые пять линий VTY на каждом устройстве, чтобы поддерживать только SSH-соединения и с локальной аутентификацией.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/51abcdR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/51abcdR2.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/51abcdS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/51abcdS2.PNG)  
**Шаг 2. Включите защищенные веб-службы с проверкой подлинности на R1.**  
a.	Включите сервер HTTPS на R1.  
`R1(config)# ip http secure-server`  
b.	Настройте R1 для проверки подлинности пользователей, пытающихся подключиться к веб-серверу.  
`R1(config)# ip http authentication local`
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/52ab.PNG)  
## Часть 6. Проверка подключения
**Шаг 1. Настройте узлы ПК.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/61PCA.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/61PCB.PNG)  
**Шаг 2. Выполните следующие тесты. Эхозапрос должен пройти успешно.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/62PCA.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/62PCB.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/62PCBSSH.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/62PCBhttp.PNG)   
## Часть 7. Настройка и проверка списков контроля доступа (ACL)  
При проверке базового подключения компания требует реализации следующих политик безопасности:
Политика1. Сеть Sales не может использовать SSH в сети Management (но в  другие сети SSH разрешен).  
`access-list 101 deny tcp 10.40.0.0 0.0.0.255 10.20.0.0 0.0.0.255 eq 22`  
Политика 2. Сеть Sales не имеет доступа к IP-адресам в сети Management с помощью любого веб-протокола (HTTP/HTTPS). Сеть Sales также не имеет доступа к интерфейсам R1 с помощью любого веб-протокола. Разрешён весь другой веб-трафик (обратите внимание — Сеть Sales  может получить доступ к интерфейсу Loopback 1 на R1).  
`access-list 101 deny tcp 10.40.0.0 0.0.0.255 host 172.16.1.1 eq www`    
`access-list 101 deny tcp 10.40.0.0 0.0.0.255 host 172.16.1.1 eq 443`  
`access-list 101 permit ip any any`  
Политика3. Сеть Sales не может отправлять эхо-запросы ICMP в сети Operations или Management. Разрешены эхо-запросы ICMP к другим адресатам.  
`access-list 101 deny icmp 10.40.0.0 0.0.0.255 10.30.0.0 0.0.0.255 echo`  
`access-list 101 deny icmp 10.40.0.0 0.0.0.255 10.20.0.0 0.0.0.255 echo`  
Политика 4: Cеть Operations  не может отправлять ICMP эхозапросы в сеть Sales. Разрешены эхо-запросы ICMP к другим адресатам.  
`access-list 102 deny icmp 10.30.0.0 0.0.0.255 10.40.0.0 0.0.0.255 echo`  
`access-list 102 permit ip any any`  
**Шаг 1. Проанализируйте требования к сети и политике безопасности для планирования реализации ACL.**  
**Шаг 2. Разработка и применение расширенных списков доступа, которые будут соответствовать требованиям политики безопасности.**  
**Шаг 3. Убедитесь, что политики безопасности применяются развернутыми списками доступа.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/73pc-a.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/73pc-b.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/26.%20Access%20control%20lists.%20ACL/pics/73pc-bHTTPS10.PNG)  
