A Docker image and docker-compose config for quickly setting up an environment with Laravel 5.3.

Inspired by [Bitnami's project](https://github.com/bitnami/bitnami-docker-laravel/) but I had problems trying to figure out how to do some things and I wanted to learn Docker so I started from scratch and learnt stuff while creating it step-by-step.

# Quick start

Copy the `docker-compose.yml` file to your computer. Now run:

`docker-compose up -d`

`docker-compose exec app setup-laravel`

You should have a working Laravel app on http://localhost (or your docker machine's address/ip).

If you want to create the basic authentication scaffolding, you can now run:

`docker-compose exec app php artisan make:auth`  
`docker-compose exec app php artisan migrate`

Similarly, most commands should be run in the container. You can run some directly on your machine, for instance if you have composer, you should be able to use it without prefixing it with "docker-compose exec app". But `npm install` will certainly need to be run in the container, the same with any artisan commands that access the database etc., you get the picture.

# Containers

As you'll see in docker-compose.yml this environment consists of
- the app server image
- a vanilla MySQL image

# Software

Most importantly:
- Laravel 5.3
- Laravel Elixir
- Nginx
- PHP (obviously)
- MySQL (in the separate image)

Also featured:
- nodejs
- npm
- git
- composer
- gulp
- bower
- vim
- curl

# User and app folder setup

There's a user called _deploy_ with passwordless sudo privileges.

The folder for the app is in this user's home folder: `/home/deploy/public/app`

node_modules and vendor/bin are only accessible in the container because they contain symlinks which causes problems on Windows.

# Running commands

The current user in the container is _deploy_ and the working directory is `/home/deploy/public/app`, so you can do this for instance:

`docker-compose exec app php artisan --version`

The _deploy_ user has passwordless sudo.
