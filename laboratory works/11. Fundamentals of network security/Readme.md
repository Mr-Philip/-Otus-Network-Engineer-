# Лабораторная работа. Доступ к сетевым устройствам по протоколу SSH

**Топология**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/Networkmap.png)  
## 	Задачи  
### Часть 1. Настройка основных параметров устройства  
### Часть 2. Настройка маршрутизатора для доступа по протоколу SSH  
### Часть 3. Настройка коммутатора для доступа по протоколу SSH  
### Часть 4. SSH через интерфейс командной строки (CLI) коммутатора  
## Часть 1. Настройка основных параметров устройств  
В части 1 настраиваю топологию сети и основные параметры, такие как IP-адреса интерфейсов, доступ к устройствам и пароли на маршрутизаторе.  
**Шаг 1. Создаю сеть согласно топологии.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P1S1.png)  
**Шаг 2. Выполняю инициализацию и перезагрузку маршрутизатора и коммутатора.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P1S2.png)  
**Шаг 3. Настраиваю маршрутизатор согласно заданию.**  
a.	Подключаюсь к маршрутизатору с помощью консоли и активирую привилегированный режим EXEC.  
b.	Вхожу в режим конфигурации.  
c.	Отключаю поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
d.	Назначаю class в качестве зашифрованного пароля привилегированного режима EXEC.  
e.	Назначаю cisco в качестве пароля консоли и включаю вход в систему по паролю.  
f.	Назначаю cisco в качестве пароля VTY и включаю вход в систему по паролю.  
g.	Шифрую открытые пароли.  
h.	Создаю баннер, который предупреждает о запрете несанкционированного доступа.  
i.	Настраиваю и активирую на маршрутизаторе интерфейс G0/0/1, используя информацию, приведенную в таблице адресации.  
j.	Сохраняю текущую конфигурацию в файл загрузочной конфигурации.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P1S3.png)  
**Шаг 4. Настраиваю компьютер PC-A.**  
a.	Настраиваю для PC-A IP-адрес и маску подсети.  
b.	Настраиваю для PC-A шлюз по умолчанию.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P1S4.png)  
**Шаг 5. Проверяю подключение к сети.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P1S5.png)  

## Часть 2. Настройка маршрутизатора для доступа по протоколу SSH  
Подключение к сетевым устройствам по протоколу Telnet сопряжено с риском для безопасности, поскольку вся информация передается в виде открытого текста. Протокол SSH шифрует данные сеанса и обеспечивает аутентификацию устройств, поэтому для удаленных подключений рекомендуется использовать именно этот протокол. В части 2 настраиваю маршрутизатор для приема соединений SSH по линиям VTY.
**Шаг 1. Настройте аутентификацию устройств.**  
При генерации ключа шифрования в качестве его части используются имя устройства и домен. Поэтому эти имена необходимо указать перед вводом команды crypto key.  
а. Задаю домен для устройства командой.  
```
R1(config)# ip domain-name ccna-lab.com
```
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P2S1.png)
**Шаг 2. Создаю ключ шифрования с указанием его длины командой.**  
```
R1(config)# crypto key generate rsa  modulus 1024 
The name for the keys will be: R1.ccna-lab.com 
% The key modulus size is 1024 bits 
% Generating 1024 bit RSA keys, keys will be non-exportable... 
[OK] (elapsed time was 1 seconds) 
R1(config)# *Jan 28 21:09:29.867: %SSH-5-ENABLED: SSH 1.99 has been enabled
```
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P2S2.png)  
**Шаг 3. Создаю имя пользователя в локальной базе учетных записей. Настраиваю имя пользователя, используя admin в качестве имени пользователя и adminpass в качестве пароля.**  
```
R1(config)# username admin privilege 15 secret adminpass
```
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P2S3.png)  
**Шаг 4. Активирую протокол SSH на линиях VTY.**  
a.	Активирую протокол SSH на входящих линиях VTY с помощью команды transport input.
```
R1(config)# line vty 0 4 
R1(config-line)# transport input  ssh
```
b.	Изменяю способ входа в систему таким образом, чтобы использовалась проверка пользователей по локальной базе учетных записей.  
```
R1(config-line)# login local 
R1(config-line)# end 
R1#
```
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P2S3.png)  
**Шаг 5. Сохраняю текущую конфигурацию в файл загрузочной конфигурации.**  
```
R1# copy running-config startup-config Destination filename [startup-config]? Building configuration... [OK] 
R1#
```
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P2S3.png)  
**Шаг 6. Устанавливаю соединение с маршрутизатором по протоколу SSH.**  
a.	Запускаю Tera Term с PC-A.  
b.	Устанавливаю SSH-подключение к R1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P2S6.png)  
### Часть 3. Настройка коммутатора для доступа по протоколу SSH  
В части 3 мне  предстоит настроить коммутатор для приема подключений по протоколу SSH, а затем установить SSH-подключение с помощью программы Tera Term.
**Шаг 1. Настройте основные параметры коммутатора.**  
a.	Подключаюсь к коммутатору с помощью консольного подключения и активируйте привилегированный режим EXEC.  
b.	Вхожу в режим конфигурации.  
c.	Отключаю поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
d.	Назначаю class в качестве зашифрованного пароля привилегированного режима EXEC.  
e.	Назначаю cisco в качестве пароля консоли и включаю вход в систему по паролю.  
f.	Назначаю cisco в качестве пароля VTY и включаю вход в систему по паролю.  
g.	Шифрую  открытые пароли.  
h.	Создаю  баннер, который предупреждает о запрете несанкционированного доступа.  
i.	Настраиваю  и активирую  на коммутаторе интерфейс VLAN 1, используя информацию, приведенную в таблице адресации.  
j.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P3S1.png)
**Шаг 2. Настройте коммутатор для соединения по протоколу SSH.**  
Для настройки протокола SSH на коммутаторе использую те же команды, которые применялись для аналогичной настройки маршрутизатора в части 2.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P3S2.png)  
**Шаг 3. Установите соединение с коммутатором по протоколу SSH.**  
Запускаю программу Tera Term на PC-A, затем устанавливаю подключение по протоколу SSH к интерфейсу SVI коммутатора S1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P3S3.png)  
 отвечаю на вопрос:
