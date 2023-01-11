# laravel-geoip-world-cities (Laravel 5,6,7,8)

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Latest Unstable Version](https://poser.pugx.org/moharrum/laravel-geoip-world-cities/v/unstable)](https://packagist.org/packages/moharrum/laravel-geoip-world-cities)
[![Software License][ico-license]](https://github.com/moharrum/laravel-geoip-world-cities/blob/master/LICENSE.md)
[![Total Downloads][ico-downloads]][link-downloads]

Laravel GeoIP World Cities is package that provides [MaxMind](https://www.maxmind.com/en/free-world-cities-database) Free World Cities Database support for laravel applications.

## Contents

- [Introduction](#introduction)
- [Before installing](#before-installing)
- [Installation](#installation)
- [Table structure](#table-structure)
- [Example](#example)
- [Troubleshooting](#troubleshooting)
- [Changelog](#changelog)
- [Contributing](#contributing)
- [Credits](#credits)
- [License](#license)


## Introduction

Includes city, region, country, latitude and longitude. This database doesn't contain any IP addresses. It's simply a listing of all the cities in the world.

This package simply loads the data provided in `worldcitiespop.txt.gz` file by [MaxMind](https://www.maxmind.com/) into a database and provides a `City` model to query the table.

## Before installing

If you are looking for the Laravel 4 version, take a look [Branch 1.0](https://github.com/moharrum/laravel-geoip-world-cities/tree/1.0).

## Installation

**Note: This package is a bit large, ~40MB, installing and seeding the data could take a while.**

Add `moharrum/laravel-geoip-world-cities` to `composer.json`:

    "moharrum/laravel-geoip-world-cities": "2.*"

for the last stable version, or

    "moharrum/laravel-geoip-world-cities": "dev-master"

for the latest version.

Run `composer update` to pull down laravel-geoip-world-cities.

Edit `config/app.php` and add the `provider` (ignore this step if you have package discovery enabled)

```php
    'providers' => [
        Moharrum\LaravelGeoIPWorldCities\LaravelGeoIPWorldCitiesServiceProvider::class,
    ]
```

Optionally add the alias.

```php
    'aliases' => [
        'Cities' => Moharrum\LaravelGeoIPWorldCities\Facade::class,
    ]
```

Configure MySQL and PDO, insert the following code in `config/database.php`:

```php
    'mysql' => [
        'options'   => [PDO::MYSQL_ATTR_LOCAL_INFILE => true],
    ],
```

Publishing the configuration file, this is where you can change the default table name

    php artisan vendor:publish

Publishing the migration and seeder files

    php artisan cities:migration
    php artisan cities:seeder

To make sure the data is seeded insert the following code in `seeds/DatabaseSeeder.php`

```php
    // Seeding the cities
    $this->call(CitiesTableSeeder::class);
    $this->command->info('Seeded the cities table ...');
```

You may now run:

    php artisan migrate --seed

After running this command the filled cities table will be available

## Table structure

| id       | country  | city      | city_ascii  | region  | population  | latitude  | longitude  |
| -------- | ---------| --------- | ----------- | ------- | ----------- | --------- | ---------- |
| ..       | ..       | ..        | ..          | ..      | ..          | ..        | ..         |
| 2685662  | sd       | Khartoum  | khartoum    | 29      | 1974780     | 15.588056 | 32.534167  |
| ..       | ..       | ..        | ..          | ..      | ..          | ..        | ..         |

## Example

The package provides a `City` model which can be used to query the data

```php
    \Moharrum\LaravelGeoIPWorldCities\City::whereCity('Khartoum')->first();
```

## Troubleshooting

If you are getting a `ReflectionException` when trying to seed

```php
    [ReflectionException]                   
    Class CitiesTableSeeder does not exist
```

run:

```php
    composer dump-autoload
```

and try again.

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) and [CONDUCT](CONDUCT.md) for details.

## Credits

- [MaxMind](https://www.maxmind.com)
- [Khalid Moharrum][link-author]
- [MCMatters](https://github.com/MCMatters)

## License

MaxMind WorldCities [License](http://download.maxmind.com/download/geoip/database/LICENSE_WC.txt).

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/moharrum/laravel-geoip-world-cities.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/moharrum/laravel-geoip-world-cities.svg?style=flat-square

[link-packagist]: https://packagist.org/packages/moharrum/laravel-geoip-world-cities
[link-downloads]: https://packagist.org/packages/moharrum/laravel-geoip-world-cities
[link-author]: https://github.com/moharrum
[link-contributors]: ../../contributors
