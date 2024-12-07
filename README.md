# Symfony/React telegram mini app template

Dockerize php/ts monolith for quick telegram mini app development start.

> [!NOTE]
> The work is still in progress.

## Libraries

- [Nugram Bundle for Symfony](https://github.com/nutgram/symfony-bundl) 
- [Telegram UI](https://github.com/Telegram-Mini-Apps/TelegramUI)

## Install Development Environment

### Docker

If you haven't already install Docker on your local development machine: https://docs.docker.com/engine/install/

### Start Docker

 Run the following commands to get the environment up and running:

```shell
docker compose up
```

### Installation
Install php and javascript dependencies:

```shell
docker compose exec php composer install
docker compose run --rm node npm install
```

Build react app:

```shell
docker compose run --rm node npm run build
```

Execute migrations:

```shell
docker compose exec php php bin/console doctrine:migration:migrate
```
Modify /etc/hosts file:

```shell
$ sudo nano /etc/hosts
127.0.0.1       localhost
127.0.0.1       mini-app.loc
```

Generate certificate/key for https protocol:

```shell

openssl req -x509 -out docker/nginx/ssl/mini-app.loc.crt -keyout docker/nginx/ssl/mini-app.loc.key \
  -newkey rsa:2048 -nodes -sha256 \
  -subj '/CN=mini-app.loc' -extensions EXT -config <( \
   printf "[dn]\nCN=mini-app.loc\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:mini-app.loc\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```

