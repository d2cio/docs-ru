# Вступление

Стэки это набор сервисов и серверов, которые требуются для запуска вашего приложения. Это очень простой способ разворачивания приложения в разных окружениях (разработка, тестирование, staging, production).

Все сервисы и настройки сервисов, которые поддерживаются в D2C через интерфейс, могут быть описаны в одном **Стэк** файле в формате YAML.

## Создание стэк файла

### Что требуется знать

!!! note

```
Стэк файл должен называться **stackFile.yml**
```

Для сопоставления переменных из других сервисов вы можете использовать следующие шаблоны:

Шаблон                                                   | Комментарии
:------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------
`{{=service('serviceName').get('fieldName')}}`           | Возвращает переменную сервиса
`{{=service('serviceName').getMainPort()}}`              | Возвращает основной порт
`{{=service(serviceName).getAppAlias()}}`                | Возвращает alias контейнера [сервиса приложений](/getting-started/services/#_5)) и всех не реплицируемых сервисов (например, Redis или NGINX)
`{{=service('serviceName').getMasterAlias()}}`           | Возвращает alias мастер-контейнера (для [сервисов хранения данных](/getting-started/services/#data-services))
`{{=service(serviceName).getSlaveAlias()}}`              | Возвращает alias of слейв-контейнера (для [сервисов хранения](/getting-started/services/#_4))
`{{=service('serviceName').getContainerName(num)}}`      | Возвращает имя контейнера сервиса с номером `num`
`{{=service('serviceName').getEnv('environmentfield')}}` | Возвращает поле переменной сервиса
`{{=service('serviceName').getNginxDomain()}}`           | Возвращает стандартный домен, который планируется использовать в NGINX
`{{=service('serviceName').getBalancerDomain()}}`        | Возвращает стандартный домен, который планируется использовать в HAProxy
`{{=randomString(num)}}`                                 | Генерирует случайную строку указанной длины

Вы можете использовать `null` как значение для параметров. Это будет означать, что вы добавите эти параметры через интерфейс во время импорта стэка.

## Сервисы хранения данных

Параметр             | Обязательный | Комментарии
:------------------- | :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
name                 | Да           | Имя должно быть уникальным внутри всего аккаунта. Если имя уже используется - оно будет заменено автоматически сгенерируемым
type                 | Да           | Сервис, который вы хотите развернуть
version              | Да           | Вы можете указать любую из [поддерживаемых версий](/getting-started/services/#_4)
configuration        | Да           | [Поддерживаемые конфигурации](/getting-started/services/#_4)
password             | Нет          | Пароль или пароль пользователя root. Обязательный для некоторых конфигураций, например MongoDB ReplicaSet
username             | Нет          | Создание пользователя в течении разворачивания. База данных будет создана с таким же именем
userPassword         | Нет          | Пароль для пользователя базы данных
ports                | Нет          | Порты сервиса.<br>
Примеры: 8080 - порт 8080 (TCP), 7709\udp - порт 7709 (UDP)
remoteAccess         | Нет          | Все сервисы внутри проекта видны друг для друга изнутри. Если вы хотите, чтобы сервис был доступ из Интернета - используйте `true`
env                  | Нет          | Переменные окружения для вашего приложения. [Примеры](/getting-started/stacks/#_5)
configFiles          |              | Список конфигов
configFiles[i].dest  | Нет          | Имя (для стандартных конфигов) или путь к файлу конфига в контейнере (для [пользовательских конфигов](/getting-started/creating-services/#_12))
configFiles[i].src   | Нет          | Путь к файлу конфига в вашей директории стэка
volumes              |              | Список директорий [постоянного хранилища](/getting-started/containers/#_2)
volumes[i].directory | Нет          | Путь к директории постоянного хранилища
volumes[i].sync      | Нет          | В случаях, когда у вас более одного контейнера в сервисе вам может потребоваться синхронизация данных между директориями постоянного хранилища. Чтобы включить - используйте `true`
deployTo             | Да           | Имена серверов на которых нужно развернуть сервисы

### Примеры

```yml
name: db
type: mysql
version: 8.0
configuration: MasterSlave
username: wordpress
userPassword: null
ports:
  - 3306
remoteAccess: false
configFiles:
  - dest: my.cnf
    src: ./configs/my.cnf
deployTo:
  - main-1
  - main-2
```

```yaml
name: mongo
type: mongodb
version: 3.4
configuration: StandAlone
password: null
ports:
  - 27017
remoteAccess: false
configFiles:
  - dest: my.cnf
    src: ./configs/my.cnf
deployTo:
  - db
```

## Сервисы приложений

Параметр             | Обязательный | Комментарии
:------------------- | :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
name                 | Да           | Имя должно быть уникальным внутри всего аккаунта. Если имя уже используется - оно будет заменено автоматически сгенерируемым
type                 | Да           | Сервис, который вы хотите развернуть
version              | Да           | Вы можете указать любую из [поддерживаемых версий](/getting-started/services/#_5)
source.type          | Да           | Варианты: `git`, `download`<br>
Если вы используете приватный репозиторий, вы должны добавить SSH ключ в ваш аккаунт (инструкции к [GitHub](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) и [BitBucket](https://confluence.atlassian.com/bitbucket/add-an-ssh-key-to-an-account-302811853.html) )
source.url           | Да           | Протоколы: http, https, ftp.<br>
Форматы файлов: .tar.bz2, .tar.gz, .tar, .zip<br>
Пример: <https://wordpress.org/latest.tar.gz>
source.version       | Нет          | Только для git. По умолчанию - `master`. Может использоваться для указания ветки, номера коммита, тэга.
extensions           | Нет          | Дополнительные модули для сервисов PHP-FPM и PHP-Apache
pecl                 | Нет          | Дополнительные модули для сервисов PHP-FPM и PHP-Apache
ports                | Да           | Порты сервиса<br>
Примеры: 8080 - порт 8080 (TCP), 7709\udp - порт 7709 (UDP)
remoteAccess         | Нет          | Все сервисы внутри проекта видны друг для друга изнутри. Если вы хотите, чтобы сервис был доступ из Интернета - используйте `true`
env                  | Нет          | Переменные окружения для вашего приложения. [Примеры](/getting-started/stacks/#_5)
volumes              |              | Список директорий [постоянного хранилища](/getting-started/containers/#_2)
volumes[i].directory | Нет          | Путь к директории постоянного хранилища
volumes[i].sync      | Нет          | В случаях, когда у вас более одного контейнера в сервисе вам может потребоваться синхронизация данных между директориями постоянного хранилища. Чтобы включить - используйте `true`
globalDeps           | Нет          | Команды для установки глобальных зависимостей вашего сервиса.<br>
Примеры: pip install, bundle install, apt-get install, npm install -g
localDeps            | Нет          | Команды для установки локальных зависимостей и подготовке кода к работе.<br>
Примеры: npm install, composer install, bower install, и т.д. или для подготовки:<br>
Примеры: gulp build, grunt build, и т.д.
startCommand         | Нет          | [Команда запуска](//platform/deployment/#_4) приложения
configFiles          |              | Список конфигов
configFiles[i].dest  | Нет          | Имя (для стандартных конфигов) или путь к файлу конфига в контейнере (для [пользовательских конфигов](/getting-started/creating-services/#_12))
configFiles[i].src   | Нет          | Путь к файлу конфига в вашей директории стэка
deployTo             | Да           | Имена серверов на которых нужно развернуть сервисы

### Примеры

```yaml
name: mongo-express
type: nodejs
version: 8
ports:
  - 8081
source:
  type: git
  url: https://github.com/mongo-express/mongo-express
localDeps: "npm install\nnpm run build"
env:
  ME_CONFIG_MONGODB_SERVER: "{{=service('mongo').getMasterAlias()}}"
  ME_CONFIG_MONGODB_AUTH_USERNAME: root
  ME_CONFIG_MONGODB_AUTH_PASSWORD: "{{=service('mongo').get('password')}}"
  ME_CONFIG_MONGODB_PORT: "{{=service('mongo').getMainPort()}}"
  ME_CONFIG_MONGODB_ENABLE_ADMIN: true
  ME_CONFIG_BASICAUTH_USERNAME: admin
  ME_CONFIG_BASICAUTH_PASSWORD: null
  VCAP_APP_HOST: 0.0.0.0
  VCAP_APP_PORT: 8081
deployTo:
  - app
```

```yaml
name: blog
type: php
version: 7.1
source:
  type: download
  url: https://wordpress.org/latest.tar.gz
extensions:
  - mysqli
  - opcache
pecl:
  - redis
env:
  DEBUG: true
volumes:
  - directory: $MAIN_PATH/wp-content/uploads
    sync: true
  - directory: $MAIN_PATH/wp-content/plugins
    sync: true
configFiles:
  - dest: php-fpm.conf
    src: ./configs/php.conf
  - dest: $MAIN_PATH/wp-config.php
    src: ./configs/wp-config.php
  - dest: $MAIN_PATH/db-config.php
    src: ./configs/db-config.php
  - dest: $MAIN_PATH/wp-content/db.php
    src: ./configs/db.php
deployTo:
  - main-1
  - main-2
```

## Other services

Параметр                | Обязательный | Комментарии
:---------------------- | :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
name                    | Да           | Имя должно быть уникальным внутри всего аккаунта. Если имя уже используется - оно будет заменено автоматически сгенерируемым
type                    | Да           | Сервис, который вы хотите развернуть
version                 | Да           | Вы можете указать любую из [поддерживаемых версий](/getting-started/services/#_6)
ports                   | Да           | Порты сервиса<br>
Примеры: 8080 - порт 8080 (TCP), 7709\udp - порт 7709 (UDP)
remoteAccess            | Нет          | Все сервисы внутри проекта видны друг для друга изнутри. Если вы хотите, чтобы сервис был доступ из Интернета - используйте `true`
env                     | Нет          | Переменные окружения для вашего приложения. [Примеры](/getting-started/stacks/#_5)
volumes                 |              | Список директорий [постоянного хранилища](/getting-started/containers/#_2)
volumes[i].directory    | Нет          | Путь к директории постоянного хранилища
volumes[i].sync         | Нет          | В случаях, когда у вас более одного контейнера в сервисе вам может потребоваться синхронизация данных между директориями постоянного хранилища. Чтобы включить - используйте `true`
globalDeps              | Нет          | Команды для установки глобальных зависимостей вашего сервиса.<br>
Примеры: pip install, bundle install, apt-get install, npm install -g
serviceFiles            |              | Список сервисов, которые обслуживает NGINX or HAProxy
serviceFiles[i].name    | Нет          | Имя сервиса, который будет обслуживать NGINX или HAProxy
serviceFiles[i].static  | Нет          | `true` если вам нужно обслуживать статику. **Будьте внимательны**: NGINX может обслуживать статику только на этом же сервере
serviceFiles[i].src     | Нет          | Путь к конфигу обслуживаемого сервиса. Если требуется стандартный конфиг - не заполняйте этот параметр
serviceFiles[i].domains | Нет          | Массив, который содержит список доменов сервиса
serviceFiles[i].https   | Нет          | Значение по умолчанию `none` (режим HTTP). Используйте `letsencrypt`, если вы хотите сгенерировать TLS сертификат для указанного списка доменов. DNS-запись для доменов должна быть доступна в момент создания стэка
configFiles             |              | Список конфигов
configFiles[i].dest     | Нет          | Имя (для стандартных конфигов) или путь к файлу конфига в контейнере (для [пользовательских конфигов](/getting-started/creating-services/#_12))
configFiles[i].src      | Нет          | Путь к файлу конфига в вашей директории стэка
deployTo                | Да           | Имена серверов на которых нужно развернуть сервисы

### Examples

```yaml
name: proxy
type: nginx
version: 1.13
ports:
  - 80
  - 443
remoteAccess: true
serviceFiles:
  - name: blog
    src: ./configs/blog.conf
    domains: [example.com, www.example.com]
  - name: mongo-express
    src: ./configs/mongo-express.conf
deployTo:
  - edge
```

```yaml
name: balancer
type: haproxy
version: latest
ports:
  - 80
  - 443
remoteAccess: true
serviceFiles:
  - name: cluster
    src: ./configs/cluster.conf
    https: letsencrypt
    domains: [example.com, www.example.com]
deployTo:
  - edge
```

## Docker services

Параметр             | Обязательный | Комментарии
:------------------- | :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
name                 | Да           | Имя должно быть уникальным внутри всего аккаунта. Если имя уже используется - оно будет заменено автоматически сгенерируемым
type                 | Да           | Сервис, который вы хотите развернуть
image                | Да           | Docker образ приложения из [DockerHub](https://hub.docker.com/).<br>
Примеры: openjdk, million12/varnish, quay.io/letsencrypt/dnsmasq
version              | Да           | Версия приложения
source.type          | Да           | Варианты: `git`, `download`<br>
Если вы используете приватный репозиторий, вы должны добавить SSH ключ в ваш аккаунт (инструкции к [GitHub](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) и [BitBucket](https://confluence.atlassian.com/bitbucket/add-an-ssh-key-to-an-account-302811853.html) )
source.url           | Да           | Протоколы: http, https, ftp.<br>
Форматы файлов: .tar.bz2, .tar.gz, .tar, .zip<br>
Пример: <https://wordpress.org/latest.tar.gz>
source.version       | Нет          | Только для git. По умолчанию - `master`. Может использоваться для указания ветки, номера коммита, тэга.
ports                | Да           | Порты сервиса<br>
Примеры: 8080 - порт 8080 (TCP), 7709\udp - порт 7709 (UDP)
remoteAccess         | Нет          | Все сервисы внутри проекта видны друг для друга изнутри. Если вы хотите, чтобы сервис был доступ из Интернета - используйте `true`
env                  | Нет          | Переменные окружения для вашего приложения. [Примеры](/getting-started/stacks/#_5)
volumes              |              | Список директорий [постоянного хранилища](/getting-started/containers/#_2)
volumes[i].directory | Нет          | Путь к директории постоянного хранилища
volumes[i].sync      | Нет          | В случаях, когда у вас более одного контейнера в сервисе вам может потребоваться синхронизация данных между директориями постоянного хранилища. Чтобы включить - используйте `true`
globalDeps           | Нет          | Команды для установки глобальных зависимостей вашего сервиса.<br>
Примеры: pip install, bundle install, apt-get install, npm install -g
localDeps            | Нет          | Команды для установки локальных зависимостей и подготовке кода к работе.<br>
Примеры: npm install, composer install, bower install, и т.д. или для подготовки:<br>
Примеры: gulp build, grunt build, и т.д.
startCommand         | Нет          | [Команда запуска](//platform/deployment/#_4) приложения
configFiles          |              | Список конфигов
configFiles[i].dest  | Нет          | Имя (для стандартных конфигов) или путь к файлу конфига в контейнере (для [пользовательских конфигов](/getting-started/creating-services/#_12))
configFiles[i].src   | Нет          | Путь к файлу конфига в вашей директории стэка
volumesUID           | Нет          | Идентификатор пользователя директории постоянного хранилища
deployTo             | Да           | Имена серверов на которых нужно развернуть сервисы

### Example

```yaml
name: varnish
type: docker
image: debian
version: jessie
ports:
  - 80
remoteAccess: false
configFiles:
  - dest: /etc/varnish/default.vcl
    src: ./configs/default.vcl
globalDeps: |
  apt-get install wget
  wget -qO- https://packagecloud.io/install/repositories/varnishcache/varnish51/script.deb.sh | bash
  apt-get install varnish
startCommand:  : varnishd -j unix,user=vcache -F -f /etc/varnish/default.vcl -s malloc,100m -a 0.0.0.0:80
deployTo:
  - edge
```

## Hosts

Параметр            | Обязательный | Комментарии
:------------------ | :----------- | :------------------------------------
name                | Да           | Имя сервера, который будет создан
requirements.cores  | Да           | Количество ядер сервера
requirements.memory | Да           | Количество оперативной памяти сервера

### Example

```yaml
hosts:
  - name: main-1
    requirements:
      cores: 2
      memory: 4

  - name: main-2
    requirements:
      cores: 2
      memory: 4

  - name: edge
    requirements:
      cores: 1
      memory: 0.5
```

## Как развернуть стэк

### В существующий проект

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Создайте или откройте проект
3. Нажмите **Импортировать стэк**
4. Вставьте ссылку на стэк или загрузите архив (или файл `.yml`, если в стэке только он) со стэком с вашего компьютера
5. Выберите провайдера и регион в котором вы хотите создать новые сервера или нажмите **Выбрать существующие сервера** и выберите сервера, которые уже созданы
6. Заполните необходимые поля (если они есть)
7. Нажмите **Создать сервера и сервисы**

### В новый проект

1. [Выберите стэк](/getting-started/stack-hub), который вы хотите развернуть<br>
  или вставьте ссылку на ваш стэк. Пример: **<https://panel.d2c.io/?import=yourlink>**
2. Выберите провайдера и регион в котором вы хотите создать новые сервера или нажмите **Выбрать существующие сервера** и выберите сервера, которые уже созданы
3. Заполните необходимые поля (если они есть)
4. Нажмите **Создать сервера и сервисы**

Новый проект будет создан. При необходимости, вы можете изменить его имя.
