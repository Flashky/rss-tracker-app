# rss-tracker-app

## Configuration properties

Before running the service, you will need to customize several properties or environment variables:

Property | Description | Default value
--|--|--
``TELEGRAM_BOT_TOKEN`` | The Telegram Bot token provided by [@BotFather](https://t.me/botfather) | None
``MONGODB_HOST`` | The MongoDB instance hostname or ip | ``localhost``
``MONGODB_PORT`` | The MongoDB port | ``27017``
``MONGODB_USERNAME`` | The MongoDB username | ``admin`` **(*)**
``MONGODB_PASSWORD`` | The MongoDB password | ``admin`` **(*)**
``MONGODB_DATABASE`` | The MongoDB database | ``rss_tracker_db``
``JOB_FIXED_DELAY_SECONDS`` | The delay in seconds between job executions | ``60``

***:** *It is highly recommended to change both default username and password.*

On Docker Compose running mode:
- ``MONGODB_HOST`` value is ignored when using. It will use a default hostname ``mongodb`` specified by the ``docker-compose.yml`` file. 
- ``MONGODB_PORT`` refers to the exposed MongoDB port to the Docker host (internally the container will still use ``27017``). Use this port if you need to connect with your MongoDB database manager.

## Docker Compose

#### Requirements

- Docker.

#### Run

Check for images updates:

```bash
docker-compose pull
```

Run in dettach mode:

```shell
docker-compose up -d
```

The previous command will setup the following containers:
- rss-tracker-mongodb 
- rss-tracker-bot
- rss-tracker-batch

It will use ``.env`` file by default for getting the [configuration properties](#configuration-properties).

If you want to use multiple environments you can duplicate ``.env``, customize its values, and finally run ``docker-compose`` specifying ``--env-file`` flag  to select which configuration to use.

Example with a ``.env.dev`` file:

```shell
docker-compose pull
docker-compose --env-file .env.dev up -d
```
