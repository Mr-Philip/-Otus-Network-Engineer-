# **Лабораторная работа. Базовая настройка коммутатора **

Топология и Таблица адресации![Топология и Таблица адресации](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/%D0%A2%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.png)

**	Задачи**
##### Часть 1. Проверка конфигурации коммутатора по умолчанию
##### Часть 2. Создание сети и настройка основных параметров устройства
- Настройте базовые параметры коммутатора.
- Настройте IP-адрес для ПК.

##### Часть 3. Проверка сетевых подключений
- Отобразите конфигурацию устройства.
- Протестируйте сквозное соединение, отправив эхо-запрос.
- Протестируйте возможности удаленного управления с помощью Telnet.

### Часть 1. Создание сети и проверка настроек коммутатора по умолчанию.
В первой части лабораторной работы настраиваю топологию сети и проверяю настройку коммутатора по умолчанию.  
**Шаг 1. Создаю сеть согласно топологии.**  
**a. **Подсоединяю консольный кабель, как показано в топологии. На данном этапе не подключаю кабель Ethernet к компьютеру PC-A.  
Согласно примечанию использую Netlab отключая интерфейс F0/6 на коммутаторе S1.  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(a).png)  
**b.**Устанавливаю консольное подключение к коммутатору с компьютера PC-A с помощью Tera Term или другой программы эмуляции терминала.  
Вопрос:  
Почему нужно использовать консольное подключение для первоначальной настройки коммутатора? Почему нельзя подключиться к коммутатору через Telnet или SSH?  
**Потому что без него мы никак не сможем настроить другие подключения и поэтому нельзя подключиться к коммутатору через Telnet или SSH ибо он там не настроен по умолчанию.  **  
**Шаг 2. Проверяю настройку коммутатора по умолчанию.  **  
**a.**	Предположим, что коммутатор не имеет файла конфигурации, сохраненного в энергонезависимой памяти (NVRAM). Консольное подключение к коммутатору с помощью Tera Term или другой программы эмуляции терминала предоставит доступ к командной строке пользовательского режима EXEC в виде Switch>. Ввожу команду **enable**, чтобы войти в привилегированный режим EXEC.  
Убеждаюсь, что на коммутаторе находится пустой файл конфигурации по умолчанию, с помощью команды **show running-config** в привилегированного режима EXEC.
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(b2).png)  
**b.**	Изучая текущий файл running configuration отвечаю на вопросы.  
Вопросы:  
Сколько интерфейсов FastEthernet имеется на коммутаторе 2960?
 **24**  
Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960?
 **2**  
Каков диапазон значений, отображаемых в vty-линиях?
** 0-4, 5-15**  
**c.**	Изучая файл загрузочной конфигурации (startup configuration) который содержится в энергонезависимом ОЗУ (NVRAM) введя команду show startup-config и отвечаю на вопросы.
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(c).png)    
Вопрос:  
Почему появляется это сообщение?  
**startup-config is not present - потому что нет еще записей конфига (чаще всего это сообщение выпадает при заводских настройках)**  
**d.**	Изучаю характеристики SVI для VLAN 1 и отвечаю на вопросы.  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(d).png)
Вопросы:  
Назначен ли IP-адрес сети VLAN 1?
**no ip address**  
Какой MAC-адрес имеет SVI?
**Его нужно настраивать**  
Данный интерфейс включен?
**выключен**  
**e.**	Изучаю IP-свойства интерфейса SVI сети VLAN 1 введя команду #show interface vlan1 .  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(e).png)  
**f.**	Подсоединяю кабель Ethernet компьютера PC-A к порту 6 на коммутаторе Согласно примечанию при использовании Netlab включаю интерфейс F0/6 на коммутаторе S1.  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(f).png)  
Вопрос:  
Какие выходные данные вы видите?  
```
%LINK-5-CHANGED: Interface FastEthernet0/6, changed state to up  
  
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/6, changed state to up  
```
**g.**	Изучаю сведения о версии ОС Cisco IOS на коммутаторе введя команду show version и овтечаю на вопросы.  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(g).png)  
Вопросы:  
Под управлением какой версии ОС Cisco IOS работает коммутатор?
**Version 15.0(2)SE4**  
Как называется файл образа системы?
**C2960-LANBASEK9-M**  
Какой базовый MAC-адрес назначен коммутатору?
**00:E0:B0:E3:98:E3**  
**h.**	Изучаю свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A введя команду  show interface f0/6 и овтечаю на вопросы.  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(h).png)   
Вопросы:  
Интерфейс включен или выключен?
**включен**  
Что нужно сделать, чтобы включить интерфейс?  
**ввести команду no shutdown в режиме конфигурации интерфейса**  
```
Switch#conf
Switch#configure t
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#int
Switch(config)#interface f
Switch(config)#interface fastEthernet 0/6
Switch(config-if)#no shu
Switch(config-if)#no shutdown
Switch(config-if)#
```
Какой MAC-адрес у интерфейса?
** 00:E0:B0:E3:98:E3**  
Какие настройки скорости и дуплекса заданы в интерфейсе? 
** Full-duplex, 100Mb/s**  

