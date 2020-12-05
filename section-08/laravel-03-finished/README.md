# laravel create project CMD that uses Composer util container

docker-compose run --rm composer create-project --prefer-dist laravel/laravel .

# this auto-generates a bunch of files in src
# edit the generated config file .env

DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret

# use docker-compose to selectively bring up three services

docker-compose up server mysql php

# by adding the depends_on, that line can be reduced to

docker-compose up server

# one more iteration on the command
# adding --build keeps your images always up to date

docker-compose up -d --build server

# running the artisan utility - migrate

docker-compose run --rm artisan migrate

