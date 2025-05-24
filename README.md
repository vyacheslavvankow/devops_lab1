DevOps Lab1. Скрипт запроса погоды.

Задание

Написать bash-скрипт, который принимает в качестве входящего параметра город. 
Выводит температуру и влажность в текущий день в этом городе.
Установить nginx.
Скрипт запускать по крону раз в минуту, вывод сохранять в index.html дефолтного сайта.
Необходимо использовать:
https://github.com/chubin/wttr.in (json формат)
библиотека jq для работы с json

Установка необходимых пакетов

sudo apt -y install curl nginx jq

Установка прав на запись для скрипта в файл всем /var/www/html/index.nginx-debian.html

sudo chmod a+w /var/www/html/index.nginx-debian.html

Создание файла скрипта, установка прав на выполнение

touch weather.sh
chmod u+x weather.sh

Скрипт запроса погоды

#!/usr/bin/bash

CITY=$1

echo "<HTML><BODY>"

date
echo "<br />"
curl -s https://wttr.in/${CITY}?format=j1 | jq '.["current_condition"][0] | .temp_C,.humidity'

echo "</HTML></BODY>"


Создание cron задания

crontab -e

Задание crontab

* * * * * /home/user/weather.sh Samara > /var/www/html/index.nginx-debian.html 2>> /home/user/wather.err

Проверка через curl (Скрин в приложении)

curl 127.0.0.1

<HTML><BODY>
Sat May 24 01:30:01 PM UTC 2025
<br />
"16"
"59"
</HTML></BODY>
