---
layout: default
title: Getting Started
permalink: /getting-started/
---

# Getting Started

<!--
## Introduction
-->

<!--
Benjamin is a pre-configured [Laravel](http://laravel.com/docs/installation) application. 
-->

[Install Benjamin](#installation), run composer and [launch the application](#start-the-application) with `php artisan serve`. Then you can start to build your website.

Once installed, you can start [adding new web pages](#add-new-pages). You don't have to worry about URLs, they will be automatically deduced by the page's filename stripping out the file extension.

Client side you will have, out of the box, an instant navigation for each link between your web pages. Benjamin will use the `pushState` api to update the URL when a page is changed, but it will automatically fallback to a *standard* navigation if the browser doesn't support `pushState`. 

**Note**: using Benjamin you have to think to your website like a [Single-Page Application](https://en.wikipedia.org/wiki/Single-page_application) since web pages are directly changed client-side. This have some implications on how the javascript code is loaded and executed. Take a look to the [Scripts](#scripts) section for more informations.

After you added some web pages, you may want to create [layouts](#layouts) to share a common structure between pages, or you can play with [page transitions and callbacks](#page-transitions) if you need to control the switching process from a page to another one. Also you may need to add a [contact form](#forms) in your website that will [send an email](#sending-emails) when it is triggered, or you can enable the [multi-language support](#multi-language) if your website need to provide more than one language. You will find all this really simple and straightforward.

### For what kind of websites you should consider Benjamin

You should consider to use Benjmian if your website is a *static website*, in the sense that content of pages is fixed and can change only when you *manually* modify it. 
<!--
Also Benjamin works by pre-loading client-side the html code for **all** website's pages, so use it for website with a relative small number of pages (let's say less than one hundred of pages, but some test are required).
-->

This is a list of functionalities already supported by Benjamin:

- Page layout
- Manage transitions from a page to another one (client-side)
- Sending forms to the server
- Multi-language

If your website must have all or some of above functionalities you should consider to use Benjamin. If your website needs more advanced features perhaps you may want to use other solutions or you can take in account to customize your Benjamin installation adding features you need.

In general, you should avoid to use Benjamin if your website:

- have some dynamic content that could changes on different requests;
- is constantly growing in the number of pages and constantly needs to add a lot of new pages;
- needs authenticated users.

## Requirements

You need to have [composer](http://getcomposer.org/) installed on your PC in order to be able to download all Benjamin's dependencies. This is not really required on the production server.

Also, these are PHP requirements from [Laravel](https://laravel.com/docs/5.2#installation):

- PHP >= 5.5.9
- Extensions: OpenSSL PHP, PDO PHP, Mbstring PHP, Tokenizer PHP.

## Installation

[Download Benjamin 1.0](https://github.com/netgloo/benjamin/archive/1.0.0.zip), extract it and rename the folder with the name of your project, e.g. `my-website`. Then from inside the project's folder type:

``` bash
$ composer install
$ cp .env.example .env
$ php artisan key:generate
```

The first command will download all PHP dependencies. Then you will create the `.env` file copying it from the example provided. This file will store all your configurations. Finally, the last command will automatically generate an unique [application key](https://laravel.com/docs/5.2#installation) for you, storing it inside the `.env` file.

### Troubleshooting

If it is the first time you run Composer, can happen that you get an error like the one below when you run `composer install`:

``` 
Could not fetch https://api.github.com/repos/username/repo/zipball/863df9687835c62aa423a22412d26fa2ebde3fd3, please create a GitHub OAuth token to go over the API rate limit
Head to https://github.com/settings/tokens/new?scopes=repo&description=Composer+on+my+PC
to retrieve a token. It will be stored in "/home/user/.composer/auth.json" for future use by Composer.
Token (hidden):
```

To solve this you need a GitHub account, then simply follow instructions from the error message, that are:

- Go to https://github.com/settings/tokens/new?scopes=repo&description=Composer+on+my+PC to retrive a token to using with Composer.
- Give the token to composer pasting it when prompted, after `Token (hidden):`.

<!--
### Configurations

If you want to start developing the website you can [start now](#start-the-application). You don't have to configure anything more.

However, if you need some advanced configuration, you may find some useful information on how to configure a new Laravel application from [here](https://laravel.com/docs/5.2/configuration).
-->

## Start The Application

From the application root's folder just type:

``` bash
$ php artisan serve
```

Then visit [http://localhost:8000](http://localhost:8000) and you will see a welcome page.

Now you can start adding your own [web pages and folders](#website-pages), and building your website.

**Note**: in the production server you shouldn't use `php artisan serve` but rely on Apache (or Nginx) instead. Take a look on the [Website Deployment](#website-deployment) section for more informations.

## Application Structure

A Benjamin website is a [Laravel](https://laravel.com) application, so you can take a look [here](https://laravel.com/docs/5.2/structure#the-root-directory) for any detail about the whole application's structure.

However we want to create simple and static websites, so it is not needed to know in depth the whole structure.
You can build the website working only inside these two folders:

- `/public`: you should put here all public resources, as images, javascripts, stylesheets and fonts.
- `/resources`: inside `resources` there are views (the website pages), languages files (if your website is multi-language) and raw assets as SASS or development version of javascript files.


-----

Next: [Website Pages]({{ '/website-pages/' | prepend: site.github.url }})
