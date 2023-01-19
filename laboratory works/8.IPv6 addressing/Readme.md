# Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах

**Топология**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/%D1%82%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.png)  
**Таблица адресации**  
|Устройство   |  Интерфейс |IPv6-адрес  | Длина префикса  | Шлюз по умолчанию  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
|R1|G0/0/0| 2001:db8: acad :a ::1 | 64 |  - |
|R1|G0/0/1| 2001:db8: acad :1::1 | 64 |  - |
|S1|VLAN 1|2001:db8: acad: 1 ::b | 64 | -  |
|PC-A|NIC|2001:db8: acad :1 ::3 | 64 | fe80::1|
|PC-B|NIC|2001:db8: acad :a ::3 | 64 | fe80::1|  

## Задачи
### Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
### Часть 2. Ручная настройка IPv6-адресов
### Часть 3. Проверка сквозного соединения
  
#### Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
После подключения сети, инициализации и перезагрузки маршрутизатора и коммутатора выполняю следующие действия:  
**Шаг 1. Настройка маршрутизатора.**  
Назначаю имя хоста и настраиваю основные параметры устройства.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/11.png)  
**Шаг 2. Настройка коммутатора.**  
Назначаю имя хоста и настраиваю основные параметры устройства.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/12.png)
#### Часть 2. Ручная настройка IPv6-адресовЧасть 2. Ручная настройка IPv6-адресов
**Шаг 1. Назначаю IPv6-адреса интерфейсам Ethernet на R1.**  
**a.**	Назначаю глобальные индивидуальные IPv6-адреса, указанные в таблице адресации обоим интерфейсам Ethernet на R1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/21a.png)  
**b.**	Введите команду show ipv6 interface brief, чтобы проверить, назначен ли каждому интерфейсу корректный индивидуальный IPv6-адрес.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/21b.png)  
Примечание. Отображаемый локальный адрес канала основан на адресации EUI-64, которая автоматически использует MAC-адрес интерфейса для создания 128-битного локального IPv6-адреса канала.
**c.**	Чтобы обеспечить соответствие локальных адресов канала индивидуальному адресу, вручную ввожу локальные адреса канала на каждом интерфейсе Ethernet на R1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/21c.png)  
Примечание. Каждый интерфейс маршрутизатора относится к отдельной сети. Пакеты с локальным адресом канала никогда не выходят за пределы локальной сети, а значит, для обоих интерфейсов можно указывать один и тот же локальный адрес канала.
**d.**	Использую  команду show ipv6 interface g0/0/0, чтобы убедиться, что локальный адрес связи изменен на fe80::1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/21d.png)  
Отвечаю на вопрос: Какие группы многоадресной рассылки назначены интерфейсу G0/0? FF02::1  FF02::2   FF02::1:FF00:1  
**Шаг 2. Активирую IPv6-маршрутизацию на R1.**  
**a.**	В командной строке на PC-B ввожу команду ipconfig, чтобы получить данные IPv6-адреса, назначенного интерфейсу ПК.
Отвечаю на вопрос: Назначен ли индивидуальный IPv6-адрес сетевой интерфейсной карте (NIC) на PC-B? нет
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/22a.png)  
**b.**	Активирую IPv6-маршрутизацию на R1 с помощью команды IPv6 unicast-routing.  
Примечание. Это позволит компьютерам получать IP-адреса и данные шлюза по умолчанию с помощью функции SLAAC (Stateless Address Autoconfiguration (Автоконфигурация без сохранения состояния адреса)).  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/22b.png)  
**c.**	Теперь, когда R1 входит в группу многоадресной рассылки всех маршрутизаторов, еще раз ввожу команду ipconfig на PC-B. Проверя данные IPv6-адреса.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/22c.png)  
Отвечаю на вопрос:Почему PC-B получил глобальный префикс маршрутизации и идентификатор подсети, которые вы настроили на R1?  потому что мы включили SlAAC который разрешает раздачу адресов   
**Шаг 3. Назначьте IPv6-адреса интерфейсу управления (SVI) на S1.**  
**a.**	Назначьте адрес IPv6 для S1. Также назначьте этому интерфейсу локальный адрес канала.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/23a.png)  
**b.**	Проверьте правильность назначения IPv6-адресов интерфейсу управления с помощью команды show ipv6 interface vlan1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/23b.png)  
**Шаг 4. Назначаю компьютерам статические IPv6-адреса.**  
**a.**	Открываю окно свойства Ethernet для каждого ПК и назначаю адресацию IPv6.   
**b.**	Убеждаюсь, что оба компьютера имеют правильную информацию адреса IPv6. Каждый компьютер должен иметь два глобальных адреса IPv6: один статический и один SLACC  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/24ab.png)  
#### Часть 3. Проверяю сквозное подключение  
**a.**	С PC-A отправляю эхо-запрос на FE80::1. Это локальный адрес канала, назначенный G0/1 на R1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/3a.png)  
**b.**	отправляю эхо-запрос на интерфейс управления S1 с PC-A. Ввожу команду tracert на PC-A, чтобы проверить наличие сквозного подключения к PC-B.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/3b.png)  
**c.**	С PC-B отправляю эхо-запрос на PC-A.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/3c.png)  
**d.**	С PC-B отправляю эхо-запрос на локальный адрес канала G0/0 на R1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/8.IPv6%20addressing/Pics/3d.png)  
Вопросы для повторения  
**1.	Почему обоим интерфейсам Ethernet на R1 можно назначить один и тот же локальный адрес канала — FE80::1?**Каждый интерфейс маршрутизатора находится в отдельной сети    
**2.	Какой идентификатор подсети в индивидуальном IPv6-адресе 2001:db8:acad::aaaa:1234/64?**  2001:db8:acad:
