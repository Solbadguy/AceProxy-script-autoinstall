#!/bin/bash
####
###
##
#Обновим БД пакетов и  установим необходимые нам утилиты
apt update & apt install nano mc wget -y

#Скачаем архив с AceStream и распакуем его
wget http://dl.acestream.org/linux/acestream_3.1.16_ubuntu_16.04_x86_64.tar.gz && tar zxvf acestream_3.1.16_ubuntu_16.04_x86_64.tar.gz && rm acestream_3.1.16_ubuntu_16.04_x86_64.tar.gz

#Перенесем все в /opt/
mv acestream_3.1.16_ubuntu_16.04_x86_64/ ~/opt/acestream

#Установим зависимости
apt-get install python python-setuptools python-m2crypto python-apsw python-pip -y
pip install greenlet gevent psutil

#Установим необходимые утилиты
apt-get install python-gevent git python-psutil python-pkg-resources -y

#Скопируем свежую версию AceProxy от Pepsik-Kiev.
cd ~/opt && git clone https://github.com/pepsik-kiev/HTTPAceProxy.git

# Меняем значения конф
cd ~/opt/HTTPAceProxy

# Включаем автозапуск движка
sed -i 's/.*acespawn = False.*/acespawn = True/' aceconfig.py

#Меняем путь к исполняемому файлу 
sed -i "s/acecmd = 'acestreamengine --client-console --live-buffer 25 --vod-buffer 10 --vod-drop-max-age 120'/acecmd = '\/opt\/acestream\/acestreamengineacestreamengine --client-console --live-buffer 25 --vod-buffer 10 --vod-drop-max-age 120'/" aceconfig.py

#Запустим прокси
python ~/opt/HTTPAceProxy/acehttp.py
