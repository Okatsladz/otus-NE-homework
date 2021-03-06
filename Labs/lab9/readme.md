
## Лабораторная работа #9. Конфигурация безопасности коммутатора 
------

Топология сети:  
![Топология сети](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab9/Images/Topology.png)  
Используемое ПО: Cisco Packet Tracer 

**Таблица адресации**
| Устройство | Интерфейс  | IP-Адрес| Маска подсети | 
| ------------- |:---------:| ----------:|----------:|
| R1     | G0/0/1    | 192.168.10.1 |/24 |
| R1     | Loopback 0    | 10.0.1.1 |/24 |
| S1     | VLAN 10 |   192.168.10.201  |/24 |
| S2    | VLAN 10    | 192.168.10.202|/24 |
| PC-A     | NIC |   DHCP  |/24 |
| PC-B     | NIC |   DHCP |/24 |

### Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора

#### Шаг 1. Создаём сеть согласно топологии.  
**a.**	Соединяем с помощью Витой Пары следующие узлы:
| Устройство/Порт | Устройство/Порт | 
| ------------- |:------------------:| 
| PC-A / Fa0/0     | S1 / Fa0/6    | 
| PC-B / Fa0/0     | S1 / Fa0/18    | 
| S1 / Fa0/1     | S2 / F0/1    | 
| R1 / G0/0/1     | S1 / Fa0/5   |   


#### Шаг 2.Настроим базовые параметры маршрутизатора R1 и коммутаторов S1 и S2.
**a.**  Настраиваем R1. Включаем DHCP, настраиваем интерфейсы и доп настройки. 

![Консоль1](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab9/Images/console1.png)    

**b.**  Настраиваем S1 и S2.

![Консоль2](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab9/Images/console2.png)    
 
  
### Часть 2. Настройка сетей VLAN на коммутаторах.

#### Шаг 1. Конфигурируем Vlan 10 на S1 и S2

**a.** Настроим адресанцию на Vlan 10 и назовём его **managment** 

![Консоль3](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console3.png)    

**b.** Настроим транки, использовав native Vlan 333. Также введём неиспользуемые порты в Vlan 999. 

![Консоль4](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console4.png)    

Ответ на вопрос, - **_Какие группы многоадресной рассылки назначены интерфейсу G0/0?:_**  
_FE80::1_

#### Шаг 2. Активируем IPv6-маршрутизацию на R1

**a.**	Настроим PC-B 

2.1.1. Введём команду на PC-B **ipconfig** , чтобы получить данные IPv6-адреса, назначенного интерфейсу ПК.

![Консоль5](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console5.png)  

2.1.2. Ответ на вопрос, - **_Назначен ли индивидуальный IPv6-адрес сетевой интерфейсной карте (NIC) на PC-B?:_**  
_IPv6-адресс, назначенный на PC-B - FE80::260:5CFF:FE5D:753C_  

![Консоль6](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console6.png)  

**b.**  b.	Активируем IPv6-маршрутизацию на R1 с помощью команды **IPv6 unicast-routing.**

2.2.1 Теперь, когда R1 входит в группу многоадресной рассылки всех маршрутизаторов, еще раз введём команду **ipconfig** на PC-B.

![Консоль7](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console7.png)  

2.2.2. Ответ на вопрос, - **_Почему PC-B получил глобальный префикс маршрутизации и идентификатор подсети, которые вы настроили на R1?:_**  
_Маршрутизатор отослал на компьютер данный адрес с помощью SLAAC_  

#### Шаг 3. Назначим IPv6-адреса на S1.

**a.**	Назначим глобальный и локальный адреса на VLAN-1 S1

![Консоль8](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console8.png)  

**b.**	Проверим корректность записанных адресов через **show ipv6 interface vlan 1**.

![Консоль9](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console9.png)  

#### Шаг 4. Назначим статические IPv6-адреса на компьютеры PC-A и PC-B.

**a.**	Назначим статические IPv6-адреса на компьютеры PC-A и PC-B.

**b.**	Убедимся правильность назначения IPv6 адресов, проверив сетевые настройки, вписав ipconfig в cmd обоих компьютеров.

![Консоль10](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console10.png)  

### Часть 3. Проверка сквозного подключения

**a.**	C PC-A проверим доступность R1, пропинговав его локальный адрес.

![Консоль11](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console11.png)  

**b.**	C PC-A проверим доступность S1, пропинговав его адрес.

![Консоль12](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console12.png)  

**с.**	C PC-A введём команду **tracert** до PC-B

![Консоль13](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console13.png)  

**d.**	C PC-B отправим пинг до G0/0/0 R1

![Консоль14](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab4/Images/console14.png)  

#### Ответы на общие вопросы: 

1. Ответ на вопрос, - **_Почему обоим интерфейсам Ethernet на R1 можно назначить один и тот же локальный адрес канала — FE80::1?:_**  	
_Локальный адрес можно назначить интерфейсам одного маршрутизатора_

2. Ответ на вопрос, - **_2.	Какой идентификатор подсети в индивидуальном IPv6-адресе 2001:db8:acad::aaaa:1234/64?_**  	
_0000_
