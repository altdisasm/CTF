# Container as a real drive

## TASK

Файл: [Vera](/NevaCTF-2022/Container_as_a_real_drive/files/MemeContainer)

К нам на экспертизу попал крипто контейнер. Думали, что TrueCrypt, а нет. Кое-что поновее :). Эксперт смонтировал, пароль кстати был смешной: qwe123qwe. И... ничего не нашел. Думаю, что ты мог/могла бы поискать получше, все-таки была пяница и эксперт торопился домой...

## WRITEUP

Название задания - отсылка к факту, что крипто контерйнеры не зависимо от операционной системы после монтирования представляют собой ничем не отличающийся от обычного логический раздел, соответственно:
- могут иметь таблицу разделов;
- имеют файловую систему.

Из условия видим, что имеется крипто контейнер, созданный чем-то новее TrueCrypt. Тут напрашиваются очевидные вещи, т.к. после опубликованного свидетельства канарейки ([тык](https://www.opennet.ru/opennews/art.shtml?num=40008 "В обращении о закрытии TrueCrypt нашли скрытое предупреждение о причастности АНБ")), на замену TrueCrypt пришел VeraCrypt.

Пробуем примонтировать том, при помощи VeraCrypt.

![Vera](/NevaCTF-2022/Container_as_a_real_drive/img/1.jpg)

Указав пароль из задания, получаем примонтированный том:

![Mount](/NevaCTF-2022/Container_as_a_real_drive/img/2.jpg)

В корне раздела лежат изображения, которые побуждают перейти в папку "Мемы":

![PMount](/NevaCTF-2022/Container_as_a_real_drive/img/3.jpg)

Среди картинок в папке "мемы" - нет ничего интересного, однако есть пака "Удаленные файлы". В данной папке 4 картинки, и все они намекают на восстановление удаленных файлов. 

![PMount](/NevaCTF-2022/Container_as_a_real_drive/img/4.jpg)

Для поиска удаленных файлов можно воспользоваться различными утилитами, в данном случае будем использовать R-Studio, поскольку данное ПО показывает наилучший результат среди конкурентов.

При переходе в дирректорию "Удаленные файлы" R-Studio показывает сразу два:

![PMount](/NevaCTF-2022/Container_as_a_real_drive/img/5.jpg)

Открыв эти файлы, можно обнаружить флаг:

![PMount](/NevaCTF-2022/Container_as_a_real_drive/img/6.jpg)
![PMount](/NevaCTF-2022/Container_as_a_real_drive/img/7.jpg)

## Well done!!!