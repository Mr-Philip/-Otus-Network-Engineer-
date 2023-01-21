# Лабораторная работа - Конфигурация безопасности коммутатора 

Топология  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/%D0%A2%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.png)  
Таблица адресации  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D1%8F.png)  
#### Задачи  
##### Часть 1. Настройка основного сетевого устройства
•	Создайте сеть.
•	Настройте маршрутизатор R1.
•	Настройка и проверка основных параметров коммутатора
##### Часть 2. Настройка сетей VLAN  
•	Сконфигруриуйте VLAN 10.  
•	Сконфигруриуйте SVI для VLAN 10.  
•	Настройте VLAN 333 с именем Native на S1 и S2.  
•	Настройте VLAN 999 с именем ParkingLot на S1 и S2.  
##### Часть 3: Настройки безопасности коммутатора.
•	Реализация магистральных соединений 802.1Q.  
•	Настройка портов доступа  
•	Безопасность неиспользуемых портов коммутатора  
•	Документирование и реализация функций безопасности порта.  
•	Реализовать безопасность DHCP snooping .  
•	Реализация PortFast и BPDU Guard  
•	Проверка сквозной связанности.  
## Часть 1. Настройка основного сетевого устройства
**Шаг 1. Создаю сеть.**  
a.	Создаю сеть согласно топологии.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/11a.PNG)  
b.	Инициализация устройств  
**Шаг 2. Настройте маршрутизатор R1.**  
a.	Загружаю следующий конфигурационный скрипт на R1.
`enable`
`configure terminal`
`hostname R1`
`no ip domain lookup`
`ip dhcp excluded-address 192.168.10.1 192.168.10.9`
`ip dhcp excluded-address 192.168.10.201 192.168.10.202`
!  
`ip dhcp pool Students`
 `network 192.168.10.0 255.255.255.0`
 `default-router 192.168.10.1`
` domain-name CCNA2.Lab-11.6.1`
!  
`interface Loopback0`
` ip address 10.10.1.1 255.255.255.0`
!  
`interface GigabitEthernet0/0/1`
 `description Link to S1`
 `ip dhcp relay information trusted`
` ip address 192.168.10.1 255.255.255.0`
` no shutdown`
!  
`line con 0`
 `logging synchronous`
