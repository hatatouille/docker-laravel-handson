# docker-laravel-handson

`$ rm -fr tmp/db`

## Get Source
`$ mkdir src && cd $_`

`$ git clone https://github.com/nasirkhan/laravel-starter.git`

とか

## Start
`$ docker-compose up --build -d`

`$ docker-compose ps`

## See logs
`$ docker logs docker-laravel-handson_web_1 -f`

`$ docker logs docker-laravel-handson_app_1 -f`

`$ docker logs docker-laravel-handson_db_1 -f`

`$ tail -f logs/*.log`


## Laravel Configuration
`$ docker exec -it docker-laravel-handson_app_1 sh`

`/work # cp -p .env.example .env`

`/work # php artisan key:generate`

`/work # php artisan migrate`

`/work # php artisan db:seed`

## Destroy
`$ docker-compose down`
