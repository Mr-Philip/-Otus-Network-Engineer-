# Лабораторная работа - Настройка NAT для IPv4

**Топология**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/Topology.PNG)  
**Таблица адресации**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/table%20address.PNG)  
##Цели  
**Часть 1. Создание сети и настройка основных параметров устройства**  
**Часть 2. Настройка и проверка NAT для IPv4**  
**Часть 3. Настройка и проверка PAT для IPv4**  
**Часть 4. Настройка и проверка статического NAT для IPv4.**  

#### Часть 1. Создание сети и настройка основных параметров устройства
**Шаг 1. Подключите кабели сети согласно приведенной топологии.
Подключите устройства в соответствии с топологией и подсоедините соответствующие кабели.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/11.PNG)  
**Шаг 2. Произведите базовую настройку маршрутизаторов.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/12R1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/12R2.PNG)  
**Шаг 3. Настройте базовые параметры каждого коммутатора.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/13S1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/13S2.PNG)  
#### Часть 2. Настройка и проверка NAT для IPv4.  
В части 2 необходимо настроить и проверить NAT для IPv4.
**Шаг 1. Настройте NAT на R1, используя пул из трех адресов 209.165.200.226-209.165.200.228. **  
a.	Настройте простой список доступа, который определяет, какие хосты будут разрешены для трансляции. В этом случае все устройства в локальной сети R1 имеют право на трансляцию.  
`R1(config)# access-list 1 permit 192.168.1.0 0.0.0.255`   
b.	Создайте пул NAT и укажите ему имя и диапазон используемых адресов.
`R1(config)# ip nat pool PUBLIC_ACCESS 209.165.200.226 209.165.200.228 netmask 255.255.255.248 `   
Примечание. Параметр маски сети не является разделителем IP-адресов. Это должна быть правильная маска подсети для назначенных адресов, даже если вы используете не все адреса подсети в пуле.  
c.	Настройте перевод, связывая ACL и пул с процессом преобразования.
`R1(config)# ip nat inside source list 1 pool PUBLIC_ACCESS`  
Примечание: Три очень важных момента. Во-первых, слово «inside» имеет решающее значение для работы такого рода NAT. Если вы опустить его, NAT не будет работать. Во-вторых, номер списка — это номер ACL, настроенный на предыдущем шаге. В-третьих, имя пула чувствительно к регистру.  
d.	Задайте внутренний (inside) интерфейс.  
`R1(config)# interface g0/0/1`  
`R1(config-if)# ip nat inside`  
e.	Определите внешний (outside) интерфейс.  
`R1(config)# interface g0/0/0`  
`R1(config-if)# ip nat outside`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/21R1.PNG)  
**Шаг 2. Проверьте и проверьте конфигурацию. **  
a.	С PC-B,  запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. Если эхо-запрос не прошел, выполните процес поиска и устранения неполадок. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.  
**Вопросы:**  
Во что был транслирован внутренний локальный адрес PC-B? **209.165.200.226**  
Какой тип адреса NAT является переведенным адресом? **Inside global**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22a(pingpc-b%20-%20lo1).PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22a.PNG)  
b.	С PC-A, запустите  эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22b(pingpc-a%20-%20lo1).PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22b.PNG)  
c.	Обратите внимание, что предыдущая трансляция для PC-B все еще находится в таблице. Из S1, эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22c(S1%20-%20lo1).PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22c.PNG)  
d.	Теперь запускаем пинг R2 Lo1 из S2. На этот раз перевод завершается неудачей, и вы получаете эти сообщения (или аналогичные) на консоли R1:  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22d(S2%20-%20lo1).PNG)    
e.	Это ожидаемый результат, потому что выделено только 3 адреса, и мы попытались ping Lo1 с четырех устройств. Напомним, что NAT — это трансляция «один-в-один». Как много выделено трансляций? Введите команду show ip nat translations verbose , и вы увидите, что ответ будет 24 часа.  
**Нет в покет трейсер**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22e.PNG)  
f.	Учитывая, что пул ограничен тремя адресами, NAT для пула адресов недостаточно для нашего приложения. Очистите преобразование NAT и статистику, и мы перейдем к PAT.
`R1# clear ip nat translations *`  
`R1# clear ip nat statistics`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/22f.PNG)  
#### Часть 3. Настройка и проверка PAT для IPv4.  
В части 3 необходимо настроить замену NAT на PAT в пул адресов, а затем на PAT с помощью интерфейса.  
**Шаг 1. Удалите команду преобразования на R1.**  
Компоненты конфигурации преобразования адресов в основном одинаковы; что-то (список доступа) для идентификации адресов, пригодных для перевода, дополнительно настроенный пул адресов для их преобразования и команды, необходимые для идентификации внутреннего и внешнего интерфейсов. Из части 1 наш список доступа (список доступа 1) по-прежнему корректен для сетевого сценария, поэтому нет необходимости воссоздавать его. Мы будем использовать один и тот же пул адресов, поэтому нет необходимости воссоздавать эту конфигурацию. Кроме того, внутренний и внешний интерфейсы не меняются. Чтобы начать работу в части 3, удалите команду, связывающую ACL и пул вместе.  
`R1(config)# no ip nat inside source list 1 pool PUBLIC_ACCESS`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/31.PNG)  
**Шаг 2. Добавьте команду PAT на R1.**  
Теперь настройте преобразование PAT в пул адресов (помните, что ACL и Pool уже настроены, так что это единственная команда, которую нам нужно изменить с NAT на PAT).  
`R1(config)# ip nat inside source list 1 pool PUBLIC_ACCESS overload`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/32.PNG)    
**Шаг 3. Протестируйте и проверьте конфигурацию.**  
a.	Давайте проверим, что PAT работает. С PC-B,  запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/33a(pingpc-b%20-%20lo1).PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/33a.PNG)  
**Вопросы:**  
Во что был транслирован внутренний локальный адрес PC-B? **209.165.200.228**  
Какой тип адреса NAT является переведенным адресом? **Inside global**  
Чем отличаются выходные данные команды show ip nat translations из упражнения NAT? **Используется один внешний адрес**  
b.	С PC-A, запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/33b(pingpc-a%20-%20lo1).PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/33b.PNG)  
c.	Генерирует трафик с нескольких устройств для наблюдения PAT. На PC-A и PC-B используйте параметр -t с командой ping, чтобы отправить безостановочный ping на интерфейс Lo1 R2 (ping -t 209.165.200.1), затем вернитесь к R1 и выполните  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/33c.PNG)  
**Вопрос:**  
Как маршрутизатор отслеживает, куда идут ответы?** присваиваются уникальные номера по портам**  
d.	PAT в пул является очень эффективным решением для малых и средних организаций. Тем не менее есть неиспользуемые адреса IPv4, задействованные в этом сценарии. Мы перейдем к PAT с перегрузкой интерфейса, чтобы устранить эту трату IPv4 адресов. Остановите ping на PC-A и PC-B с помощью комбинации клавиш Control-C, затем очистите трансляции и статистику:  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/33d.PNG)  
**Шаг 4. На R1 удалите команды преобразования nat pool.**  
Опять же, наш список доступа (список доступа 1) по-прежнему корректен для сетевого сценария, поэтому нет необходимости воссоздавать его. Кроме того, внутренний и внешний интерфейсы не меняются. Чтобы начать работу с PAT к интерфейсу, очистите конфигурацию, удалив пул NAT и команду, связывающую ACL и пул вместе.  
`R1(config)# no ip nat inside source list 1 pool PUBLIC_ACCESS overload`  
`R1(config)# no ip nat pool PUBLIC_ACCESS`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/34.PNG)  
**Шаг 5. Добавьте команду PAT overload, указав внешний интерфейс.**  
Добавьте команду PAT, которая вызовет перегрузку внешнего интерфейса.  
`R1(config)# ip nat inside source list 1 interface g0/0/0 overload`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/35.PNG)  
**Шаг 6. Протестируйте и проверьте конфигурацию.**  
a.	Давайте проверим PAT, чтобы интерфейс работал. С PC-B,  запустите эхо-запрос интерфейса Lo1 (209.165.200.1) на R2. Если эхо-запрос не прошел, выполните отладку. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/36a.PNG)  
b.	Сделайте трафик с нескольких устройств для наблюдения PAT. На PC-A и PC-B используйте параметр -t с командой ping для отправки безостановочного ping на интерфейс Lo1 R2 (ping -t 209.165.200.1). На S1 и S2 выполните привилегированную команду exec ping 209.165.200.1 повторить 2000. Затем вернитесь к R1 и выполните команду show ip nat translations.
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/36b.PNG)  
#### Часть 4. Настройка и проверка статического NAT для IPv4.  
В части 4 будет настроена статическая NAT таким образом, чтобы PC-A был доступен напрямую из Интернета. PC-A будет доступен из R2 по адресу 209.165.200.229.
Примечание. Конфигурация, которую вы собираетесь завершить, не соответствует рекомендуемым практикам для шлюзов, подключенных к Интернету. Эта лаборатория полностью опускает стандартные методы безопасности, чтобы сосредоточиться на успешной конфигурации статического NAT. В производственной среде решающее значение для удовлетворения этого требования будет иметь тщательная координация между сетевой инфраструктурой и группами безопасности.  
**Шаг 1. На R1 очистите текущие трансляции и статистику.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/41.PNG)  
**Шаг 2. На R1 настройте команду NAT, необходимую для статического сопоставления внутреннего адреса с внешним адресом.**  
Для этого шага настройте статическое сопоставление между 192.168.1.11 и 209.165.200.1 с помощью следующей команды:  
`R1(config)# ip nat inside source static 192.168.1.2 209.165.200.229`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/42.PNG)  
**Шаг 3. Протестируйте и проверьте конфигурацию.** 
a.	Давайте проверим, что статический NAT работает. На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations, и вы увидите статическое сопоставление.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/43a.PNG)  
b.	Таблица перевода показывает, что статическое преобразование действует. Проверьте это, запустив ping  с R2 на 209.165.200.229. Плинги должны работать.
Примечание. Возможно, вам придется отключить брандмауэр ПК для работы pings.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/43b.PNG)  
c.	На R1 отобразите таблицу NAT на R1 с помощью команды show ip nat translations, и вы увидите статическое сопоставление и преобразование на уровне порта для входящих pings.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/29.NAT%20protocol/pics/43c.PNG)  
Это подтверждает, что статический NAT работает  

