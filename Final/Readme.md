# Защита проекта  
## Тема: «Модернизация локальной сети Дом-интерната с использованием NAT, STP, VLAN, ACL,SSH»  
### Цели проекта  
1. Оптимизация обмена трафиком в сети  
2. Увеличение безопасности сети  
3. Разграничение сетевого трафика делением на подсети  
4. Создание резервных каналов  
5. Ограничить доступ к серверу кроме бухгалтерии и кадров  
6. Ограничить удаленный доступ к сетевым устройствам, кроме администратора  
7. Ограничить выход в интернет для пользователей повысив скорость для тех кому он нужен
### Используемые технологии  
1. VLAN  
2. NAT  
3. SSH  
4. NTP  
5. OSPF  
6. STP  
7. ACL  
#### Топология было
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/%D1%82%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F%20%D0%B1%D1%8B%D0%BB%D0%BE.jpg)  
#### Таблица ip было 
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/%D1%82%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.jpg)  
#### Топология стало  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/%D1%82%D0%BE%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F.jpg)  
#### Таблица ip стало 
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/table%20ip%20vlan_%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0_1.jpg)  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/table%20ip%20vlan_%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0_2.jpg) 
#### Таблица vlan стало  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/vlan.jpg)  
#### Пример настройки маршрутизатора MainR
`en`  
`clock set 12:00:00 Feb 28 2023`  
`conf t`  
`host MainR `  
`service password-encryption`  
`enable secret word`  
`no ip domain-lookup`  
`banner motd #Outsiders are not allowed to enter!!!#`  
`line con 0`  
`logging synchronous`  
`password word`  
`login`  
`line vty 0 4`  
`logging synchronous`  
`password word`  
`login`  
`exit`  
`ntp master  4`  
`interface G0/0/0`  
`description GW `  
`ip address  192.168.10.1 255.255.255.0`  
`no shut`  
`exit`  
`interface G0/0/1`  
`description NAT `  
`ip address  192.168.1.2 255.255.255.0`  
`no shut`  
`exit`  
`ip route 0.0.0.0 0.0.0.0 192.168.1.1`  
`interface G0/0/0.11`  
`description DIRCONCADR`  
`ip address  192.168.11.1 255.255.255.0`  
`encapsulation dot1Q 11`  
`no shut`  
`exit`  
`interface G0/0/0.12`  
`description OT`  
`ip address  192.168.12.1 255.255.255.0`  
`encapsulation dot1Q 12`  
`no shut`  
`exit`  
`interface G0/0/0.13`  
`description Admin`  
`ip address  192.168.13.1 255.255.255.0`  
`encapsulation dot1Q 13`  
`no shut`  
`exit`  
`interface G0/0/0.14`  
`description SD`  
`ip address  192.168.14.1 255.255.255.0`  
`encapsulation dot1Q 14`  
`no shut`  
`exit`  
`interface G0/0/0.15`  
`description ORDIN`  
`ip address  192.168.15.1 255.255.255.0`  
`encapsulation dot1Q 15`  
`no shut`  
`exit`  
`interface G0/0/0.16`  
`description BUH`  
`ip address  192.168.16.1 255.255.255.0`  
`encapsulation dot1Q 16`  
`no shut`  
`exit`  
`interface G0/0/0.17`  
`description HMD`  
`ip address  192.168.17.1 255.255.255.0`  
`encapsulation dot1Q 17`  
`no shut`  
`exit`  
`interface G0/0/0.18`  
`description Food`  
`ip address  192.168.18.1 255.255.255.0`  
`encapsulation dot1Q 18`  
`no shut`  
`exit`  
`interface G0/0/0.44`  
`description Native`  
`encapsulation dot1Q 44`  
`no shut`  
`exit`  
`interface G0/0/0.55`  
`description Management`  
`ip address  192.168.55.1 255.255.255.0`  
`encapsulation dot1Q 55`  
`no shut`  
`exit`  
`access-list 1 permit 192.168.11.0 0.0.0.255`  
`access-list 1 permit 192.168.12.0 0.0.0.255`  
`access-list 1 permit 192.168.18.0 0.0.0.255`  
`ip nat pool PUBLIC 192.168.1.200 192.168.1.204 netmask 255.255.255.0`  
`ip nat inside source list 1 pool PUBLIC`  
`interface g0/0/0`  
`ip nat inside`  
`interface g0/0/1`  
`ip nat outside`  
`exit`  
`Ip ssh version 2`  
`username mdiadmin privilege 15 secret adminmdi`  
`ip domain-name mdi.com`  
`crypto key generate rsa general-keys modulus 1024`  
`line vty 0 4`  
`transport input ssh`  
`login local`  
`exit`  
`exit`  
`copy run start`  
#### Пример настройки коммутатора  
`conf t`  
`host DIRCONCADR`  
`service password-encryption`  
`enable secret word`  
`no ip domain-lookup`  
`banner motd #Outsiders are not allowed to enter!!!#`  
`line con 0`  
`logging synchronous`  
`password cisco`  
`login`  
`line vty 0 15`  
`logging synchronous`  
`password word`  
`login`  
`exit`  
`ntp server  192.168.10.1`  
`ip default-gateway 192.168.10.1`  
`vlan 11`  
`name DIRCONCADR`  
`exit`  
`vlan 12`  
`name OT`  
`exit`  
`vlan 13`  
`name Admin`  
`exit`  
`vlan 14`  
`name SD`  
`exit`  
`vlan 15`  
`name ORDIN`  
`exit`  
`vlan 16`  
`name BUH`  
`exit`  
`vlan 17`  
`name HMD`  
`exit`  
`vlan 18`  
`name Food`  
`exit`  
`vlan 33`  
`name Reserv`  
`exit`  
`vlan 44`  
`name Native`  
`exit`  
`vlan 55`  
`name Management`  
`exit`  
`interface vlan 55`  
`ip address 192.168.55.11 255.255.255.0`  
`exit`  
`interface range fa0/4,fa0/13-14,fa0/16-24,g0/1-2`  
`switchport mode access`  
`switchport access vlan 33`  
`shut`  
`exit`  
`interface range fa0/5,fa0/15`  
`switchport mode trunk`  
`switchport trunk native vlan 44`  
`switchport trunk allowed vlan 11-18,44,55`  
`exit`  
`interface range fa0/1-3, fa0/6-12`  
`switchport mode access`  
`switchport access vlan 11`  
`no shut`  
`exit`  
`Ip ssh version 2`  
`username mdiadmin privilege 15 secret adminmdi`  
`ip domain-name mdi.com`  
`crypto key generate rsa general-keys modulus 1024`  
`line vty 0 15`  
`transport input ssh`  
`login local`  
`exit`  
`exit`  
`copy run start`  
#### Пример STP на Mainsw чтоб трафик шел через Main коммутатор
`interface FastEthernet0/1`  
`switchport trunk native vlan 44`  
`switchport trunk allowed vlan 11-18,44,55`  
`switchport mode trunk`  
`spanning-tree vlan 11-18,44,55 cost 10`  
`interface FastEthernet0/2`  
`switchport trunk native vlan 44`  
`switchport trunk allowed vlan 11-18,44,55`  
`switchport mode trunk`  
`spanning-tree vlan 11-18,44,55 cost 10`  
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/STP.jpg)  
#### Пример пинга до устройства
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/ping.jpg)  
#### Пример удаленного подключения к сетевому устройству
![](https://github.com/Mr-Philip/-Otus-Network-Engineer-/blob/main/Final/Pics/ssh%20.jpg)  
