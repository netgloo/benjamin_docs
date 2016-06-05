---
layout: default
title: Multi Language
permalink: /multi-language/
---

# Multi-Language

Benjamin supports multi-language websites using sub-directories URL structure. 
If you enable the multi-langauge support you will have, out of the box, something like this:

    http://example.com       --> Website in the default language
    http://example.com/en    --> Website in English language
    http://example.com/fr    --> Website in French language

The subdirectories `en` and `fr` will be respectively the root for the website in English and the website in French.
At the web site root will be served the website in your default language.

If properly used, this method allow your website to be correctly indexed by search engines on all available languages.


## Enable Multi-Langauge Support

You can enable the Benjamin's multi-langauge support simply adding language folders inside the `resources/lang` directory. 
Each folder should be a supported language:

```
/resources
  /lang
    /en
      messages.php
    /es
      messages.php
    /fr
      messages.php
```

Within each language specific folder you should put a `messages.php` file containing language strings.

Learn more about the `lang` folder and language strings in Laravel from [here](https://laravel.com/docs/5.2/localization#introduction).

**Note**: if the multi-language is enabled, the language sub-directory name will always take precedence over views' names. So if you have, for example, the folder `resources/lang/en` and also a view `/en.blade.php`, this last one will always be ignored (if 'en' is not the default locale) and for the url `/en`  will be served the `/index.blade.php` view with `en` as locale (and not `/en.blade.php`).


## Configurations

Open the `config/app.php` configuration file and set these values:

- `locale`: the default locale. This locale will be used to serve your website in the default language, without any language sub-directory. There must be a language folder inside `resources/lang` having this value.
- `fallback_locale`: if a string is not translated for the current locale, will be used this one as fallback (usually it is set equals to the default locale).


## Translated Texts Inside Views

You can use the `trans` helper function to translate messages inside your views. For example:

    <h1>{{ trans('messages.welcome') }}</h1>

Will print the string with key `welcome` inside the `messages.php` file for the current locale.

<!--
The right `messages.php` file will be choosen from the folder with the name of the current locale (e.g. the folder `en/` for the locale `en`) inside `resources/lang/`.
-->

Take a look at the [Laravel's documentation](https://laravel.com/docs/5.2/localization#basic-usage) for more features about how to use `trans` function and messages.


## Links

If you enable the multi-language support, you have to properly handle links in your web pages to be coherent with the current language.

You can use the `trlink` helper function for links, inside Blade's views, in this way:

    <a href="{{ trlink('/about') }}">About</a>
    <a href="{{ trlink('page2') }}">Page 2</a>
    <a href="{{ trlink('http://www.example.com') }}">Example</a>

Absolute paths (e.g. `/about`) are translated for the current language, automatically prepending the language subdirectory.
Relative paths (e.g. `page1`) are translated to absolute paths where the root is the language subdirectory.
Absolute urls (e.g. `http://www.example.com`) are left as they are. 

So, if the current locale is `en` (and it is not set as default) and the current page is `/some/page1`, then the three links above will be translated to:

    <a href="/en/about">About</a>
    <a href="/en/some/page2">Page 2</a>
    <a href="http://www.example.com">Example</a>


## Switch Language

In the frontend you may want to provide a way for the user to switch the language. You can do it with a link for each language you support.

Use the `langswitch` helper function to create links for switching languages on the current page:

    <a href="{{ langswitch('en') }}" data-bj-ignore >English</a>
    <a href="{{ langswitch('es') }}" data-bj-ignore >Spanish</a>

Supposing the current page is `/about` and the default language is `es`, the code above will produce these links:

    <a href="/en/about" data-bj-ignore >English</a>
    <a href="/about" data-bj-ignore >Spanish</a>

Note that you don't have to give the current page to `langswitch`, it will be automatically deduced on each page.

The `data-bj-ignore` attribute will tell to Benjamin.js to ignore these links from the "on-client" navigation. When a user will click one of these links the website will be reloaded from the server in the selected language.


## Get active language

Within views you can get the active language with the `$activeLang` variable:

    @if ($activeLang == 'en')
      <!-- ... -->
    @endif


<!--
## Example

Look an example of a website with Benjamin configured for multilanguage on our demo here:

TODO
-->

-----

Next: [Website Deployment]({{ '/website-deployment/' | prepend: site.github.url }})
