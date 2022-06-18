## Лабораторная работа #5. Просмотр таблицы MAC-адресов коммутатора  
------

Топология сети:  
![Топология сети](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/Topology.png)  
Используемое ПО: Cisco Packet Tracer 

**Таблица адресации**
| Устройство       | Интерфейс | IP-Адрес | Маска подсети | Шлюз по умолчанию |
| ------------- |:------------------:| -----:|-----:|-----:|
| R1     | G0/0/1   | 198.168.1.1 | 255.255.255.0 | # |
| S1     | VLAN-1 |   192.168.1.11  | 255.255.255.0 | 192.168.1.1 |
| PC-A     | NIC    | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 |


### Часть 1. Настройка основных параметров устройств

#### Шаг 1. Создаём сеть согласно топологии.  
**a.**	Соединяем с помощью Витой Пары следующие узлы:
| Устройство/Порт | Устройство/Порт | 
| ------------- |:------------------:| 
| PC-A / Fa0/1     | S1 / Fa0/6    | 
| S1 / Fa0/5     | R1 / G0/0/1  |   


#### Шаг 2. Настраиваем маршрутизатор. 
**a.**  Сносим настройки, назначаем пароли для привелигрованного режима, консоли, VTY, зашифруем данные пароли.  После настроим интерфейс. Дополнительно создадим motd баннер и сохраним конфигурацию в файл.

![Консоль1](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console 1.png)    

#### Шаг 3. Настроим компьютер и проверим пинг. 

![Консоль2](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console2.png)  

![Консоль3](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console3.png)   
 

### Часть 2. Настройка маршрутизатора для доступа по протоколу SSH

#### Шаг 1. Настроим аутентификацию устройств.

**a.** Зададим имя устройства для R1, а также доменное имя. Создадим ключ шифрования с указанием его длины.


**b.** Создадим учётную запись пользователя **admin** в локальной базе учётных записей

![Консоль4](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console4.png)  

**c.** Настраиваем SSH 

![Консоль5](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console5.png)  

2.1.1 Проверяем работоспособность SSH, подключившись с PC-A на R1

![Консоль6](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console6.png) 

### Часть 3. Настройка коммутатора для доступа по протоколу SSH

**a.**  Сносим настройки, назначаем пароли для привелигрованного режима, консоли, VTY, зашифруем данные пароли.  После настроим Vlan. Дополнительно создадим motd баннер и сохраним конфигурацию в файл.

![Консоль6](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console6.png) 
![Консоль7](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console7.png) 

**b.**  Создадим учётную запись пользователя **admin** в локальной базе учётных записей
![Консоль8](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console8.png) 

**c.** Настраиваем SSH 

![Консоль10](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console10.png) 

2.3.1 Проверяем работоспособность SSH, подключившись с PC-A на S1

![Консоль11](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console11.png) 

### Часть 4. Настройка протокола SSH с использованием интерфейса командной строки коммутатора

**a.**   Установим с коммутатора S1 соединение с маршрутизатором R1 по протоколу SSH.

![Консоль12](https://github.com/Okatsladz/otus-NE-homework/blob/main/Labs/lab5/Images/console12.png)  
#### Ответы на общие вопросы:

1. Ответ на вопрос, - **_Как предоставить доступ к сетевому устройству нескольким пользователям, у каждого из которых есть собственное имя пользователя?:_**  
_Создать локальную базу пользователей через aaa, создать несколько учётных записей, раздать им разный уровень привелегий _  




