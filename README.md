# docker-rails5-alpine
## Introduction
Docker-rails5-alpine is lightweight Docker images set for Rails applications based on Alpine Linux. This is optimzed for the API mode using MySQL and Redis.

## Environment

- ruby: 2.6.3
- mysql: 8.0.16
- redis: 5.0.5

## How to use

Clone this repository
```sh
git clone https://github.com/jianghan0/docker-rails5-alpine.git
```

Add rails code to source directory
```sh
cd docker-rails5-alpine

# When use your exist rails app
git clone (your-rails-repository) source

# When create new rails app
mkdir source && cd source
rails new . --api --mysql
```

Edit your database settings
```yml
# config/database.yml

default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  host: <%= ENV.fetch("DB_HOST") { "127.0.0.1" } %>
  port: <%= ENV.fetch("DB_PORT") { 3306 } %>
  username: <%= ENV.fetch("DB_USER") { root } %>
  password: <%= ENV.fetch("DB_PASSWORD") %>

development:
  <<: *default
  database: your-database
```

Build docker image
```sh
docker-compose build
```

Create database and run the migrations
```sh
docker-compose run --rm web bin/rails db:create
docker-compose run --rm web bin/rails db:migrate
```

Run the app
```sh
docker-compose up -d
```

Attach rails server
```sh
docker attach docker-rails5-alpine_web_1
```

Then you can access your rails app by localhost:3000
