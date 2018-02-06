DOCKER - SYMFONY - VUE.JS
=========================

# Requirements

- Linux (debian or ubuntu) or MacOS X
- [docker](https://docs.docker.com/)
- [docker-compose](https://docs.docker.com/compose/)

# Get project

```bash
git clone git@github.com:eleven-labs/docker-symfony-vue.git && cd docker-symfony-vue
```

# Change environment variable
```bash
cp .env.dist .env
```

```dotenv
# APP
APP_DIR=/var/www/symfony

# SYMFONY
APP_ENV=dev
APP_DEBUG=1
APP_SECRET=93174013057b1e458ff58ae5f158a0f1

# NODE
NODE_ENV=development

# DATABASE
POSTGRES_HOST=postgres
POSTGRES_DB=db
POSTGRES_USER=user
POSTGRES_PASSWORD=password
POSTGRES_PORT=5432

# PORT WEB
WEB_PORT=81

#REDIS
REDIS_HOST=redis
```

# Initialize project

- Initialize project with script
```bash
bin/app init
```

- Initialize project without script
```bash
docker-compose build --force-rm --no-cache
docker-compose up -d --force-recreate
docker-compose exec -T php chmod 777 -R /var/www/symfony/var/cache
docker-compose exec -T php chmod 777 -R /var/www/symfony/var/logs
docker-compose exec -T --user www-data php composer install -n
docker-compose exec -T --user www-data php bin/console doctrine:database:create --if-not-exists --no-interaction
docker-compose exec -T --user www-data php bin/console doctrine:schema:update --no-interaction --force
docker-compose exec -T --user www-data php bin/console doctrine:fixtures:load --no-interaction

```

# Basic command with script

```bash
bin/app init            # Initialize project
bin/app start           # Start project
bin/app stop            # Stop project
bin/app bash            # Use bash inside the app container
bin/app exec            # Execute a command inside the app container
bin/app destroy         # Removes all the project Docker containers with their volumes
bin/app console         # Use the Symfony console
bin/app composer        # Use Composer inside the app container
bin/app tests           # Run test project inside the app container

```
