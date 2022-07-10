# EYE

## TASK

Наш информатор не переставал нас удивлять, и нам пришлось отправить его на курсы повышения квалификации. Теперь он нам зачем-то прислал фото своего глаза в инфракрасном спектре ([тык](/NevaCTF-2022/EYE/img/1.png "EYE")). Мы не давали ему никакого задания и понятия не имеем, что и как он сокрыл в файле (и есть там что-то вообще). Видимо, нам тоже нужно было посетить эти курсы... Попробуй нам помочь, иначе нам прийдется обращаться к профессионалам, вдруг там что-то важное!?

## WRITEUP

Классическая задача на LSB. Для ее решения можно использовать пакет stegano для pyhton.

Тогда решение сводится к следующему коду:

```
from stegano import lsb

test =  lsb.reveal('../Release/secret.png')

print(test)

```

Получаем на выходе флаг: nevactf{lE4Rn_1E4rn_And_LEArn_a6Ain}

![PMount](/NevaCTF-2022/Container_as_a_real_drive/img/6.jpg)
![PMount](/NevaCTF-2022/Container_as_a_real_drive/img/7.jpg)

## Well done!!!