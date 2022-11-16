# symfony-docker

//Dockerfile PHP
```
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony
```
//unlock writing directory
```
sudo chown -R $(whoami) .
```
//index.php if profiler hide
```
<?php

use App\Kernel;

require_once dirname(__DIR__).'/vendor/autoload_runtime.php';

if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https') {
    $_SERVER['HTTPS'] = 'on';
    $_SERVER['SERVER_PORT'] = 443;
}

return function (array $context) {
    return new Kernel($context['APP_ENV'], (bool) $context['APP_DEBUG']);
};
```
//run docker
```
docker-compose up -d --build
```
//php
```
docker-compose exec php /bin/bash
```
//symfony cmd
```
symfony check:requirements
```
//create project
```
symfony new . --version="6.1.*" --webapp
```
//.env.local
```
cp .env .env.local
```
//mysql .env.local
```
DATABASE_URL="mysql://root:secret@database:3306/symfony_docker?serverVersion=8.0"
```
//cmd for database
```
symfony console make:migration
# re-run # docker docker-compose down # and # docker-compose up -d --build
symfony console doctrine:migrations:migrate
```
//mysql
```
docker-compose exec database /bin/bash
mysql -u root -p symfony_docker
> show tables;
```
//encore

//install in bash php
```
composer require symfony/webpack-encore-bundle
```
//encor install in app directory
```
yarn install
```
//encore in app directory
```
yarn watch
```
//Using Sass/LESS/Stylus
```
yarn add sass-loader@^13.0.0 sass --dev
```
// assets/app.js
```
- import './styles/app.css';
+ import './styles/app.scss';
```
//change webpack.config.js
```
.enableSassLoader()
```
//create custom.scss for style code
```
custom.scss
```
//run in symfony-docker/app
```
yarn encore dev --watch
```
