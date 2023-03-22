# Домашнее задание к занятию «Компьютерные сети. Лекция 2»

### Цель задания

В результате выполнения задания вы:

* познакомитесь с инструментами настройки сети в Linux, агрегации нескольких сетевых интерфейсов, отладки их работы;
* примените знания о сетевых адресах на практике для проектирования сети.


### Инструкция к заданию

1. Создайте .md-файл для ответов на вопросы задания в своём репозитории, после выполнения прикрепите ссылку на него в личном кабинете.
2. Любые вопросы по выполнению заданий задавайте в чате учебной группы или в разделе «Вопросы по заданию» в личном кабинете.


### Дополнительные материалы для выполнения задания

1. [Онлайн-калькулятор сетей](https://calculator.net/ip-subnet-calculator.html).
2. Калькулятор сетей — программа ipcalc (`apt install ipcalc`). Если есть графический интерфейс, то у программы-калькулятора есть инженерный режим, там можно считать и сети.

------

## Задание

1. Проверьте список доступных сетевых интерфейсов на вашем компьютере. Какие команды есть для этого в Linux и в Windows?
#Ответ: ipconfig /all (windows) , ip a , ip link show (linux)
![2023-03-22_11-20-35](https://user-images.githubusercontent.com/123774335/226841927-67963400-a9b3-4bbd-bad9-e824f80ae857.png)

2. Какой протокол используется для распознавания соседа по сетевому интерфейсу? Какой пакет и команды есть в Linux для этого?
```
Для распозования используется протокол lldp и ip.
Утилиты ставиться из пакета lldpd и net-tools

Команды: 
   - lldpcli show neighbors
   - ip neigh show
   ```
   
3. Какая технология используется для разделения L2-коммутатора на несколько виртуальных сетей? Какой пакет и команды есть в Linux для этого? Приведите пример конфига.
Технология называется VLAN (Virtual LAN).
#Ответ:
```
Для разделения на несколько виртуальных сетей используется технология vlan (Virtual LAN).
пакет vlan с командой - vconfig
Пример конфига:
Добавляем vlan с тегом 200, затем выводим командой ifconfig -a список всех интерфейсов:
```
![2023-03-22_11-31-53](https://user-images.githubusercontent.com/123774335/226844554-1c5ec9da-e438-4b6a-86f0-81223bce382d.png)

так же необходимо дать ip-адрес на новый интерфейс "eth0.200"
![2023-03-22_11-37-46](https://user-images.githubusercontent.com/123774335/226846649-848236a2-1cdc-44fb-978d-836bfe1b2859.png)

4. Какие типы агрегации интерфейсов есть в Linux? Какие опции есть для балансировки нагрузки? Приведите пример конфига.
#Ответ: В Linux есть две технологии агрегации (LAG): bonding и teaming.
![2023-03-22_11-40-11](https://user-images.githubusercontent.com/123774335/226847611-0f2cc5e1-b3f5-4e04-a0fb-4036e2e3e03e.png)
```
Config:

vim /etc/network/interfaces 
auto bond0
iface bond0 inet static
	address 10.0.0.5
	gateway 10.0.0.1
	broadcast 10.0.0.255
	netmask 255.255.255.0
	up /sbin/ifenslave bond0 eth1 eth2
	down /sbin/ifenslave -d bond0 eth0 eth1
   ```
5. Сколько IP-адресов в сети с маской /29 ? Сколько /29 подсетей можно получить из сети с маской /24. Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24.
```
/29 - 6 IP адресов
из /24 подсети можно получить 32 подсети /29

Пример - 10.10.10.72/29
```
6. Задача: вас попросили организовать стык между двумя организациями. Диапазоны 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 уже заняты. Из какой подсети допустимо взять частные IP-адреса? Маску выберите из расчёта — максимум 40–50 хостов внутри подсети.
#Ответ:100.64.0.0/26
7. Как проверить ARP-таблицу в Linux, Windows? Как очистить ARP-кеш полностью? Как из ARP-таблицы удалить только один нужный IP?

*В качестве решения отправьте ответы на вопросы и опишите, как они были получены.*

---

## Задание со звёздочкой* 

Это самостоятельное задание, его выполнение необязательно.

 8. Установите эмулятор EVE-ng.
 
[Инструкция по установке](https://github.com/svmyasnikov/eve-ng).

Выполните задания на lldp, vlan, bonding в эмуляторе EVE-ng. 
 
----

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.


### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки.  
 
Обязательными являются задачи без звёздочки. Их выполнение необходимо для получения зачёта и диплома о профессиональной переподготовке.

Задачи со звёздочкой (*) являются дополнительными или задачами повышенной сложности. Они необязательные, но их выполнение поможет лучше разобраться в теме.
