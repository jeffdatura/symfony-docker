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
```
//run docker
```
docker-compose up -d --build
docker-compose exec php /bin/bash
```

//symfony
```
symfony check:requirements
symfony new .
cp .env .env.local
DATABASE_URL="mysql://root:secret@database:3306/symfony_docker?serverVersion=8.0"
symfony console make:migration
symfony console doctrine:migrations:migrate
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

//encor install in root directory
yarn install

//encore in app directory
yarn watch
```
