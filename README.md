DevOps Lab1. Скрипт запроса погоды.

Задание.

Написать bash-скрипт, который принимает в качестве входящего параметра город.
Выводит температуру и влажность в текущий день в этом городе.
Установить nginx.
Скрипт запускать по расписанию раз в минуту, вывод сохранять в index.html дефолтного сайта.
Необходимо использовать:
```bash
https://github.com/chubin/wttr.in (json формат)
```
Установка необходимых пакетов:
```bash
sudo apt -y install curl nginx jq
```
Установка прав на запись для скрипта в файл всем /var/www/html/index.nginx-debian.html:
```bash
sudo chmod a+w /var/www/html/index.nginx-debian.html
```
Создание файла скрипта, установка прав на выполнение:
```bash
touch weather.sh
```
```bash
chmod u+x weather.sh
```
Скрипт запроса погоды:

```bash
#!/usr/bin/bash

CITY=$1

echo "<HTML><BODY>"

date
echo "<br />"
curl -s https://wttr.in/${CITY}?format=j1 | jq '.["current_condition"][0] | .temp_C,.humidity'

echo "</HTML></BODY>"
```

Создание задания, запуск по расписанию:
```bash
crontab -e
```
Задание crontab:
```bash
* * * * * /home/user/weather.sh Samara > /var/www/html/index.nginx-debian.html 2>> /home/user/wather.err
```
Проверка через curl (Скрин в приложении)
```bash
curl 127.0.0.1
```
<HTML><BODY>
Sat May 24 01:30:01 PM UTC 2025
<br />
"16"
"59"
</HTML></BODY>

![README](screen.png)
