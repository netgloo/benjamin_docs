---
layout: default
title: Scripts
permalink: /scripts/
---

# Scripts

Using Benjamin you should think at your website as a [Single-Page Application](https://en.wikipedia.org/wiki/Single-page_application) (SPA). This implies that all the scripts included inside the `<head>` tag are loaded and executed only once, when the website is loaded from the server. If the page is dynamically loaded (i.e. it is loaded directly client-side) such scripts are **not** re-executed for the new page. jQuery's `$(document).ready` function also will run only when the website is loaded the first time and not on every loaded page.

Use Benjamin's [`ready`](#ready) callback to execute JavaScript code each time a page is loaded.

This callback will be executed each time a page will be loaded directly from the server, at the same time jQuery's `$(document).ready` would be executed, and each time a page will be dynamically loaded, after the page transition process is finished. The `readt` callback is a good place for all the code that initializes page's elements or code that binds page's events. Likely you can put in this callback all the code you would have put inside jQuery's `ready`.

If you have code that must be executed only once and not executed anymore, even changing page, you may want to use the [`init` callback](#init) instead.

**Note**: jQuery is already included inside Benjamin. You don't need to include it and you can just use it inside your custom JavaScript code.

## Scripts Inside The Body

Scripts inside the `<body>` tag are executed each time a page is loaded.

## Page Tracking With Google Analytics

If you want to [track pages views](https://developers.google.com/analytics/devguides/collection/analyticsjs/pages) with Google Analytics on your Benjamin website you should use the Google's [`analytics.js`](https://developers.google.com/analytics/devguides/collection/analyticsjs/) library. This library provides [functions and support for SPAs](https://developers.google.com/analytics/devguides/collection/analyticsjs/single-page-applications).

So, keeping in mind that web pages are loaded dynamically within a Benjamin website, you should add the following script inside the `<head>` tag:

``` html
<!-- Google Analytics -->
<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXX-Y', 'auto');
</script>
<!-- End Google Analytics -->
```

Replacing the string `'UA-XXXXX-Y'` with your tracking ID. 

The above JavaScript snippet is just the [Google's official one](https://developers.google.com/analytics/devguides/collection/analyticsjs/), without the last JavaScript instruction `ga('send', 'pageview')`. You should move such instruction inside the Benjamin's [`ready`](#ready) callback, in this way:

```
Benjamin.on({
  
  'ready': function() {

    // Add these two lines to tracking page views with Google Analytics
    ga('set', { page: window.location.pathname, title: document.title });
    ga('send', 'pageview');

    //

    return;
  },

});
```

The code above first will update the current page path and title for Google Analytics, with the `'set'` method, then will send a pageview hits. This will be executed on each page loaded, tracking all pages visited by an user.


-----

Next: [Page Transitions]({{ '/page-transitions/' | prepend: site.github.url }})
