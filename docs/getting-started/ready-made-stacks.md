# Introduction

At this page we provide ready to use stacks.

### How to deploy a stack

1. Choose a stack you want to deploy
2. Sign in or create an account
3. Choose a provider and a region if you want to create new hosts or choose the created ones in **Select hosts** menu
4. Fill in necessary fields (if they are)
5. Click **Create hosts and services**

A new project with a stack will be created.

## Stacks

| Stack name         |  Services  | Configuration | Sources and deploy |
| :-------------     | :-------------  | :-------------  |:------------- |
| MEAN light | MongoDB, Mongo-express (Node.js), Node.js, NGINX    | 1 hosts, 4 containers  | [GitHub](https://github.com/d2cio/mean-light-stack) \| [Deploy](https://panel.d2c.io/?import=https://github.com/d2cio/mean-light-stack/archive/master.zip)
| MEAN  | MongoDB, Mongo-express (Node.js), Node.js, NGINX    | 2 hosts, 4 containers  | [GitHub](https://github.com/d2cio/mean-stack) \| [Deploy](https://panel.d2c.io/?import=https://github.com/d2cio/mean-stack/archive/master.zip)
| Wordpress | MariaDB (MasterSlave), Redis, PHP-FPM, NGINX-Cluster, HAProxy, Varnish, PHPMyAdmin (PHP-FPM), NGINX   |  3 hosts, 11 containers |  [GitHub](https://github.com/d2cio/wordpress-scalable-stack) \| [Deploy](https://panel.d2c.io/?import=https://github.com/d2cio/wordpress-scalable-stack/archive/master.zip)
| Wordpress light | Percona (StandAlone), PHP-FPM, NGINX-Cluster, Varnish, PHPMyAdmin (PHP-FPM), NGINX   |  1 hosts, 6 containers |  [GitHub](https://github.com/d2cio/wordpress-scalable-light-stack) \| [Deploy](https://panel.d2c.io/?import=https://github.com/d2cio/wordpress-scalable-light-stack/archive/master.zip)


<!--
| Sentry             | [GitHub]()                 | Redis, PostgreSQL, Docker (web), Docker (Worker), Docker (Cron), NGINX                              | 1 host, 6 containers |-->
