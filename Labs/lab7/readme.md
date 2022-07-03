## Лабораторная работа #7. Развертывание коммутируемой сети с резервными каналами/
------

Топология сети:  
![Топология сети](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab7/Images/Topology.png)  
Используемое ПО: Cisco Packet Tracer 

**Таблица адресации**
| Устройство | Интерфейс  | IP-Адрес |
| ------------- |:------------------:| ----------:|
| S1     | Vlan 1 | 192.168.1.1 | 255.255.255.0 |
| S2     | Vlan 2 |  192.168.1.2  | 255.255.255.0 | 
| S3     | Vlan 3 |   192.168.1.3  | 255.255.255.0 | |


### Часть 1. Настройка топологии и конфигурация основных параметро коммутаторов

#### Шаг 1. Создаём сеть согласно топологии.  
**a.**	Соединяем с помощью Витой Пары следующие узлы:
| Устройство/Порт | Устройство/Порт | 
| ------------- |:------------------:| 
| S1 / Fa0/1     | S2 / Fa0/1    |
| S1 / Fa0/2     | S2 / Fa0/2    | 
| S1 / Fa0/3     | S3 / Fa0/3    | 
| S1 / Fa0/4     | S3 / Fa0/4    | 
| S2 / Fa0/3     | S3 / Fa0/1    |    
| S2 / Fa0/4     | S3 / Fa0/2    | 

#### Шаг 2.Настроим базовые параметры маршрутизатора коммутаторов S1 и S2 и S3
**a.**  На коммутаторе S1 cносим настройки, назначаем пароли для привелигрованного режима, консоли, VTY, настроим интерфейс vlan 1, включим его и введём в транк,  пропишем logging synchronous , и сохраним конфигурацию в файл.

**b.**  На коммутаторе S2 cносим настройки, назначаем пароли для привелигрованного режима, консоли, VTY, настроим интерфейс vlan 1, включим его и введём в транк,  пропишем logging synchronous , и сохраним конфигурацию в файл.

**c.**  На коммутаторе S3 cносим настройки, назначаем пароли для привелигрованного режима, консоли, VTY, настроим интерфейс vlan 1, включим его и введём в транк,  пропишем logging synchronous , и сохраним конфигурацию в файл.

![Консоль1](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab7/Images/console1.png) 

**d.**  Проверяем доступность. Она есть.

![Консоль2](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab7/Images/console2.png)  

### Часть 2. Определение корневого моста

#### Шаг 1. Отключим порты F0/1 и F0/3 на всех коммутаторах	и отобразим данные протокола spanning-tree.

**a.**  Коммутатор S1:

![Консоль3](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab7/Images/console3.png)  

**b.**  Коммутатор S2:

![Консоль4](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab7/Images/console4.png)  

**a.**  Коммутатор S3:

![Консоль5](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab7/Images/console5.png)  


**a.** Создадим Vlan 10, 20, 999, 1000 для S1, назначим интерфейс Vlan 10, назовём каждый Vlan и включим их

![Консоль4](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console4.png)    

**b.** Создадим Vlan 10, 30, 999, 1000 для S2, назначим интерфейс Vlan 10, назовём каждый Vlan и включим их

![Консоль5](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console5.png)   

**c.** Назначим все неиспользуемые порты коммутатора VLAN Parking_Lot на обоих коммутаторах, настроим их для статического режима доступа и деактивируем

![Консоль6](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console6.png)   

#### Шаг 2. Назначим сети VLAN соответствующим интерфейсам коммутатора.

**a.** Назначьте используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настройте их для режима статического доступа.

![Консоль7](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console7.png)   

**b.** Проверим корректность назначения Vlan

![Консоль8](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console8.png)   

### Часть 3. Конфигурация магистрального канала стандарта 802.1Q между коммутаторами

#### Шаг 1. Вручную настроим магистральный интерфейс F0/1 на коммутаторах S1 и S2.

**a.**	Настроим trunk режим на интерфейсах f0/1 обоих коммутаторов 

**b.**	Настроим native на Vlan 1000 обоих коммутаторов 

**с.**	Укажем, что VLAN 10, 20, 30 и 1000 могут проходить по транку.

**d.**  Проверим корректность настройки транка через **show interfaces trunk**. 

![Консоль9](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console9.png)   

#### Шаг 2. Вручную настроим магистральный интерфейс F0/5 на коммутаторе S1.

**a.**	Прведём аналогичную процедуру, что и с F0/1.

**b.**	Проверим корректность настройки транка через **show interfaces trunk**. 

![Консоль10](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console10.png)   

3.1.1. Ответ на вопрос, - **_Что произойдет, если G0/0/1 на R1 будет отключен?:_**  
_Так как мы не настроили интерфейс на G0/0/1, интерфейс коммутатора также отключён_ 

### Часть 4. Настройка маршрутизации между сетями VLAN

#### Шаг 1. Настроим маршрутизатор 

**a.**	Активируем интерфейс G0/0/1 и настроим подинтерфейсы.

![Консоль11](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console11.png)   

**b.**	Проверим корректность настройки сабинтерфейсов через **show interfaces**. 

![Консоль12](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console12.png)   


### Часть 5. Проверим работает ли маршрутизация между VLAN

#### Шаг 1. Пропингуем следующие узлы с PC-A. Все должно быть успешно.

**a.**	С PC-A на шлюз.

**b.**	С PC-A на PC-B. (пинга нет(((((((((((((( )

**c.**	С PC-A на коммутатор S2

![Консоль14](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab6/Images/console14.png)   



