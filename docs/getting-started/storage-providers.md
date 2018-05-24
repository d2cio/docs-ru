# Вступление

На этой странице, мы опишем как генерировать ключи доступа к бэкап провайдерам и как их использовать в D2C.

## Поддерживаемые бэкап провайдеры

1. Amazon S3
2. Backblaze
3. Dropbox
4. DigitalOcean Spaces
5. Microsoft OneDrive
6. Hubic
7. FTP/SFTP

## Dropbox, OneDrive, Hubic

Данные провайдеры подключаются с помощью oAuth и это самый простой способ подключения.

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Перейдите на страницу [настроек](https://panel.d2c.io/settings)
3. Нажмите на кнопку **+Добавить бэкап провайдера** в блоке **Провайдеры**
4. Выберите Dropbox, OneDrive или Hubic
5. Нажмите **Подключить**, войдите в ваш аккаунт и нажмите **+Добавить провайдера**

## Быстрый старт с Amazon S3

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Перейдите на страницу [настроек](https://panel.d2c.io/settings)
3. Нажмите на кнопку **+Добавить бэкап провайдера** в блоке **Провайдеры**
4. Выберите S3
5. Вставьте ваши ключи доступа AWS (Access Key ID and Secret Access Key) и нажмите **+Добавить провайдера**

### Сгенерировать ключи доступа (AWS credentials)

Если у вас нет ключей доступа AWS, вы можете создать их через консоль AWS (AWS Management console)

1. Войдите в аккаунт AWS, раздел [IAM Users](https://console.aws.amazon.com/iam/home?#/users), кликните Add user
2. Вставьте имя пользователя (например d2c). Выберите “Programmatic access” и кликните **Next: Permissions**
3. Нажмите кнопку "Attach existing policies directly". Найдите AdministratorAccess policy, отметьте её, затем нажмите **Next: Review**
4. Кликните Create user
5. Скопируйте ключи доступа (Access Key ID and Secret Access Key) или сохраните в .csv файл с помощью кнопки download
6. Затем следуйте инструкции **Быстрый старт с Amazon S3**

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

## DigitalOcean Spaces

### Быстрая интеграция с DigitalOcean Spaces

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Перейдите на страницу [настроек](https://panel.d2c.io/settings)
3. Нажмите на кнопку **+Добавить бэкап провайдера** в блоке **Провайдеры**
4. Выберите Digital Ocean Spaces
5. Вставьте ваши ключи доступа Digital Ocean Spaces (Key and Secret) и нажмите **+Добавить провайдера**

### Сгенерировать ключи доступа DigitalOcean Spaces

Если у вас нет ключей доступа DigitalOcean Spaces, вы можете создать их через консоль Digital Ocean

1. Откройте страницу [DigitalOcean Spaces](https://cloud.digitalocean.com/spaces)
2. Нажмите на **Manage Keys** и далее на **Generate New Key**
3. Задайте имя, подтвердите действие и скопируйте ваши ключи (Key и Secret)
4. Затем следуйте инструкции **Быстрая интеграция с DigitalOcean Spaces**

## Backblaze

### Быстрая интеграция с Backblaze

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Перейдите на страницу [настроек](https://panel.d2c.io/settings)
3. Нажмите на кнопку **+Добавить бэкап провайдера** в блоке **Провайдеры**
4. Выберите Backblaze
5. Вставьте ваши ключи доступа (Account ID и Application Key) и нажмите **+Добавить провайдера**

### Сгенерировать ключи доступа Backbaze

Если у вас нет ключей доступа Backblaze, вы можете создать их через консоль Backblaze

1. Откройте страницу Backblaze [Buckets](https://secure.backblaze.com/b2_buckets.htm)
2. Нажмите **Show Account ID and Application Key**
3. Далее нажмите **Create Application Key**. Скопируйте Account ID и Application Key
4. Затем следуйте инструкции **Быстрая интеграция с Backblaze**

## FTP/SFTP

1. Войдите в ваш [D2C аккаунт](https://panel.d2c.io/account/login)
2. Перейдите на страницу [настроек](https://panel.d2c.io/settings)
3. Нажмите на кнопку **+Добавить бэкап провайдера** в блоке **Провайдеры**
4. Выберите FTP или SFTP
5. Вставьте endpoint, порт, логин и пароль и нажмите **+Добавить провайдера**
