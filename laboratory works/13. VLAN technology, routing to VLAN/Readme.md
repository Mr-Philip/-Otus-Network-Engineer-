# Лабораторная работа - Внедрение маршрутизации между виртуальными локальными сетями  
Топология  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/%D0%A2%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.png)  
**Таблица адресации**  
|Устройство|Интерфейс|IP-адрес|Маска подсети|Шлюз по умолчанию|
| ------------ | ------------ | ------------ | ------------ | ------------ |
|R1|G0/0/1.10|192.168.10.1|255.255.255.0||
|R1|G0/0/1.20|192.168.20.1|255.255.255.0||
|R1|G0/0/1.30|192.168.30.1|255.255.255.0||
|R1|G0/0/1.1000|—|—|—|
|S1|VLAN 10|192.168.10.11|255.255.255.0|192.168.10.1|
|S2|VLAN 10|192.168.10.12|255.255.255.0|192.168.10.1|
|PC-A|NIC|192.168.20.3|255.255.255.0|192.168.20.1|
|PC-B|NIC|192.168.30.3|255.255.255.0|192.168.30.1|  

**Таблица VLAN**    
|VLAN|Имя|Назначенный интерфейс|
| ------------ | ------------ | ------------ |
|10|Management|S1: VLAN 10 S2: VLAN 10|
|20|Sales|S1: F0/6|
|30|Operations|S2: F0/18|
|999|Parking_Lot|S1:F0/2-4, F0/7-24, G0/1-2 S2:0/2-17, F0/19-24, G0/1-2|
|1000|Native|—|  

## Задачи
#### Часть 1. Создание сети и настройка основных параметров устройства
#### Часть 2. Создание сетей VLAN и назначение портов коммутатора
#### Часть 3. Настройка транка 802.1Q между коммутаторами.
#### Часть 4. Настройка маршрутизации между сетями VLAN
#### Часть 5. Проверка, что маршрутизация между VLAN работает
### Часть 1. Создание сети и настройка основных параметров устройства
В первой части лабораторной работы мне предстоит создать топологию сети и настроить базовые параметры для узлов ПК и коммутаторов.  
**Шаг 1. Создаю сеть согласно топологии.**  
Подключаю устройства, как показано в топологии, и подсоединяю необходимые кабели.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/11.png)
**Шаг 2. Настраиваю базовые параметры для маршрутизатора.**  
a.	Подключаюсь к маршрутизатору с помощью консоли и активирую привилегированный режим EXEC.  
b.	Вхожу в режим конфигурации.  
c.	Назначаю маршрутизатору имя устройства.  
d.	Отключаю поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
e.	Назначаю class в качестве зашифрованного пароля привилегированного режима EXEC.  
f.	Назначаю cisco в качестве пароля консоли и включите вход в систему по паролю.  
g.	Устанавливаю е cisco в качестве пароля виртуального терминала и активируйте вход.  
h.	Шифрую открытые пароли.  
i.	Создаю баннер с предупреждением о запрете несанкционированного доступа к устройству.  
j.	Сохраняю текущую конфигурацию в файл загрузочной конфигурации.  
k.	Настраиваю на маршрутизаторе время.  
**Шаг 3. Настраиваю базовые параметры каждого коммутатора.**  
a.	Присваиваю коммутатору имя устройства.  
b.	Отключаю поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
c.	Назначаю class в качестве зашифрованного пароля привилегированного режима EXEC.  
d.	Назначаю cisco в качестве пароля консоли и включите вход в систему по паролю.  
e.	Устанавливаю cisco в качестве пароля виртуального терминала и активируйте вход.  
f.	Шифрую открытые пароли.  
g.	Создаю баннер с предупреждением о запрете несанкционированного доступа к устройству.  
h.	Настраиваю на коммутаторах время.  
i.	Сохраняю текущей конфигурации в качестве начальной.  
**Шаг 4. Настраиваю узлы ПК.**  
Согласно таблице адресации назначаю ип адреса.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/14.png)  
### Часть 2. Создание сетей VLAN и назначение портов коммутатора
Во второй части я  создаю VLAN, как указано в таблице выше, на обоих коммутаторах. Затем назначаю VLAN соответствующему интерфейсу и проверяю настройки конфигурации.  
**Шаг 1. Создаю сети VLAN на коммутаторах.**  
a.	Создаю и называю необходимые VLAN на каждом коммутаторе из таблицы выше.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/21a.png)  
b.	Настраиваю интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/21b.png)  
c.	Назначаю все неиспользуемые порты коммутатора VLAN Parking_Lot, настраиваю их для статического режима доступа и административно деактивируйте их.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/21c.png)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/21cc.png)  
**Шаг 2. Назначаю сети VLAN соответствующим интерфейсам коммутатора.**  
a.	Назначаю используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настраиваю их для режима статического доступа.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/22a.png)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/22aa.png)  
b.	Убеждаюсь, что VLAN назначены на правильные интерфейсы.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/22b.png)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/22bb.png)  
### Часть 3. Конфигурация магистрального канала стандарта 802.1Q между коммутаторами
В части 3 я вручную настраиваю интерфейс F0/1 как транк.  
**Шаг 1. Вручную настраиваю магистральный интерфейс F0/1 на коммутаторах S1 и S2.**  
a.	Настройка статического транкинга на интерфейсе F0/1 для обоих коммутаторов.
b.	Установливаю native VLAN 1000 на обоих коммутаторах.  
c.	Указываю, что VLAN 10, 20, 30 и 1000 могут проходить по транку.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/31s1.png)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/31s2.png)  
d.	Проверяю транки, native VLAN и разрешенные VLAN через транк.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/31d.png)  
**Шаг 2. Вручную настраиваю магистральный интерфейс F0/5 на коммутаторе S1.**  
a.	Настраиваю интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1. Это транк до маршрутизатора.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/32a.png)  
b.	Сохраняю текущую конфигурацию в файл загрузочной конфигурации.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/32b.png)  
c.	Проверяю транкинг.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/32c.png)  
Отвечаю на вопрос: Что произойдет, если G0/0/1 на R1 будет отключен?
**Если отключить физический интерфейс, то все подчиненные интерфейсы также отключаются**  
### Часть 4. Настройка маршрутизации между сетями VLAN
**Шаг 1. Настриваю маршрутизатор.**  
a.	активирую интерфейс G0/0/1 на маршрутизаторе.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/41a.png)  
b.	Настраиваю подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q. Убеждаюсь, что подинтерфейсу для native VLAN не назначен IP-адрес. Включаю описание для каждого подинтерфейса.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/41b10.png)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/41b20.png)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/41b30.png)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/41b1000.png)  
c.	Убеждаюсь, что вспомогательные интерфейсы работают  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/41c.png)  
### Часть 5. Проверьте, работает ли маршрутизация между VLAN
**Шаг 1. Выполняю следующие тесты с PC-A.**  
a.	Отправьте эхо-запрос с PC-A на шлюз по умолчанию.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/51a.png)  
b.	Отправьте эхо-запрос с PC-A на PC-B.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/51b.png)  
c.	Отправьте команду ping с компьютера PC-A на коммутатор S2.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/51c.png)  
**Шаг 2. Пройдите следующий тест с PC-B**  
В окне командной строки на PC-B выполняю команду tracert на адрес PC-A.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/13.%20VLAN%20technology%2C%20routing%20to%20VLAN/Pics/52.png)  
отвечаю на вопрос:Какие промежуточные IP-адреса отображаются в результатах?**192,168,30,1**  