i.	Изучаю параметры сети VLAN по умолчанию на коммутаторе введя команду show vlan.
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(i).png)  
Какое имя присвоено сети VLAN 1 по умолчанию? 
default  
Какие порты расположены в сети VLAN 1?
Fa0/1, Fa0/2, Fa0/3, Fa0/4 Fa0/5, Fa0/6, Fa0/7, Fa0/8 Fa0/9, Fa0/10, Fa0/11, Fa0/12 Fa0/13, Fa0/14, Fa0/15, Fa0/16 Fa0/17, Fa0/18, Fa0/19, Fa0/20 Fa0/21, Fa0/22, Fa0/23, Fa0/24  Gig0/1, Gig0/2  
Активна ли сеть VLAN 1?
active  
К какому типу сетей VLAN принадлежит VLAN по умолчанию?
enet  
j.	Изучаю  флеш-память выполняя одну из следующих команд, чтобы изучить содержимое флеш-каталога.  
Switch# show flash   
Switch# dir flash:  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step1(j).png)    
 
Отвечаю на вопрос:  
Какое имя присвоено образу Cisco IOS?
2960-lanbasek9-mz.150-2.SE4.bin  
### Часть 2. Настройка базовых параметров сетевых устройств
Во второй части необходимо будет настроить основные параметры коммутатора и компьютера.  
Шаг 1. Настройте базовые параметры коммутатора.  
**a.**	В режиме глобальной конфигурации копирую следующие базовые параметры конфигурации и вставляю их в файл на коммутаторе S1.  
```
no ip domain-lookup
hostname S1
service password-encryption
enable secret class
banner motd #
Unauthorized access is strictly prohibited. #
```  
**b.**	Назначаю IP-адрес интерфейсу SVI на коммутаторе. Благодаря этому получаю возможность удаленного управления коммутатором.  
c.	Доступ через порт консоли ограничиваю  с помощью пароля. Использую cisco в качестве пароля для входа в консоль в этом задании. Конфигурация по умолчанию разрешает все консольные подключения без пароля. Чтобы консольные сообщения не прерывали выполнение команд, используйте параметр logging synchronous.  
```
S1(config)# line con 0
S1(config-line)# logging synchronous
```  
**d.**	Настраиваю каналы виртуального соединения для удаленного управления (vty), чтобы коммутатор разрешил доступ через Telnet. Если не настроить пароль VTY, будет невозможно подключиться к коммутатору по протоколу Telnet.
Вопрос:
Для чего нужна команда login?
**Включает доступ для удаленного протокола**  
**Шаг 2. Настройте IP-адрес на компьютере PC-A.**  
Назначаю компьютеру IP-адрес и маску подсети в соответствии с таблицей адресации.  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Step2(f).png)
### Часть 3. Проверка сетевых подключений  
В третьей части лабораторной работы мне предстоит проверить и задокументировать конфигурацию коммутатора, протестировать сквозное соединение между компьютером PC-A и коммутатором S1, а также протестировать возможность удаленного управления коммутатором.  
**Шаг 1. Отобразите конфигурацию коммутатора.**  
Использую консольное подключение на компьютере PC-A для отображения и проверки конфигурации коммутатора. Команда show run позволяет постранично отобразить всю текущую конфигурацию. Для пролистывания использую клавишу пробела.  
**a.**	конфигурация приведена ниже.  
```
S1# show run
Building configuration...

Current configuration : 2206 bytes
!
version 15.2
no service pad
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
!
hostname S1
!
boot-start-marker
boot-end-marker
!
enable secret 5 $1$mtvC$6NC.1VKr3p6bj7YGE.jNg0
!
no aaa new-model
system mtu routing 1500 
!
!
no ip domain-lookup
!
<output omitted>
!
interface FastEthernet0/24
 switchport access vlan 99
!
interface GigabitEthernet0/1
 switchport access vlan 99
!
interface GigabitEthernet0/2
 switchport access vlan 99
!
interface Vlan1
 ip address 192.168.1.2 255.255.255.0
!
ip default-gateway 192.168.1.1
ip http server
ip http secure-server
!
banner motd ^C
Unauthorized access is strictly prohibited. ^C
!
line con 0
 password 7 00071A150754
 logging synchronous
 login
line vty 0 4
 password 7 121A0C041104
 login
line vty 5 15
 password 7 121A0C041104
 login
!
end
```  
b.	Проверяю параметры VLAN 1 введя команду. S1# show interface vlan 1  
Какова полоса пропускания этого интерфейса?**MTU 1500 bytes, BW 100000 Kbit, DLY 1000000 usec**  
В каком состоянии находится VLAN 1? Vlan1 is up  
В каком состоянии находится канальный протокол? line protocol is up  
**Шаг 2. Тестирую сквозное соединение, отправив эхо-запрос.**  
![Шаг](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/f18eaa391e5dacc8354e27989fec37525ccf7687/laboratory%20works/iOS%20commands.%20Basic%20device%20configuration/pics/Ping.png)
**a.**	В командной строке компьютера PC-A с помощью утилиты ping проверьте связь сначала с адресом PC-A.  
C:\> ping 192.168.1.10  
**b.**	Из командной строки компьютера PC-A отправьте эхо-запрос на административный адрес интерфейса SVI коммутатора S1.  
C:\> ping 192.168.1.2  
**Шаг 3. Проверяю удаленное управление коммутатором S1.**  
**a.**	Открываю Tera Term  
**b.**	Выберите сервер Telnet и указываю адрес управления SVI для подключения к S1.  Пароль: cisco.  
**c.**	После ввода пароля cisco вы оказываюсь в командной строке пользовательского режима. Для перехода в исполнительский режим EXEC введите команду enable и используйте секретный пароль class.  
**d.**	Сохраняю конфигурацию.  
**e.**	Завершаю сеанс Telnet, введя exit.  
	Вопросы для повторения  
