---
date: 2016-03-09T00:11:02+01:00
title: The Basics 
weight: 20
---

## Routing

All Trada routes are defined in `app/config/routing.php` file, which is automatically loaded by the framework. Its returned a 2-dimensional array for grouping the routes and easier to read.

```php
<?php

return array(
    '/' => array(
        '/' => 'HomeController:index:home::get',
        '/hello/{name}' => ['HomeController', 'hello', 'hello_person', 'name=world'],
    ),
);
```

- The key of first dimensional is a routing prefix of its routing options.
- Next, keys of second dimensional is routing pattern of the route
- Each value can be a 5 items array or a string separated by `:` charater
    - First item : name of Controller will handle
    - Second item : name of method will handle the request, method must have a suffix `Action`
    - Third item : name of route, use for generating url 
    - Fourth item : default values of route, example `page=1,parent_id=2`
    - Fifth item : HTTP methods of route, default is `get|post` means `get` or `post` 

## Controllers

Instead of defining all of your request handling logic in a single `routing.php` file, Trada organize this behavior using Controller classes. Controllers can group related HTTP request handling logic into a class. Controllers are stored in the `app/controller` directory with namespace `App\Controller`.

The mission of controller is return a HTTP response (returned string will be converted to Response object). We have some ways to return responses :

### Return a twig view

- `app/controller/HomeController.php` :

```php
<?php

namespace App\Controller;

use Sifoni\Controller\Base;

class HomeController extends Base
{
    // This method will return a twig view of 'home.html.twig' with data layout inside $data
    public function helloAction($name)
    {
        $data['name'] = $name;
        return $this->render('home.html.twig', $data);
    }
}
```

- `app/view/home.html.twig` :

```twig
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello {{ name|capitalize|e }} ! :)</title>
</head>
<body>
    <h1>Welcome to {{ name|capitalize|e }} ! :)</h1>
</body>
</html>
```

### Return string content

```php
// .....
    public function saySomethingAction($text)
    {
        return "Simon says : " . $text; 
    }
// ...
```

### Return JSON response
```php
// .....
    public function getNumbersAction()
    {
        $data['posts'] = [
            ['a' => 1, 'b' => 2],
            ['a' => 2, 'b' => 4],
            ['a' => 3, 'b' => 6],
        ];
        return $this->json($data);
    }
// ...
```

### Return redirect response
```php
// .....
    public function loginAction()
    {
        return $this->redirect('dashboard'); // redirect to url of route named 'dashboard' 
    }
// ...
```

## Configuration

Before you are able to run your website you should take a few minute to adjust some information in the `.env` (copy from `.env.example` and open the file in an editor)

```bash
APP_VENDOR_NAME=App
APP_KEY="This is secret key"

DEBUG=true
WEB_PROFILTER=true

TIMEZONE="Asia/Ho_Chi_Minh"

DB_DRIVER=mysql
DB_HOST=localhost
DB_DATABASE=trada
DB_USERNAME=root
DB_PASSWORD=passwd
DB_CHARSET=utf8
DB_COLLATION=utf8_unicode_ci
```

## Options

### Application config

- Change the `APP_VENDOR` if you want to replace the main namespace of all application classes. (Not recommended)
- Change the `APP_SECRET` could help your application more secure when encrypt the data.

### Debug mode

In order to debug errors (development environment), you should enable `DEBUG=true` to see detail of errors while develop the web.

### Timezone

- Change the `TIMEZONE` by your main application timezone. List of support timezones is [here](https://secure.php.net/manual/en/timezones.php)

### Database config

- `DB_DRIVER` is main database driver, supports :
    - `sqlite` is SQLite
    - `sqlsrv` is SQL Server
    - `mysql` is MySQL
    - `pgsql` is PostgreSQL
- `DB_HOST` is database hostname
- `DB_DATABASE` is database name
- `DB_USERNAME` is database user
- `DB_PASSWORD` is database user password
- `DB_CHARSET` is database charset
- `DB_COLLATION` is database collation