` exec-timeout 0 0`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/12a.PNG)
b.	Проверяю текущую конфигурацию на R1, используя следующую команду:  
`R1# show ip interface brief`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/12b.PNG)  
c.	Убеждаюсь, что IP-адресация и интерфейсы находятся в состоянии up / up  
![]()  
**Шаг 3. Настройка и проверка основных параметров коммутатора**  
a.	Настраиваю имя хоста для коммутаторов S1 и S2.    
b.	Запрещаю нежелательный поиск в DNS.  
c.	Настраиваю описания интерфейса для портов, которые используются в S1 и S2.  
d.	Устанавливаю для шлюза по умолчанию для VLAN управления значение 192.168.10.1 на обоих коммутаторах.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/13as1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/13as2.PNG) 
## Часть 2. Настройка сетей VLAN на коммутаторах.  
**Шаг 1. Сконфигруриуйте VLAN 10.**  
Добавляю VLAN 10 на S1 и S2 и называю VLAN - Management.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/21s1.PNG) 
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/21s2.PNG) 
**Шаг 2. Сконфигруриуйте SVI для VLAN 10.**  
Настраиваю IP-адрес в соответствии с таблицей адресации для SVI для VLAN 10 на S1 и S2. Включаю интерфейсы SVI и делаю описание для интерфейса.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/22s1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/22s2.PNG)  
**Шаг 3. Настраиваю VLAN 333 с именем Native на S1 и S2.**   
**Шаг 4. Настраиваю VLAN 999 с именем ParkingLot на S1 и S2.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/234s1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/234s2.PNG)  
## Часть 3. Настройки безопасности коммутатора.
**Шаг 1. Релизация магистральных соединений 802.1Q.**  
a.	Настраиваю все магистральные порты Fa0/1 на обоих коммутаторах для использования VLAN 333 в качестве native VLAN.  
b.	Убеждаюсь, что режим транкинга успешно настроен на всех коммутаторах.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/31bs1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/31bs2.PNG)  
c.	Отключаю согласование DTP F0/1 на S1 и S2.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/31cs1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/31cs2.PNG)  
d.	Проверяю с помощью команды show interfaces.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/31ds1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/31ds2.PNG)  
**Шаг 2. Настройка портов доступа**  
a.	На S1 настраиваю F0/5 и F0/6 в качестве портов доступа и связываю их с VLAN 10.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/32a.PNG)  
b.	На S2 настраиваю порт доступа Fa0/18 и связываю его с VLAN 10.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/32b.PNG)  
**Шаг 3. Безопасность неиспользуемых портов коммутатора**
a.	На S1 и S2 перемещаю неиспользуемые порты из VLAN 1 в VLAN 999 и отключа. неиспользуемые порты.  
b.	Убеждаюсь, что неиспользуемые порты отключены и связаны с VLAN 999, введя команду ` show interfaces status`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/3bs1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/20.Network%20Security%20Principles/pics/3bs2.PNG)  
**Шаг 4. Документирование и реализация функций безопасности порта.**  
Интерфейсы F0/6 на S1 и F0/18 на S2 настроены как порты доступа. На этом шаге настраиваю безопасность портов на этих двух портах доступа.  
a.	На S1, ввожу  команду `show port-security interface f0/6`  для отображения настроек по умолчанию безопасности порта для интерфейса F0/6.  
![]()  
b.	На S1 включаю защиту порта на F0 / 6 со следующими настройками:  
o	Максимальное количество записей MAC-адресов: 3  
o	Режим безопасности: restrict  
o	Aging time: 60 мин.  
o	Aging type: неактивный  
c.	Verify port security on S1 F0/6.  
![]()  
![]()  
d.	Включаю безопасность порта для F0 / 18 на S2. Настраиваю каждый активный порт доступа таким образом, чтобы он автоматически добавлял адреса МАС, изученные на этом порту, в текущую конфигурацию.  
![]()  
e.	Настраиваю следующие параметры безопасности порта на S2 F / 18:  
o	Максимальное количество записей MAC-адресов: 2  
o	Тип безопасности: Protect  
o	Aging time: 60 мин.  
![]()  
f.	Проверяю функции безопасности портов на S2 F0/18.  
![]()  
**Шаг 5. Реализовать безопасность DHCP snooping.**  
a.	На S2 включаю DHCP snooping и настраиваю DHCP snooping во VLAN 10.  
![]()  
b.	Настраиваю магистральные порты на S2 как доверенные порты.  
![]()  
c.	Ограничиваю ненадежный порт Fa0/18 на S2 пятью DHCP-пакетами в секунду.  
![]()  
d.	Проверка DHCP Snooping на S2.  
![]()  
**Шаг 6. Реализация PortFast и BPDU Guard**  
a.	Настраиваю PortFast на всех портах доступа, которые используются на обоих коммутаторах.  
![]()  
b.	Включа. защиту BPDU на портах доступа VLAN 10 S1 и S2, подключенных к PC-A и PC-B.  
![]()  
c.	Убеждаюсь, что защита BPDU и PortFast включены на соответствующих портах.  
![]()  
**Шаг 7. Проверяю наличие сквозного ⁪подключения.**  
![]()  
Проверьте PING свзяь между всеми устройствами в таблице IP-адресации. В случае сбоя проверки связи может потребоваться отключить брандмауэр на хостах.
Закройте окно настройки.
Вопросы для повторения
1.	С точки зрения безопасности порта на S2, почему нет значения таймера для оставшегося возраста в минутах, когда было сконфигурировано динамическое обучение - sticky?
2.	Что касается безопасности порта на S2, если вы загружаете скрипт текущей конфигурации на S2, почему порту 18 на PC-B никогда не получит IP-адрес через DHCP?
3.	Что касается безопасности порта, в чем разница между типом абсолютного устаревания и типом устаревание по неактивности?

