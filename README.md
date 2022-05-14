Laravel Symphony Mailer CSS Inliner
===================================

![](https://github.com/ajohnson6494/laravel-symfony-mailer-css-inliner/workflows/CI/badge.svg)
[![Latest Stable Version](https://poser.pugx.org/ajohnson6494/laravel-symfony-mailer-css-inliner/v/stable.png)](https://packagist.org/packages/ajohnson6494/laravel-symfony-mailer-css-inliner)
[![License](https://poser.pugx.org/ajohnson6494/laravel-symfony-mailer-css-inliner/license.png)](https://packagist.org/packages/ajohnson6494/laravel-symfony-mailer-css-inliner)

## Why?
Most email clients won't render CSS (on a `<link>` or a `<style>`). The solution is inline your CSS directly on the HTML. Doing this by hand easily turns into unmantainable templates.
The goal of this package is to automate the process of inlining that CSS before sending the emails.

## Instalation and compatability

Requires PHP 8.1 and Laravel 9.0 or higher.

## How?
Using a wonderful [CSS inliner package](https://github.com/tijsverkoyen/CssToInlineStyles) wrapped in a Symfony Mailer plugin and served as a Service Provider it just works without any configuration.
Since this is a Symfony Mailer plugin, it will automatically inline your css when parsing an email template. You don't have to do anything!

Turns style tag:
```html
<html>
    <head>
        <style>
            h1 {
                font-size: 24px;
                color: #000;
            }
        </style>
    </head>
    <body>
        <h1>Hey you</h1>
    </body>
</html>
```
Or the link tag:
```html
<html>
    <head>
        <link rel="stylesheet" type="text/css" href="./tests/css/test.css">
    </head>
    <body>
        <h1>Hey you</h1>
    </body>
</html>
```

Into this:
```html
<html>
    <head>
        <style>
            h1 {
                font-size: 24px;
                color: #000;
            }
        </style>
    </head>
    <body>
        <h1 style="font-size: 24px; color: #000;">Hey you</h1>
    </body>
</html>
```

## Installation
This package needs Laravel 9.x.

Begin by installing this package through Composer. Require it directly from the Terminal to take the last stable version:
```bash
$ composer require ajohnson6494/laravel-symfony-mailer-css-inliner
```

At this point the inliner should be already working with the default options. If you want to fine-tune these options, you can do so by publishing the configuration file:
```bash
$ php artisan vendor:publish --provider='ajohnson6494\LaravelSymfonyMailerCssInliner\LaravelMailCssInlinerServiceProvider'
```
and changing the settings on the generated `config/css-inliner.php` file.

## Contributing
```bash
$ composer install
$ ./vendor/bin/phpunit
```

## Found a bug?
Please, let me know! Send a pull request or a patch. Questions? Ask! I will respond to all filed issues.

## Inspiration
This package is greatly inspired, and mostly copied, from [SwiftMailer CSS Inliner](https://github.com/OpenBuildings/swiftmailer-css-inliner). I just made an easy drop-in solution for Laravel.

## License
This package is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
