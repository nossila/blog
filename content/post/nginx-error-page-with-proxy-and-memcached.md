+++
title = "Nginx error_page with proxy and memcached"
date  = "2013-01-17T07:31:42-02:00"
draft = false
+++

Today I was trying to setup a custom error_page on my nginx server and I had some hard time trying to make it work so here's what I've learned.

When serving static files or have the simplest upstream configuration I could just easily set *error_page* and everything should work like its supposed to, like this:

{{< gist nossila 4557047 >}}

But when you make use of *error_page* as a way to redirect requests to a upstream server it does not work like expected. It's a common setup when you use memcached inside nginx to cache your pages like I do.

That does not work because nginx does not use *error_page* recursively by default. If the request comes from a *error_page* (like 404 on my example), nginx ignores every other *error_page* setting. So the only thing you should do is to set *[recursive_error_pages](http://wiki.nginx.org/HttpCoreModule#recursive_error_pages)* on and everything works like a charm:

{{< gist nossila 4557033 >}}

