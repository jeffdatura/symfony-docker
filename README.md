# symfony-docker

//Dockerfile PHP
```
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony
```
//root project
```
sudo chown -R $(whoami) .
```

//dependancies maybe not need all
```
composer require --dev symfony/profiler-pack
composer require symfony/maker-bundle --dev
composer req --dev maker ormfixtures fakerphp/faker
composer req doctrine twig
composer require form validator security-csrf annotations

//index.php if profiler hide
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

//enter in application
docker-compose exec php /bin/bash
```

//symfony
```
symfony check:requirements
symfony new . --version="6.1.*" --webapp
cp .env .env.local

DATABASE_URL="mysql://root:secret@database:3306/symfony_docker?serverVersion=8.0"

symfony console make:migration
//re-run docker docker-compose down ::: docker-compose up -d --build
symfony console doctrine:migrations:migrate

//fixtures if you want
symfony console make:fixture
symfony console doctrine:fixtures:load
```

//mysql
```
docker-compose exec database /bin/bash
mysql -u root -p symfony_docker
> show tables;
```

//encor
```
//install in bash php
composer require symfony/webpack-encore-bundle

//encor install in app directory
yarn install

//encore in app directory
yarn watch

//for bootstrap
yarn add sass-loader@^13.0.0 sass --dev

//change webpack.config.js
.enableSassLoader()

//change app.css to and create custom.scss
app.scss
custom.scss

//run in app
yarn watch

//bootstrap
yarn add bootstrap --dev
yarn add jquery @popperjs/core --dev

//in app.scss

@import "custom";
@import "~bootstrap/scss/bootstrap";


body {
    background-color: lightgray;
}

//change assets/app.js

/*
 * Welcome to your app's main JavaScript file!
 *
 * We recommend including the built version of this JavaScript file
 * (and its CSS file) in your base layout (base.html.twig).
 */

// any CSS you import will output into a single css file (app.css in this case)
import './styles/app.scss';

// You can specify which plugins you need
import { Tooltip, Toast, Popover } from 'bootstrap';

// start the Stimulus application
import './bootstrap';

//run in app
yarn watch
```