Удалось ли вам установить SSH-соединение с коммутатором? **Да**  
## Часть 4. Настройка протокола SSH с использованием интерфейса командной строки (CLI) коммутатора  
Клиент SSH встроен в операционную систему Cisco IOS и может запускаться из интерфейса командной строки. В части 4 мне предстоит установить соединение с маршрутизатором по протоколу SSH, используя интерфейс командной строки коммутатора.  

**Шаг 1. Посмотрите доступные параметры для клиента SSH в Cisco IOS.**  
Использую вопросительный знак (?), чтобы отобразить варианты параметров для команды ssh.  
```
S1# ssh?
  -l Log in using this user name
  -v Specify SSH Protocol Version
```  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P4S1.png)  
**Шаг 2. Устанавливаю с коммутатора S1 соединение с маршрутизатором R1 по протоколу SSH.**  
a.	Чтобы подключиться к маршрутизатору R1 по протоколу SSH, ввожу командуssh -l admin 192.168.1.1. Это позволит мне войти в систему под именем admin. При появлении приглашения введите в качестве пароля adminpass  
```  
S1# ssh -l admin 192.168.1.1
Password: 
Authorized Users Only!
R1#
```  
b.	Чтобы вернуться к коммутатору S1, не закрывая сеанс SSH с маршрутизатором R1, нажимаю комбинацию клавиш Ctrl+Shift+6. Отпускаю клавишу Ctrl+Shift+6 и нажимаю x. Отображается приглашение привилегированного режима EXEC коммутатора.  
```
R1#
S1#
```  
c.	Чтобы вернуться к сеансу SSH на R1, нажимаю клавишу Enter в пустой строке интерфейса командной строки. Чтобы увидеть окно командной строки маршрутизатора, нажимаю клавишу Enter еще раз.  
```
S1#
[Resuming connection 1 to 192.168.1.1 ... ]
R1#
```  
d.	Чтобы завершить сеанс SSH на маршрутизаторе R1, ввожу в командной строке маршрутизатора команду exit.  
```
R1# exit
[Connection to 192.168.1.1 closed by foreign host]
S1#
```  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/11.%20Fundamentals%20of%20network%20security/Pics/P4S2.png)  
отвечаю на вопросы.  
Вопрос:
Какие версии протокола SSH поддерживаются при использовании интерфейса командной строки? **Ssh 1 и 2**  
	Вопрос для повторения
Как предоставить доступ к сетевому устройству нескольким пользователям, у каждого из которых есть собственное имя пользователя?
**Нужно настроить доступ по SSH и создать несколько пользователей при помощи команды username.**  
