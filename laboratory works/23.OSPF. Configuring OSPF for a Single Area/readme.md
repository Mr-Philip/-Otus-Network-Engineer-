# Лабораторная работа. Настройка протокола OSPFv2 для одной области

**Топология**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/%D0%A2%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.PNG)  
**Таблица адресации**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/%D0%A2%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0%20%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D0%B8.PNG)
## Задачи  
#### Часть 1. Создание сети и настройка основных параметров устройства  
#### Часть 2. Настройка и проверка базовой работы протокола  OSPFv2 для одной области  
#### Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области  
## Часть 1. Создание сети и настройка основных параметров устройства
**Шаг 1. Создайте сеть согласно топологии.**  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/%D1%81%D0%B5%D1%82%D1%8C.PNG)
**Шаг 2. Произведите базовую настройку маршрутизаторов.**  
Настройки выполнены  согласно инструкции. Скриншоты опустил  
**Шаг 3. Настройте базовые параметры каждого коммутатора.**  
Настройки выполнены  согласно инструкции. Скриншоты опустил  
## Часть 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области
**Шаг 1. Настройте адреса интерфейса и базового OSPFv2 на каждом маршрутизаторе.**  
a.	Настройте адреса интерфейсов на каждом маршрутизаторе, как показано в таблице адресации выше.
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21aR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21aR2.PNG)  
b.	Перейдите в режим конфигурации маршрутизатора OSPF, используя идентификатор процесса 56.  
c.	Настройте статический идентификатор маршрутизатора для каждого маршрутизатора (1.1.1.1 для R1, 2.2.2.2 для R2).  
d.	Настройте инструкцию сети для сети между R1 и R2, поместив ее в область 0.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21bcdR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21bcdR2.PNG)  
e.	Только на R2 добавьте конфигурацию, необходимую для объявления сети Loopback 1 в область OSPF 0.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21eR2.PNG)  
f.	Убедитесь, что OSPFv2 работает между маршрутизаторами. Выполните команду, чтобы убедиться, что R1 и R2 сформировали смежность.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21fR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21fR2.PNG)  
**Вопрос:**  
**Какой маршрутизатор является DR?**  R2  
**Какой маршрутизатор является BDR?** R1  
**Каковы критерии отбора?**  В среде с  LAN маршрутизатор с наивысшим идентификатором маршрутизатора выбирается DR. Устройство маршрутизации со следующим значением идентификатора выбирается как маршрутизатор BDR.  
1.Идентификатор задается с помощью команды router-idrid, выполняемой в режиме конфигурации маршрутизатора OSPF Данный метод является рекомендуемым для назначения идентификатора маршрутизатора.  
2.Маршрутизатор выбирает наибольший адрес IPv4 любого из настроенных интерфейсов обратной петли.  
3.Маршрутизатор выбирает наибольший активный адрес IPv4 любого из своих физических интерфейсов.  
  
g.	На R1 выполните команду show ip route ospf, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации. Обратите внимание, что поведение OSPF по умолчанию заключается в объявлении интерфейса обратной связи в качестве маршрута узла с использованием 32-битной маски.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21g.PNG)  
h.	Запустите Ping до  адреса интерфейса R2 Loopback 1 из R1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/21h.PNG)  
## Часть 3. Оптимизация и проверка конфигурации OSPFv2 для одной области  
**Шаг 1. Реализация различных оптимизаций на каждом маршрутизаторе.**  
a.	На R1 настройте приоритет OSPF интерфейса G0/0/1 на 50, чтобы убедиться, что R1 является назначенным маршрутизатором.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/31a.PNG)  
b.	Настройте таймеры OSPF на G0/0/1 каждого маршрутизатора для таймера приветствия, составляющего 30 секунд.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/31bR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/31bR2.PNG)  
c.	На R1 настройте статический маршрут по умолчанию, который использует интерфейс Loopback 1 в качестве интерфейса выхода. Затем распространите маршрут по умолчанию в OSPF. Обратите внимание на сообщение консоли после установки маршрута по умолчанию.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/31c.PNG)  
d.	добавьте конфигурацию, необходимую для OSPF для обработки R2 Loopback 1 как сети точка-точка. Это приводит к тому, что OSPF объявляет Loopback 1 использует маску подсети интерфейса.  
e.	Только на R2 добавьте конфигурацию, необходимую для предотвращения отправки объявлений OSPF в сеть Loopback 1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/31de.PNG)  
f.	Измените базовую пропускную способность для маршрутизаторов. После этой настройки перезапустите OSPF с помощью команды clear ip ospf process . Обратите внимание на сообщение консоли после установки новой опорной полосы пропускания.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/31fR1.PNG)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/31fR2.PNG)  
**Шаг 2. Убедитесь, что оптимизация OSPFv2 реализовалась.**  
a.	Выполните команду show ip ospf interface g0/0/1 на R1 и убедитесь, что приоритет интерфейса установлен равным 50, а временные интервалы — Hello 30, Dead 120, а тип сети по умолчанию — Broadcast  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/32a.PNG)  
b.	На R1 выполните команду show ip route ospf, чтобы убедиться, что сеть R2 Loopback1 присутствует в таблице маршрутизации. Обратите внимание на разницу в метрике между этим выходным и предыдущим выходным. Также обратите внимание, что маска теперь составляет 24 бита, в отличие от 32 битов, ранее объявленных.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/32b.PNG)  
c.	Введите команду show ip route ospf на маршрутизаторе R2. Единственная информация о маршруте OSPF должна быть распространяемый по умолчанию маршрут R1.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/32c.PNG)  
d.	Запустите Ping до адреса интерфейса R1 Loopback 1 из R2. Выполнение команды ping должно быть успешным.  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/laboratory%20works/23.OSPF.%20Configuring%20OSPF%20for%20a%20Single%20Area/pics/32d.PNG)  
**Вопрос:**  
**Почему стоимость OSPF для маршрута по умолчанию отличается от стоимости OSPF в R1 для сети 192.168.1.0/24?** Из за статичного адреса и его стоимости по отношение к адресу по умолчанию в OSPF  
