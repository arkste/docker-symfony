docker-symfony
==============

This is my basic docker stack for developing Symfony 4 Apps.

- Traefik (http://traefik.symfony.local)
- PHP 7.4 (+ Node.js, Yarn & Ansible, see the [Dockerfile](https://github.com/arkste/docker-ci/blob/php74/Dockerfile))
- Xdebug (Port 9000)
- Blackfire (Agent & Probe)
- Nginx 1.17 (http://symfony.local)
- MySQL 5.7
- Adminer (http://db.symfony.local)
- Mailhog (http://mail.symfony.local)

# Installation

You'll need either the [Symfony Binary](https://symfony.com/download) or Composer installed.

 ```bash
$ git clone https://github.com/arkste/docker-symfony.git
$ cd docker-symfony
$ symfony new --full Source // or "composer create-project symfony/website-skeleton Source"
$ docker network create proxy
$ docker-compose up -d
```

then update your system host file:

```bash
echo "127.0.0.1 symfony.local db.symfony.local mail.symfony.local traefik.symfony.local" | sudo tee -a /etc/hosts
```

then go to http://symfony.local

# FAQ

* Why a (big) custom PHP Image?
Because most of my servers are running Ubuntu with PHP built by `ondrej/php` and i want to be as close as possible to the target system while developing. The PHP-Container has the recent Node.js- + Yarn-Version installed, which is necessary if you're using Symfony's [Webpack Encore](https://symfony.com/doc/current/frontend/encore/installation.html).

* Why is X missing?
You're free to customize it for your needs. Like PostgreSQL instead of MySQL, Redis, RabbitMQ, etc.
