# Docker template to work with Laravel, Postgres, Redis and Nginx

## Getting started

### Create a new folder to store postgres volume data
~~~/bin/bash
mkdir services/postgres/database-data
~~~

### Set-up the environment variables
~~~
cp .env.example .env
nano .env
~~~

### Start docker
~~~
docker-compose up -d
~~~

### Go to localhost
If everything goes fine, you should see your laravel app at localhost.