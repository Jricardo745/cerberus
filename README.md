# Placetopay multitenancy package

This package is based on the first version of package `spatie/laravel-multitenancy/`.

Because it is a customization, it requires override steps mentioned below for proper installation.

[More information about the package](https://github.com/spatie/laravel-multitenancy/tree/v1).

This package aims to standardize the configuration of the ``tenants`` table of the landlord database, in addition to reducing the number of queries made to the same database by using cache.

## Prerequsites
- `php7.4+`
- `Laravel 7.0+`

## Limitations:
- cache: you need to use a driver that support tags like redis, cache tags are not supported when using the file, dynamodb, or database cache drivers
- jobs: we recommend use redis or sqs to process queues

## Installation

This package can be installed via composer:

``` bash
composer require "placetopay/cerberus:^1.0"
```

### Publishing the config file

You must publish the config file:

``` bash
php artisan vendor:publish --provider="Placetopay\Cerberus\TenancyServiceProvider" --tag="config"
```

### Publishing the migrate file

``` bash
php artisan vendor:publish --provider="Placetopay\Cerberus\TenancyServiceProvider" --tag="migrations"
```

### To considers
The migration of the landlord table in relation to the spatie package was modified, adding a `config` field of json type, 
with which it's intended to centralize the configuration that is carried out in front of each tenant, 
in this field you can define the connection to the database using the following structure.
```
{
	"app": {
		"url": "...",
		"name": "..."
	},
	"database": {
		"connections": {
			"mysql": {
				"host": "localhost",
				"port": "3306",
				"database": "tenant_db",
			}
		}
	}
}
```