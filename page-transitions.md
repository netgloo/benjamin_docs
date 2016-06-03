---
layout: default
title: Page Transitions
permalink: /page-transitions/
---

# Page Transitions

If an user is on page `/a` and click on a link for page `/b`, following callbacks are executed:

1. `out` global.
1. `out` for page `/a`.
1. `in` global.
1. `in` for page `/b`.
1. `ready` global.
1. `ready` for page `/b`.

When a page is loaded directly from the server or when a page is opened through back/forward browser's buttons, only `ready` callbacks are executed.

## Callbacks

There are two types of callbacks: **global** and **per-page**. First ones are always executed independently on the current page. Second ones are executed only on the given page.

You can set your own callback functions, inside your JavaScript code, in this way:

``` javascript

// Global callbacks

Benjamin.on({
  'init': function() {  },
  'ready': function() {  },
  'out': function(next) { return next(); },
  'in': function(next) { return next(); },
});

// Per-page callbacks

Benjamin.on('/', {
  'ready': function() {  },
  'out': function(next) { return next(); },
  'in': function(next) { return next(); },
});

Benjamin.on('/example', {
  'ready': function() {  },
  'out': function(next) { return next(); },
  'in': function(next) { return next(); },
});

// ...

```

**Note**: do not put above callbacks definitions inside jQuery's `$(document).ready`.

### init ( )

Initialize your things.

- Executed only once, when the website is loaded from the server.
- Executed before any `ready` callback.
- Only global version exists.

### ready ( )

The page is ready.

- Executed when the page is loaded form the server in the jQuery's document ready event (`$(document).ready`) and after the `in` callback when the page is changed client-side.
- Executed also when the browser's history is navigated (back and forward).
- This is a good place for binding things on your document (e.g. using `$('.some-element').on(...)`).
- Both global and per-page versions exists. The global one will be always executed first.

### out (`next`)

The page is going to be changed with another page.

- If you are on page `/a` and a link to an internal page is clicked, this callback is executed before the content of `/a` is replaced.
- It is **not** executed when the page is loaded from the server neither when the page is showed browsing the browser's history.
- Both global and per-page versions exists. The global one will be always executed first.
- Remember to call `next()` to execute the `in` callback for the page that will be displayed.

### in (`next`)

The page is changed.

- If a link to `/a` is clicked, this callback is executed when the content of the page `/a` is inside the body.
- The document's title and the page url refers to the page `/a`.
- It is **not** executed when the page is loaded from the server neither when the page is showed browsing the browser's history.
- Both global and per-page versions exists. The global one will be always executed first.
- Remember to call `next()` to execute the `ready` callback for page `/a`.

<!--
### Effects

TODO

Note: you should avoid to apply transitions effects directly to the `body` element. 
-->


-----

Next: [Forms]({{ '/forms/' | prepend: site.github.url }})
