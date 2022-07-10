# EYE

## TASK

Наш информатор поехал на задание 18 февраля и с тех пор не выходит на связь. Это последнее видео, что он нам прислал. Помогите разобраться, что с ним случилось...

Video: https://mega.nz/file/A6hhSLha#9_Y0pk93bUiQIIru6aLijwlPsuVK00TtawQ-6lpeX-I

## WRITEUP

НЕ Классическая задача на LSB. Но достаточно тривиальная!!! Основная сложность - понять, что это LSB. Но на то она и стегонаграфия, чтобы скрывать очевидное в неочевидном месте!

В каждом кадре данного видео содержится часть скрытого послания, для того, чтобы получить его полностью, нужно применить тот же алгоритм, что в задаче EYE к каждому кадру данного видео! 
 
Для ее решения можно использовать пакет stegano для pyhton.

Тогда решение сводится к следующему коду:

```
from stegano import lsb
from subprocess import call,STDOUT
import os
import cv2
import base64
import math
import shutil

def frame_extraction(video):
    if not os.path.exists("temp_folder"):
        os.makedirs("temp_folder")
    temp_folder="temp_folder"
    print("[INFO] tmp directory is created")

    vidcap = cv2.VideoCapture(video)
    count = 0

    while True:
        success, image = vidcap.read()
        if not success:
            break
        cv2.imwrite(os.path.join("temp_folder/", "{:d}.png".format(count)), image)
        count += 1

def decode_string(video):
    frame_extraction(video)
    secret=""
    root="temp_folder/"
    for i in range(len(os.listdir(root))):
        f_name="{}{}.png".format(root,i)
        secret_dec=lsb.reveal(f_name)
        if secret_dec == None:
            break
        secret+=secret_dec
    secret = base64.b64decode(secret)
    png = open("out.png", "wb")
    png.write(secret)
    png.close()

def clean_tmp(path="temp_folder"):
    if os.path.exists(path):
        shutil.rmtree(path)
        print("[INFO] tmp files are cleaned up")

decode_string("video.mov")
clean_tmp()

```

На первом этапе, видео при помощи CV2 разделяется на фреймы или кадры, после чего из каждого фрейма извлекается lsb вставка. Извлеченная вставка добавляется в переменную - накопитель, в которой после обработки всех фреймов будет храниться общий секрет.

После получения секрета, можно заметить, что он представляет собой base64 строку. После декодирования, становится очевидно, что это бинарный файл! Тогда применив к файлу команду (в linux) file secret.bin, можно заметить, что файл представляет собой png изображение. Флаг, был на изображении!

![PMount](/NevaCTF-2022/HARD_WORK/img/secret.png)


## Well done!!!