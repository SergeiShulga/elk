# elk
Домашнее задание к занятию «ELK» - "Сергей Шульга"

#### Задание 1. Elasticsearch
Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный.
Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name.

![alt text](https://github.com/SergeiShulga/elk/blob/main/img/001.png)
#### Задание 2. Kibana
Установите и запустите Kibana.
Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty.

![alt text](https://github.com/SergeiShulga/elk/blob/main/img/002.png)

##### Задание 3. Logstash
Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch.
Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.

установка NGINX Debian
Установите пакеты, необходимые для подключения apt-репозитория:
sudo apt install curl gnupg2 ca-certificates lsb-release debian-archive-keyring

Теперь нужно импортировать официальный ключ, используемый apt для проверки подлинности пакетов. Скачайте ключ:
curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
    | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null

Проверьте, верный ли ключ был загружен:
gpg --dry-run --quiet --no-keyring --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
Вывод команды должен содержать полный отпечаток ключа 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62:

pub   rsa2048 2011-08-19 [SC] [expires: 2024-06-14]
      573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
uid                      nginx signing key <signing-key@nginx.com>

Если отпечаток отличается от вышеуказанного, удалите файл ключа.

Для подключения apt-репозитория для стабильной версии nginx, выполните следующую команду:

echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
http://nginx.org/packages/debian `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
Если предпочтительно использовать пакеты для основной версии nginx, выполните следующую команду вместо предыдущей:

echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
http://nginx.org/packages/mainline/debian `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
Для использования пакетов из нашего репозитория вместо распространяемых в дистрибутиве, настройте закрепление:

echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | sudo tee /etc/apt/preferences.d/99nginx
Чтобы установить nginx, выполните следующие команды:

sudo apt update
sudo apt install nginx


![alt text]

#### Задание 4. Filebeat.
Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat.
Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.
![alt text]
Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

Задание 5*. Доставка данных
Настройте поставку лога в Elasticsearch через Logstash и Filebeat любого другого сервиса , но не Nginx. Для этого лог должен писаться на файловую систему, Logstash должен корректно его распарсить и разложить на поля.

Приведите скриншот интерфейса Kibana, на котором будет виден этот лог и напишите лог какого приложения отправляется.
