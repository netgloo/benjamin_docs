---
layout: default
title: Layouts
permalink: /layouts/
---

# Layouts

If you need to structure your website using common layouts between pages you can just use [Blade's layout mechanisms](https://laravel.com/docs/5.2/blade#template-inheritance).

In general, within Benjamin you are free to use any Blade's directives, as `@extends`, `@section`, `@yield`, `@include`, and all the others. The only thing you have to keep in mind is that the resulting view must follow the page structure as described [here](#page-structure), that is: extend `$benjamin` (with `@extends($benjamin)`) and define sections `title` and `body`.

So, for example, we can define a `main` layout inside the `layouts` folder:

``` html
<!-- File: resources/views/layouts/main.blade.php -->

@extends($benjamin)

@section('title')
  @yield('page-title') - Website Name
@endsection

@section('body')
  
  <div class="content">

    @yield('content')

  </div>

@endsection
```

Note that the `layouts` folder's content is [ignored by Benjamin](#ignored-pages-and-folders), so it will be **not** exposed as web pages.

We can now define a couple of web pages using the above layout:

``` html
<!-- File: resources/views/index.blade.php -->

@extends('layouts.main')

@section('page-title', 'Index')

@section('content')
  <p>Index page content ...</p>
@endsection
```

``` html
<!-- File: resources/views/example.blade.php -->

@extends('layouts.main')

@section('page-title', 'Example')

@section('content')
  <p>Example page content ...</p>
@endsection
```

## Include Layout Parts

Continuing the example above, we can also include in our layout a header and a footer using the `@include` directive:

``` html
<!-- File: resources/views/layouts/main.blade.php -->

@extends($benjamin)

@section('title')
  @yield('page-title') - Website Name
@endsection

@section('body')
  
  @include('layouts.header')

  <div class="content">

    @yield('content')

  </div>

  @include('layouts.footer')

@endsection
```

```
<!-- File: resources/views/layouts/header.blade.php -->
<header> 
  Here there will be the header content ...
</header>
```

```
<!-- File: resources/views/layouts/footer.blade.php -->
<footer> 
  Here there will be the footer content ...
</footer>
```

-----

Next: [Scripts]({{ '/scripts/' | prepend: site.github.url }})
