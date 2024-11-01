# Docker - Laravel

# Creditos dos Projetos

[docker-laravel-8 supermavster](https://github.com/supermavster/docker-laravel-8)

[sigi_project isaacpontes](https://github.com/isaacpontes/sigi_project)

A pretty simplified Docker Compose workflow that sets up a LEMP (Linux, NGINX, MySQL, PHP) network of containers for local Laravel development.

## Ports

Ports used in the project:
| Software | Port |
|-------------- | -------------- |
| **nginx** | 8080 |
| **phpmyadmin** | 8081 |
| **mysql** | 3306 |
| **php** | 9000 |
| **xdebug** | 9001 |
| **redis** | 6379 |

## Use

To get started, make sure you have [Docker installed](https://docs.docker.com/) on your system and [Docker Compose](https://docs.docker.com/compose/install/), and then clone this repository.

1. Clone this project:

   ```sh
   git clone https://github.com/c3t4r4/Docker-with-Sigi-Project.git && cd Docker-with-Sigi-Project && cp .env.example .env && cd source && cp .env.example .env
   ```

2. Set de Database Passwords and Copy to .env of Laravel into ./source folder

The configuration of the database **must be the same on both sides** .

```dotenv
# .env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
DB_ROOT_PASSWORD=secret
```

```dotenv
# source/.env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
```

The only change is the `DB_HOST` in the `source/.env` where is called to the container of `mysql`:

```dotenv
# source/.env
DB_HOST=mysql
```

3. Build the project whit the next commands:
```sh
docker-compose up -d
```

4. Install Dependency:
```sh
docker-compose run --rm composer install \ 
&& docker-compose run --rm npm install \ 
&& docker-compose run --rm npm run prod
```

5. Generate Key:
```sh
docker-compose run --rm artisan key:generate \
&& docker-compose run --rm artisan optimize
```

6. Run Migrate and Seed:
```sh
docker-compose run --rm artisan migrate:fresh --seed
```

---

---

## Special Cases

To Down and remove the volumes we use the next command:

```sh
docker-compose down -v
```

Update Composer:

```sh
docker-compose run --rm composer update
```

Run compiler (Webpack.mix.js) or Show the view compiler in node:

```sh
docker-compose run --rm npm run dev
```

Run all migrations:

```sh
docker-compose run --rm artisan migrate
```
