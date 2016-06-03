---
layout: default
title: Website Pages
permalink: /website-pages/
---

# Website Pages

Website pages are inside the folder `resources/views`. Each page file must be a [Blade view](https://laravel.com/docs/5.2/blade), ending with the extension `.blade.php`.

A Blade view is essentially a PHP file plus some really nice directives and an easy way for defining layouts. If you don't already know Blade, you will learn it effortless and very quickly. Take a look [here](https://laravel.com/docs/5.2/blade) for all the informations you need to know.

## Add New Pages

Just add new Blade views inside `resources/views`. 

Views will be available as pages for your website. The URL path will be composed by the view's path without the `.blade.php` extension. For example:

- The view `resources/views/page.blade.php` will be served at `http://example.com/page`.
- The view `resources/views/inside/a/folder.blade.php` will be served at `http://example.com/inside/a/folder`.

There are some exceptions to these rules, like the [index page](#index-page) served at the website's root path or some [special filenames and folder names](#ignored-pages-and-folders) that will be ignored by Benjamin.

Also, you should avoid to use names already used inside the `/public` folder. For example, if you have the folder `public/images` containing your images, you can't create a view named `images.blade.php`. 
<!--since at the url `http://example.com/images` will be served the `images` folder inside `public` and the view will be shadowed and never available. -->

To be correctly served with Benjamin, each view must follow the page structure described [next](#page-structure).

### Page Structure

Each page file you add inside `resources/views` must:

- Extend `$benjamin`, with the directive `@extends($benjamin)`.
- Define a section `title`: you should set here the page's title that will go inside the `<title>` tag.
- Define a section `body`: here you can put the page's HTML content that will be inside the `<body>` tag.

For example, this is a valid Benjamin's page file:

``` html
<!-- File: resources/views/example.blade.php -->
@extends($benjamin)

@section('title')
  Page title
@endsection

@section('body')
  <p>
    Here the page's HTML content ...
  </p>
@endsection
```

The above view will generate the following HTML page:

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <script defer src="/vendor/jquery/jquery-1.11.3.min.js"></script>
  <script defer src="/vendor/benjamin/Benjamin.js"></script>
  <title>Page title</title>
</head>
<body>
  <p>
    Here the page's HTML content ...
  </p>
</body>
</html>
```

<!--
When you download Benjamin the first time, you will find under `resources/views` two example pages: `index.blade.php` and `example.blade.php`. The first one is the [website's index page](#index-page), served at the website's root (e.g. `http://example.com/`), and it is defined as a *stand-alone* view extending directly `$benjamin`. The second one instead is a normal page, served at the path defined by its filename (e.g. `http://example.com/page`); this view use a layout structure, extending a layout view defined inside the `layouts` folder. You can see more about layouts [here](#layouts).
-->

## Body Class Attribute

You may want to specify a value for the body's `class` attribute. You can do it using the `bodyClass` parameter, extending `$benjamin`:

```
@extends($benjamin, ['bodyClass' => 'some-class'])
```

The value `some-class` will be placed inside the `class` attribute in the `<body>` tag.

## Page Head

The content of the `<head>` tag will be shared between all the pages. Only the `<title>` will change when a page is changed.

You can find the head's content inside the view `layouts/head.blade.php`.

You can modify the head's content as you want, but you should leave jQuery and Benjamin.js inside it for the proper functioning of the Benjamin platform.

## Index Page

For the website's root will be served the content of the view named `index.blade.php` inside `resources/views`.

For example, if the below content is inside `resources/views/index.blade.php`:

``` html
@extends($benjamin)

@section('title', 'Welcome')

@section('body')
  <h1>Welcome</h1>
@endsection
```

will be showed this HTML page at `http://example.com/`:

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <!-- scripts ... -->
  <title>Welcome</title>
</head>
<body>
  <h1>Welcome</h1>
</body>
</html>
```

## Ignored Pages And Folders

Following pages and folders, inside `resources/views`, will be ignored by Benjamin:

- Files not ending with `.blade.php`.
- Each file or directory starting with `_`: you can use the underscore prefix to temporarily disable a page or a whole folder from your website.
- Directory `/errors`: inside this directory you should put [error pages](#error-pages).
- Directory `/layouts`: use this folder to store all your layouts and layouts' parts (like the footer or the header). This is also the default folder for the [head view](#page-head).
- Directory `/templates`: you can optionally use this folder if you have commons pieces used around the website and you want to keep them separate from the layout folder.
- Directory `/vendor`: this is a Laravel's special folder and its content is ignored.
- Directory `/app`: you can use this folder in the case you want to add some functionalities to Benjamin and you need custom views, not processed by Benjamin itself.

## Error Pages

You can create a custom page for the 404 HTTP error (page not found) simply creating the view file `resources/views/errors/404.blade.php`.

Note that this page is ignored by the Benjamin platform and doesn't needs to follow the [page structure](#page-structure) of other web pages (then doesn't needs to extends `$benjamin`) but needs to define its own `<html>` and `<head>` tags.

## Links

If the browser [support the `pushState` api](http://caniuse.com/#search=pushState), each link between two pages internal to the website will be handled by Benjamin client side. When the user will click on a link for an internal page, the target page will be loaded directly client side, without any call to the server. This allow a true smooth navigation between pages, without requiring any loading time.

You don't need to do anything, just normally add links in your web pages.

### Ignored Links

By default following links will be ignored by Benjamin and will have a *standard* behaviour:

- Links poiting to another domain.
- Links with an application protocol different from the current one.
- Links with `data-bj-ignore` attribute.

## Ready Callback

In the Javascript code, use Benjamin's [`ready`](#ready) callback to execute JavaScript code each time a page is loaded:

``` javascript
// File: public/js/main.js

Benjamin.on({
  
  'ready': function() {

    // Here your javascript code executed when a page is ready

    return;
  },

});
```

You should use this callback in place of jQuery's `$(document).ready`. If you have some JavaScript code that needs to run only once, use Benjamin's [`init`](#init) callback.

Take a look in the [Scripts](#scripts) section for more informations about how to properly use JavaScript in Benjamin.


-----

Next: [Layouts]({{ '/layouts/' | prepend: site.github.url }})
