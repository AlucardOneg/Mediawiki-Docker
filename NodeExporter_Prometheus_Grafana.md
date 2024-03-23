На ControlVM в корне директории пользователя altlinux создать файл monitoring.yml:
-> mcedit monitoring.yml
Содержимое:
![image](https://github.com/AlucardOneg/Mediawiki-Docker/assets/144745012/0921613a-a6f8-4c35-9a61-8e507b70ff6d)
Сохранить и закрыть.
Запустить:
-> docker-compose -f monitoring.yml up -d
Необходимо перейти в основную машину и в браузере зайти по адресу ControlVM, указав порт :3000
Чтобы зайти в Grafana, используется логин/пароль: admin/admin
Новый пароль указать: P@ssw0rd
После входа на главную страницу, нажать на табло Data Source, внутри которорго необходимо 
нажать на Prometheus.
Во вкладке Connection необходимо ввести IP-адрес: http://Prometheus:9090
Снизу нажать Save & Test.
Далее необходимо экспортировать Grafana Dashboard: https://grafana.com/grafana/dashboards/12486-node-exporter-full/
На сайте нажать кнопку Download JSON. Скачать файл и скопировать его содержимое.
Вернуться на веб-интерфейс Grafana и нажать кнопку Create your first dashboard.
Внутри нового окна нажать на кнопку Import dashboard. Откроется окно, внутрь которого необходимо
вставить содержимое файла JSON. Конкретно в поле "Import via dashboard JSON model". Там же
нажать на кнопку Load.
После загрузки появится поле Prometheus: там необходимо выбрать prometheus-1
И нажать кнопку Import.

Затем на ControlVM:
-> sudo mcedit /var/lib/docker/volumes/altlinux_prom-configs/_data/prometheus.yml
![image](https://github.com/AlucardOneg/Mediawiki-Docker/assets/144745012/eb85e1aa-d330-46b1-bbd7-878fe183b267)
Далее в веб-интерфейсе перейти на IP-адрес ControlVM, используя порт :9090
В шапке веб-интерфейса нажать на кнопку Status -> Targets.
В данной вкладке появится новый таргет только после перезагрузки перезагрузки образа:
-> docker-compose -f monitoring.yml restart
Обновляем в веб-интерфейсе страницу и видим, что появился "node-exporter".
