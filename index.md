---
layout: default
---

# Quick Start

## Get Benjamin

[Download the latest version](https://github.com/netgloo/benjamin/archive/master.zip) from GitHub.

Extract it and rename the folder with the name of your project.

## Getting Started

Run these commands within the project folder:

```
$ composer install
$ cp .env.example .env
$ php artisan key:generate
$ php artisan serve
```

Go to [http://localhost:8000](http://localhost:8000) and you will see a welcome page.

Have fun!


# Benjamin

## Contents

* [Getting Started]({{ '/getting-started/' | prepend: site.github.url }})
* [Website Pages]({{ '/website-pages/' | prepend: site.github.url }})
* [Layouts]({{ '/layouts/' | prepend: site.github.url }})
* [Scripts]({{ '/scripts/' | prepend: site.github.url }})
* [Page Transitions]({{ '/page-transitions/' | prepend: site.github.url }})
* [Forms]({{ '/forms/' | prepend: site.github.url }})
* [Multi-Language]({{ '/multi-language/' | prepend: site.github.url }})
* [Website Deployment]({{ '/website-deployment/' | prepend: site.github.url }})
* [How It Works]({{ '/how-it-works/' | prepend: site.github.url }})
* [Credits]({{ '/credits/' | prepend: site.github.url }})

<!-- 
* [Getting Started](#getting-started) 
* [Setup]
  * [Installation]
  * ...
* [Basics](#basics) 
   * [Website Pages](#website-pages)
   * ...
   * [Development Workflow](#development-workflow) 
   * ...
* [Advanced](#advanced) 
   * [How It Works](#how-it-works)
   * [Optimizations](#optimizations) 
   * [Customizations](#customizations) 
   * ...
-->

## What is Benjamin

Benjamin is a PHP/JavaScript platform for easily building *static websites* with a really instant and smooth navigation out of the box.

<!--
You can try a Benjamin powered website here: [http://benjamin.netgloo.com](http://benjamin.netgloo.com)
-->

### Everyone loves fast websites

Benjamin is made for building fast websites. With Benjamin you can rapidly create websites that load fast and with an amazing smooth and instant navigation between pages. Website's pages will be changed directly client-side, without any call to the server and without any loading time.

### Easy development

Benjamin is easy to use. You can start just adding new web pages and your website will be ready right away. Also you will find some very useful features out of the box. Like a painless [multi-language support](#multi-language) and an easy way for adding [transitions effects](#page-transitions) changing page. 

### Run everywhere

Almost all hosting services supports PHP nowadays, also on basic and cheaper plans. Benjamin is built on [Laravel](http://laravel.com/) and it only requires [PHP with some basic extensions](https://laravel.com/docs/5.2#installation). Very likely it will run on your current and favourite hosting service.

### Flexible

The main aim of Benjamin is to provide a platform for small and light websites. But no ones will stopping you to add new features if you need them. If you already have some experience with [Laravel](http://laravel.com/) framework, you will find really easy add your custom functionalities, like new routes, controllers, a database connection and anything else your website needs.

<!--
## Who is using Benjamin?

Netgloo's website is built using Benjamin. Take a look: [http://netgloo.com/en](http://netgloo.com/en).
-->


----

Next: [Getting Started]({{ '/getting-started/' | prepend: site.github.url }})
