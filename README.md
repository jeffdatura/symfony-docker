# symfony-docker

# codesandbox
```
docker-compose.yml => image: mysql:5.7

//in workspace terminal for added extensions php
apt install php8.1-{bcmath,xml,fpm,mysql,zip,intl,ldap,gd,cli,bz2,curl,mbstring,pgsql,opcache,soap,cgi}

DATABASE_URL="mysql://root:secret@database:3306/symfony_docker?serverVersion=5.7"

docker ps

docker exec -it <container_id> /bin/bash

ls -a
```

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
//pour codesandbox
docker exec -it <container_id> /bin/bash
```
//symfony cmd
```
symfony check:requirements
```
//create project
```
symfony new . --version="6.2.*" --webapp
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
//pour codesandbox
docker exec -it <container_id> /bin/bash
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
yarn encore dev --watch
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
//bootstrap in app directory
```
yarn add bootstrap --dev

//for css
//assets/styles/app.css
@import "bootstrap";

//for scss
//assets/styles/app.scss
@import "~bootstrap/scss/bootstrap";

// customize some Bootstrap variables
$primary: darken(#428bca, 20%);

yarn encore dev --watch
```
//Import JavaScript Bootstrap
```
yarn add jquery @popperjs/core --dev

// app.js
import './styles/app.scss';

//jquery
const $ = require('jquery');

// start the Stimulus application
import './bootstrap';

//javascript
import './controllers/hello_controller'
```