1.	Зачем необходимо настраивать пароль VTY для коммутатора?
Для того чтобы дать доступ для подключения по TELNET  
2.	Что нужно сделать, чтобы пароли не отправлялись в незашифрованном виде?
	service password-encryption  



**	Приложение А. Инициализация и перезагрузка коммутатора**  
a.	Подключаюсь к коммутатору с помощью консоли и вхожу  в привилегированный режим EXEC.  
Открываю окно конфигурации
```
Switch> enable
Switch#
```  
b.	Пользуюсь командой show flash, чтобы определить, были ли созданы сети VLAN на коммутаторе.  
```
Switch# show flash

```  
c.	Если во флеш-памяти обнаруживаю файл vlan.dat, удаляю его.  
```
Switch# delete vlan.dat
Delete filename [vlan.dat]?
```  
d.	Появится запрос о проверке имени файла.  
Будет предложено подтвердить удаление этого файла. Нажимаю клавишу Enter для подтверждения.  
```
Delete flash:/vlan.dat? [confirm]
Switch#
```  
e.	Ввожу команду erase startup-config, чтобы удалить файл загрузочной конфигурации из NVRAM. Появится запрос об удалении конфигурационного файла. Нажимаю клавишу Enter для подтверждения.  
```
Switch# erase startup-config
Erasing the nvram filesystem will remove all configuration files! Продолжить? [confirm]
[OK]
Erase of nvram: complete
Switch#
```  
f.	Перезагружаю коммутатор, чтобы удалить устаревшую информацию о конфигурации из памяти. Затем появится запрос на подтверждение перезагрузки коммутатора. Нажимаю клавишу Enter, чтобы продолжить.  
```
Switch# reload
```  
Proceed with reload? (Команда reload запускается на активном модуле, будет перезагружен весь стек. Продолжить ее выполнение?) [confirm]
Примечание. До перезагрузки коммутатора может появиться запрос о сохранении текущей конфигурации. Ввожу  no и нажимаю клавишу Enter.  
```
System configuration has been modified. Save? [yes/no]: no
```  
g.	После перезагрузки коммутатора появится запрос о входе в диалоговое окно начальной конфигурации. Отвечаю no и нажимаю клавишу Enter.  
```
Would you like to enter the initial configuration dialog? [yes/no]: no
Switch>
```  
