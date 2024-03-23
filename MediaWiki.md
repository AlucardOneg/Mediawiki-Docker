На ControlVM в корне пользователя altlinux создать файл wiki.yml:

-> mcedit wiki.yml

Содержимое:

![image](https://github.com/AlucardOneg/Mediawiki-Docker/assets/144745012/d7e9d05a-918b-45d9-82af-5a74fe0c67e4)

Далее выполнить:

-> docker volume create dbvolume

-> docker-compose -f wiki.yml up -d

Проверка:

-> docker ps

На основной машине необходимо зайти в браузер и в URL вписать IP-адрес ControlVM.

Должен открыться интерфейс MediaWiki: и дальше обычный процесс установки...

После установки, необходимо скачать LocalSettings.php

В основной машине выполнить команду:

-> scp LocalSettings.php altlinux@%IP_ADDRESS_CONTROLVM%:~/

Зайти на ControlVM в файл wiki.yml и раскомментировать единственную строчку:

(удалить решетку).
И выполнить команды:
-> docker-compose -f wiki.yml stop
-> docker-compose -f wiki.yml up -d
В браузере необходимо заново открыть MediaWiki и убедиться, что Заглавная страница отображается.
