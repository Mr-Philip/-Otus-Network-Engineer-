# Лабораторная работа - Настройка протоколов CDP, LLDP и NTP  
Топология  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/Topology.PNG)  
Таблица адресации  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/iptable.PNG)  
## Задачи
**Часть 1. Создание сети и настройка основных параметров устройства**  
**Часть 2. Обнаружение сетевых ресурсов с помощью протокола CDP**  
**Часть 3. Обнаружение сетевых ресурсов с помощью протокола LLDP**  
**Часть 4. Настройка и проверка NTP**  

#### Часть 1. Создание сети и настройка основных параметров устройства
В первой части лабораторной работы вам предстоит создать топологию сети и настроить основные параметры для маршрутизатора и коммутаторов.  
**Шаг 1. Создайте сеть согласно топологии.**  
Подключите устройства, как показано в топологии, и подсоедините необходимые кабели.
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/11.PNG)  
**Шаг 2. Настройте базовые параметры для маршрутизатора.**  
a.	Назначьте маршрутизатору имя устройства.  
b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.  
d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.  
e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.  
f.	Зашифруйте открытые пароли.  
g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.  
h.	Настройка интерфейсов, перечисленных в таблице выше  
i.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/12.PNG)  
**Шаг 3. Настройте базовые параметры каждого коммутатора.**  
a.	Присвойте коммутатору имя устройства.  
b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.  
d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.  
e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.  
f.	Зашифруйте открытые пароли.  
g.	Создайте баннер, который предупреждает всех, кто обращается к устройству, видит баннерное сообщение «Только авторизованные пользователи!».  
h.	Отключите неиспользуемые интерфейсы  
i.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/13S1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/13S2.PNG)  
#### Часть 2. Обнаружение сетевых ресурсов с помощью протокола CDP  
На устройствах Cisco протокол CDP включен по умолчанию. Воспользуйтесь CDP, чтобы обнаружить порты, к которым подключены кабели.  
a.	На R1 используйте соответствующую команду show cdp, чтобы определить, сколько интерфейсов включено CDP, сколько из них включено и сколько отключено.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2a.PNG)  
**Вопрос:  **
Сколько интерфейсов участвует в объявлениях CDP?  **Vlan1 GigabitEthernet0/0/0 GigabitEthernet0/0/1**  

Какие из них активны? **GigabitEthernet0/0/1**  
b.	На R1 используйте соответствующую команду show cdp, чтобы определить версию IOS, используемую на S1.  
Какая версия IOS используется на  S1?**Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2b.PNG)  
c.	На S1 используйте соответствующую команду show cdp, чтобы определить, сколько пакетов CDP было выданных.  
`S1# show cdp traffic`  
`CDP counters : `  
 `       Total packets output: 179, Input: 148 `  
        `Hdr syntax: 0, Chksum error: 0, Encaps failed: 0 `  
       ` No memory: 0, Invalid packet: 0, `  
      `  CDP version 1 advertisements output: 0, Input: 0 `  
`        CDP version 2 advertisements output: 179, Input: 148`  
Вопрос:  
Сколько пакетов имеет выход CDP с момента последнего сброса счетчика? Не работает в CPT  
Из примера в лабораторной  output: 179  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2c.PNG)  
d.	Настройте SVI для VLAN 1 на S1 и S2, используя IP-адреса, указанные в таблице адресации выше. Настройте шлюз по умолчанию для каждого коммутатора на основе таблицы адресов.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2dS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2dS2.PNG)  
e.	На R1 выполните команду show cdp entry S1 .  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2e.PNG)  
**Вопрос:**  
Какие дополнительные сведения доступны теперь? **10.22.0.2**  
f.	Отключить CDP глобально на всех устройствах.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2fR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2fS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/2fS2.PNG)  
#### Часть 3. Обнаружение сетевых ресурсов с помощью протокола LLDP  
На устройствах Cisco протокол LLDP может быть включен по умолчанию.   Воспользуйтесь LLDP, чтобы обнаружить порты, к которым подключены кабели.  
a.	Введите соответствующую команду lldp, чтобы включить LLDP на всех устройствах в топологии.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3aR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3aS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3aS2.PNG)  
b.	На S1 выполните соответствующую команду lldp, чтобы предоставить подробную информацию о S2.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3b.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3bb.PNG)  
Что такое chassis ID  для коммутатора S2? **Mac address**  
c.	Соединитесь через консоль на всех устройствах и используйте команды LLDP, необходимые для отображения топологии физической сети только из выходных данных команды show.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3cR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3cS1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/3cS2.PNG)  
#### Часть 4. Настройка NTP
В части 4 необходимо настроить маршрутизатор R1 в качестве сервера NTP, а маршрутизатор R2 в качестве клиента NTP маршрутизатора R1. Необходимо выполнить синхронизацию времени для Syslog и отладочных функций. Если время не синхронизировано, сложно определить, какое сетевое событие стало причиной данного сообщения.  
**Шаг 1. Выведите на экран текущее время.**  
![]()  
**Шаг 2. Установите время.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/32.%20Network%20design%20and%20management/pics/412.PNG)  
С помощью команды clock set установите время на маршрутизаторе R1. Введенное время должно быть в формате UTC. 
**Шаг 3. Настройте главный сервер NTP.**  
Настройте R1 в качестве хозяина NTP с уровнем слоя 4.
`S1(config)#ntp master 4`  
`S1(config)#ntp update-calendar`  
`S1(config)#ntp server 10.22.0.1 `  
`S2(config)#ntp server 10.22.0.1 `  
**Шаг 4. Настройте клиент NTP.**  
a.	Выполните соответствующую команду на S1 и S2, чтобы просмотреть настроенное время. Запишите текущее время,  в следующей таблице.  
b.	Настройте S1 и S2 в качестве клиентов NTP. Используйте соответствующие команды NTP для получения времени от интерфейса G0/0/1 R1, а также для периодического обновления календаря или аппаратных часов коммутатора.
**Шаг 5. Проверьте настройку NTP**.  
a.	Используйте соответствующую команду show , чтобы убедиться, что S1 и S2 синхронизированы с R1.  
Примечание. Синхронизация метки времени на маршрутизаторе R2 с меткой времени на маршрутизаторе R1 может занять несколько минут.  
b.	Выполните соответствующую команду на S1 и S2, чтобы просмотреть настроенное время и сравнить ранее записанное время.  
![]()  
**Вопрос для повторения**  
Для каких интерфейсов в пределах сети не следует использовать протоколы обнаружения сетевых ресурсов? для внешних интерфейсов в WAN  

