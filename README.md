# Порпавка.
Я хотел сделать для каждой лабы свой репозиторий, но потом понял, что это нехорошо. Поэтому во второй лабе будут файлы с 1 и 5 лабой.


МИНОБРНАУКИ РОССИИ
Федеральное государственное бюджетное образовательное учреждение высшего образования

«МИРЭА – Российский технологический университет»
(РТУ МИРЭА)
Институт комплексной безопасности и специального приборостроения

Кафедра КБ-4 «Автоматизированные системы управления»

ОТЧЕТ
по лабораторным работам 1-5

Студент: Тихомиров Кирилл
Группа: ББСО-02-18

Москва, 2020

# Lab_2
## Отчёт по выполнению лабораторной работы номер 2

# Задание 1

К сожалению, я не заскринил настройки ОС в VB, но все було сделано чётко по примеру ( разве что только памяти выделил побольше на всякий )

#### Вот мы и создали ОС
Посмотрим, правильно ли создались диски с помощью fdisk -l
![alt text](Screenshots/Screenshot_1.png "Смотрим Диски")

Также посмотрим диски в системе с помощью lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
![alt text](Screenshots/Screenshot_2.png "")

При установки grub ошибок не вывелось
![alt text](Screenshots/Screenshot_3.png "")

При попытке просмотреть информацию о текущем raid система не находит файл или директорию
![alt text](Screenshots/Screenshot_4.png "")

Также посмотрим информацию о системе с помощью команд pvs, vgs, lvs, mount
![alt text](Screenshots/Screenshot_5.png "")
![alt text](Screenshots/Screenshot_6.png "")
![alt text](Screenshots/Screenshot_7.png "")

## В итоге
Мы создали ОС по указаниям, создали два диска и просмотрели всю необходимую информацию.


# Задание 2
Удаляем один диск в нашей ОС. Перезапускаем машину и проверяем её работоспособность. 
![alt text](Screenshots/Screenshot_9.png "")

Проверяем статус RAID-массива с помощью cat /proc/mdstat
![alt text](Screenshots/Screenshot_10.png "")

Добавляем в интерфейсе VM новый диск такого же размера и называем е его ssd3. Смотрим информацию о дисках
![alt text](Screenshots/Screenshot_11.png "")

Скопируем таблицу разделов со старого диска на новый
![alt text](Screenshots/Screenshot_12.png "")

Смотрим новое состояние дисков
![alt text](Screenshots/Screenshot_13.png "")

Добавим в рейд массив новый диск ( всегда говорит, что не хватает длины, хотя я много раз менял размер)
![alt text](Screenshots/Screenshot_14.png "")

Итоговый результат
![alt text](Screenshots/Screenshot_19.png "")

Выполним синхронизацию разделов, не входящих в RAID
![alt text](Screenshots/Screenshot_17.png "")

Посмотрим состояние дисков 
![alt text](Screenshots/Screenshot_20.png "")

## Итог
Мы удалили один диск, и добавили новый, для восстановления RAID массива. Скапировали данные со старого диска на новый.

# Задание 3

Допустим, у нас случился сбой с диском
![alt text](Screenshots/Screenshot_21.png "")

Добавляем новый диск 
![alt text](Screenshots/Screenshot_22.png "")

Для того, чтобы перенести /boot на новый диск нам сначала нужно установить загрузчик и создать новый RAID массив
![alt text](Screenshots/Screenshot_23.png "")

Настроим LVM/ Создаем новый физический том.
![alt text](Screenshots/Screenshot_24.png "")

Увеличим размер Volume Group system и увилим, что свободное место у md63 увеличилось, но пока var, log и root находятся на sda
![alt text](Screenshots/Screenshot_25.png "")

Перенесем var, log, root на новый диск
![alt text](Screenshots/Screenshot_26.png "")

Перенеслось успешно
![alt text](Screenshots/Screenshot_27.png "")

На диске sda не осталось смонтированных элементов
![alt text](Screenshots/Screenshot_28.png "")

Удаляем диск и добавиляем 1 SSD и 2 HDD
![alt text](Screenshots/Screenshot_29.png "")

Востановим RAID массив
![alt text](Screenshots/Screenshot_30.png "")

Перенесем загрузочный раздел со старого диска на новый
![alt text](Screenshots/Screenshot_31.png "")

Увеличиваем размер второго раздела
![alt text](Screenshots/Screenshot_32.png "")

Расширим размер RAID (размер md127 увеличился)
![alt text](Screenshots/Screenshot_33.png "")

Разер LV не изменился
![alt text](Screenshots/Screenshot_34.png "")

Распределим место между разделами
![alt text](Screenshots/Screenshot_35.png "")

Создадим новый RAID массив, там создадим новый PV, в нем создадим группу и дадим все свободное простанство. 
![alt text](Screenshots/Screenshot_36.png "")

Отформатируем раздел в ex4
![alt text](Screenshots/Screenshot_37.png "")

Выполним синхронизацию и увидим, что у нас все получилось
![alt text](Screenshots/Screenshot_38.png "")

В конце мы перезагрузим нашу ВМ и убедимся, что у нас все работает.
![alt text](Screenshots/Screenshot_39.png "")
