# Вступление

На этой странице мы отображаем список готовых стэков.

## Как развернуть стэк

1. Выберите стэк, который хотите развернуть
2. Войдите в аккаунт или создайте новый
3. Выберите провайдера и регион
4. Заполните необходимые поля (если они есть)
5. Нажмите **Создать сервера и сервисы**

## Стэки

!!! note

    Актуальный список стэков [можно найти в Stackhub](https://d2c.io/stackhub)

Название стэка      | Сервисы                                                                                             | Конфигурация              | Ссылки на GitHub<br>и разворачивание
:------------------ | :-------------------------------------------------------------------------------------------------- | :------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
MEAN light          | MongoDB, Mongo-express (Node.js), Node.js, NGINX                                                    | 1 сервер, 4 контейнера    | [GitHub](https://github.com/d2cio/mean-light-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mean-light-stack/archive/master.zip)
MEAN                | MongoDB, Mongo-express (Node.js), Node.js, NGINX                                                    | 2 сервера, 4 контейнера   | [GitHub](https://github.com/d2cio/mean-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mean-stack/archive/master.zip)
WordPress           | MariaDB (MasterSlave), Redis, PHP-FPM, NGINX-Cluster, HAProxy, Varnish, PHPMyAdmin (PHP-FPM), NGINX | 3 сервера, 11 контейнеров | [GitHub](https://github.com/d2cio/wordpress-scalable-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/wordpress-scalable-stack/archive/master.zip)
WordPress Apache    | MariaDB (MasterSlave), Redis, PHP-Apache, Varnish, HAProxy, PHPMyAdmin (PHP-Apache)                 | 3 сервера, 8 контейнеров  | [GitHub](https://github.com/d2cio/wordpress-scalable-apache-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/wordpress-scalable-apache-stack/archive/master.zip)
WordPress light     | MariaDB (StandAlone), PHP-Apache, PHPMyAdmin (PHP-Apache), HAProxy                                  | 1 сервер, 4 контейнера    | [GitHub](https://github.com/d2cio/wordpress-scalable-light-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/wordpress-scalable-light-stack/archive/master.zip)
Sentry              | Redis, PostgreSQL, Docker (web), Docker (Worker), Docker (Cron), NGINX                              | 1 сервер, 6 контейнеров   | [GitHub](https://github.com/d2cio/sentry-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/sentry-stack/archive/master.zip)
Odoo                | PostgreSQL, Docker, NGINX                                                                           | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/odoo-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/odoo-stack/archive/master.zip)
Redmine             | PostgreSQL, Docker, NGINX                                                                           | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/redmine-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/redmine-stack/archive/master.zip)
RocketChat          | MongoDB, Docker, NGINX                                                                              | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/rocketchat-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/rocketchat-stack/archive/master.zip)
Ghost               | MariaDB, Docker, NGINX                                                                              | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/ghost-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/ghost-stack/archive/master.zip)
PyroCMS             | PostgreSQL, PHP-FPM, NGINX                                                                          | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/pyrocms-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/pyrocms-stack/archive/master.zip)
Cachethq            | PostgreSQL, Docker, NGINX                                                                           | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/cachethq-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/cachethq-stack/archive/master.zip)
MongoDB             | MongoDB, Mongo-express(Node.js), NGINX                                                              | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/mongodb-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mongodb-stack/archive/master.zip)
MongoDB ReplicaSet  | MongoDB, Mongo-express(Node.js), NGINX                                                              | 3 сервера, 5 контейнеров  | [GitHub](https://github.com/d2cio/mongodb-replicaset-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mongodb-replicaset-stack/archive/master.zip)
MariaDB             | MariaDB, PHPMyAdmin (PHP-FPM), NGINX                                                                | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/mariadb-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mariadb-stack/archive/master.zip)
MariaDB MasterSlave | MariaDB, PHPMyAdmin (PHP-FPM), NGINX                                                                | 2 сервера, 4 контейнера   | [GitHub](https://github.com/d2cio/mariadb-masterslave-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mariadb-masterslave-stack/archive/master.zip)
Percona             | Percona, PHPMyAdmin (PHP-FPM), NGINX                                                                | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/percona-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/percona-stack/archive/master.zip)
Percona MasterSlave | Percona, PHPMyAdmin (PHP-FPM), NGINX                                                                | 2 сервера, 4 контейнера   | [GitHub](https://github.com/d2cio/percona-masterslave-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/percona-masterslave-stack/archive/master.zip)
MySQL               | MySQL, PHPMyAdmin (PHP-FPM), NGINX                                                                  | 1 сервер, 3 контейнера    | [GitHub](https://github.com/d2cio/mysql-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mysql-stack/archive/master.zip)
MySQL MasterSlave   | MySQL, PHPMyAdmin (PHP-FPM), NGINX                                                                  | 2 сервера, 4 контейнера   | [GitHub](https://github.com/d2cio/mysql-masterslave-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/mysql-masterslave-stack/archive/master.zip)
Adminer             | PHP+Apache                                                                                          | 1 сервер, 1 контейнер     | [GitHub](https://github.com/d2cio/adminer-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/adminer-stack/archive/master.zip)
Adminer+NGINX       | PHP-FPM, NGINX                                                                                      | 1 сервер, 2 контейнеров   | [GitHub](https://github.com/d2cio/adminer-nginx-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/adminer-nginx-stack/archive/master.zip)
pgAdmin4            | Python                                                                                              | 1 сервер, 1 контейнер     | [GitHub](https://github.com/d2cio/pgAdmin-stack) и [Развернуть](https://panel.d2c.io/?import=https://github.com/d2cio/pgAdmin-stack/archive/master.zip)
