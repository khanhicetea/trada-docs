---
date: 2016-07-03T21:07:13+01:00
title: Introduction
type: index
weight: 0
---

## Trada Framework 

Trada (Trà Đá - name of simple and the best drink in Vietnam) is very lightweight framework – it is built from scratch using [Silex 2](http://silex.sensiolabs.org/) and [Symfony Components](https://symfony.com/components) that supports lazy load components.

It only loads what you need for the request via a smart Denpendencies Injection Container [Pimple](http://pimple.sensiolabs.org/).

> Say in simple, it's a skeleton of Silex 2 that helps you can build a web application faster, easier and more extendable.

![Sifoni Admin Panel](/images/sifoni-admin.png)

## Features

- Simple but good as its name
- Very user-friendly design insprired by Laravel 5 
- Exposes an intuitive and concise API that is fun to use
- Run fast (faster than Laravel 5, Symfony Framework)
- Abstraction HTTP Request-Response, that supports [StackPHP](http://stackphp.com/) and [PHP-PM](https://github.com/php-pm/php-pm)
- Enough to build a Website or RESTful server with handy tools :
  - Migration by [phinx](https://phinx.org/)
  - Query Builder and ORM by [Eloquent](https://laravel.com/docs/5.2/eloquent)
  - Console Commands by [Symfony Console](https://symfony.com/doc/current/components/console/index.html)
  - [WebProfiler](https://github.com/silexphp/Silex-WebProfiler) Toolbar
  - [Monolog](https://github.com/Seldaek/monolog)
- Extra configuration options to extend the framework.

See the [getting started guide]({{< relref "getting-started/index.md" >}}) for instructions how to get
it up and running.

## Acknowledgements

Thanks to [Fabien Potencier](http://fabien.potencier.org/) for creating Silex and Symfony Components. 
