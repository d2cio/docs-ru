# Вступление

На этой странице мы расскажем как подключить аккаунты облачных провайдеров к D2C.

## Поддерживаемые хостинг провайдеры

- **Amazon Web Services**
- **DigitalOcean**
- **Vultr**
- **UpCloud**
- **Google Cloud Platform**

## Amazon Web Services

### Видео-инструкция

<iframe width="640" height="360" src="https://www.youtube.com/embed/LT866IxJ5Qo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br>

### Быстрый старт с AWS

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Нажмите **+ Создать сервер**
3. Нажмите **Добавить провайдера** и выберите **Amazon Web Services**
5. Вставьте ваши ключи доступа AWS (Access Key ID and Secret Access Key)

### Сгенерировать ключи доступа (AWS credentials)

Если у вас нет ключей доступа AWS, вы можете создать их через консоль AWS (AWS Management console)

1. Войдите в аккаунт AWS, раздел [IAM Users](https://console.aws.amazon.com/iam/home?#/users), кликните Add user
2. Вставьте имя пользователя (например d2c). Выберите “Programmatic access” и кликните **Next: Permissions**
3. Нажмите кнопку "Attach existing policies directly". Найдите AdministratorAccess policy, отметьте её, затем нажмите **Next: Review**
4. Кликните Create user
5. Скопируйте ключи доступа (Access Key ID and Secret Access Key) или сохраните в .csv файл с помощью кнопки download
6. Затем следуйте инструкции **Быстрый старт с AWS**

### Создать индивидуальную policy

1. Откройте раздел AWS [policies](https://console.aws.amazon.com/iam/home?#/policies)
2. Кликните **Create policy**
3. Выберите **Create Your Own Policy**
4. Введите имя (например, d2c-policy)
5. Вы можете сгенерировать индивидуальную policy [здесь](https://awspolicygen.s3.amazonaws.com). Ниже приведен простой пример с ограничением по регионам (замените "eu-west-1" на регионы, которые вы хотите использовать):

        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Action": [
                        "ec2:*"
                    ],
                    "Effect": "Allow",
                    "Resource": "*",
                    "Condition": {
                        "StringEquals": {
                            "ec2:Region": "eu-west-1"
                        }
                    }
                }
            ]
        }

6. Кликните **Create policy**
7. Теперь вы можете [сгенерировать ключи доступа AWS](/getting-started/cloud-providers/#generate-aws-credentials) с вашей собственной policy

## Google Cloud Platform

### Видео-инструкция

<iframe width="640" height="360" src="https://www.youtube.com/embed/WhbvLZLGUiE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br>

### Быстрый старт с GCP

!!! note

    Убедитесь, что для вашего GCP проекта включен API Compute Engine и подключен платежный аккаунт

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Нажмите **+ Создать сервер**
3. Нажмите **Добавить провайдера** и выберите **Google Cloud**
4. Загрузите JSON файл вашего [Сервисного аккаунта](https://console.cloud.google.com/iam-admin/serviceaccounts) с ключами доступа

### Сгенерировать GCP JSON файл

Если у вас нет JSON файла с ключами доступа GCP, вы можете создать его через консоль GCP

1. Создайте новый проект в [GCP](https://console.cloud.google.com), если требуется
2. На странице GCP [APIs & Services](https://console.cloud.google.com/apis/dashboard) нажмите **ENABLE APIS AND SERVICES**, найдите **Compute Engine API** и нажмите **Enable**
3. Далее, перейдите в [Credentials](https://console.cloud.google.com/apis/api/compute.googleapis.com/credentials) и выберите созданный сервисный аккаунт (вы будете перенаправлены на страницу [IAM & admin/Service accounts](https://console.cloud.google.com/iam-admin/serviceaccounts))
4. На странице Service accounts создайте новый ключ для созданного сервисного аккаунта (Actions → ⋮ → Create key) в формате JSON
5. Затем следуйте инструкции **Быстрый старт с GCP**

## DigitalOcean

Если у вас ещё нет аккаунта в DigitalOcean вы можете [заригестрироваться по этой ссылке](https://m.do.co/c/3e6774908846) и получить бонус на свой аккаунт в размере **$100**.

### Видео-инструкция

<iframe width="640" height="360" src="https://www.youtube.com/embed/bCzGLQ6op0U" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br>

### Быстрый старт с DigitalOcean

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Кликните **+ Создать сервер**
3. Нажмите **Добавить провайдера** и выберите **DigitalOcean**
4. Нажмите кнопку **Подключить** и авторизуйтесь в аккаунте **DigitalOcean**

## Vultr

Если у вас ещё нет аккаунта в Vultr вы можете [зарегистрироваться по этой ссылке](https://www.vultr.com/?ref=7772421-4F) и получить бонус на свой аккаунт в размере **$50**.

### Видео-инструкция

<iframe width="640" height="360" src="https://www.youtube.com/embed/5pQzCXkhNKM" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br>

### Быстрый старт с Vultr

!!! note

    Для того, чтобы разрешить D2C управлять серверами Vultr необходимо добавить IP-адреса 52.58.244.78/32 и 52.57.161.208/32 в разделе Access Control

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Кликните **+ Создать сервер**
3. Нажмите **Добавить провайдера** и выберите **Vultr**
4. Вставьте ваш Vultr API key

### Авторизовать D2C в Vultr

Если у вас нет Vultr API key, вы можете создать его в аккаунте Vultr

1. Войдите в аккаунт Vultr, раздел [API](https://my.vultr.com/settings/#settingsapi)
2. Нажмите **Enable API** и скопируйте API key
3. Добавьте 52.58.244.78/32 и 52.57.161.208/32 IP в разделе Access Control
4. Далее следуйте инструкции **Быстрый старт с Vultr**

## UpCloud

Если у вас ещё нет аккаунта в Upcloud вы можете [зарегистрироваться по этой ссылке](https://upcloud.com/signup/?promo=8YR3X6) и получить бонус на свой аккаунт в размере **$25**.

### Видео-инструкция

<iframe width="640" height="360" src="https://www.youtube.com/embed/adxjApELOu8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br>

### Быстрый старт с UpCloud

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Кликните **+ Создать сервер**
3. Нажмите **Добавить провайдера** и выберите **UpCloud**
4. Вставьте ваш API username и API password

### Создание API пользователя

1. Войдите в UpCloud аккаунт, раздел [User Accounts](https://my.upcloud.com/account#t2)
2. Нажмите **Add user**
3. Заполните необходимые данные, такие как username, password, phone и т.д.
4. Отключите Access to Control Panel
4. Разрешите **API connections** from *All addresses*
5. Далее следуйте инструкции **Быстрый старт с UpCloud**
