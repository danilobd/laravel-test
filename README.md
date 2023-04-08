# Laravel Test API Project

[![Tests](https://github.com/danilobd/laravel-test/workflows/ci/badge.svg)](https://github.com/danilobd/laravel-test/actions)

## Installation

Clone this repository and with Docker (or Docker Desktop) running, execute to build and install all dependencies:

``` sh

docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    laravelsail/php82-composer:latest \
    composer install --ignore-platform-reqs

```

Then run the containers:

```sh
sail up -d
```

Create the tables in database and add test data:

```sh
sail artisan migrate --seed
```

To stop the containers, run:

```sh
sail stop
```

To remove all containers, run:

```sh
sail down
```

### Using

- Access the PHP application in **http://localhost/**

- The *MeiliSearch* service is accessible in **http://localhost:7700/**

- The *MailPit* can be accessible in **http://localhost:8025/**

To access the databases, you can use the [Table Plus](https://tableplus.com/) app to use both MySql and Redis databases.


#### Alias to Sail command (Optional)

Execute the command to be able to run Sail commands as like:

```sh
sail up
```

Otherwise you need to execute like:

```sh
./vendor/bin/sail up -d
```

On terminal run:

```sh
alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail'
```

Or put this in your *~/.zshrc* or *~/.bashrc* file to be always available, then restart your terminal.

### Services

- **PHP**
- **MySQL**
- **Redis**
- MeiliSearch
- Mailpit
- Selenium

## Testing

To run the automated tests execute the command:

```sh
sail test
```

To see the code coverage run:

```sh
sail test --coverage
```

To generate code coverage report in HTML, run:

``` sh
sail bin phpunit --coverage-html reports/
```

# Deployment

```sh
composer install --optimize-autoloader --no-dev
php artisan config:cache
php artisan route:cache
php artisan view:cache

```