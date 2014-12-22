# detect-proxy

### This repo is unmaintained and this technique may not work anymore.

By [Feross Aboukhadijeh](http://feross.org).

This code allows a malicious website to **detect whether the user is browsing through a proxy or not** by using image tags. Proxies are often used by corporations, political dissidents, and privacy conscience Internet users because they can provide additional security or anonymous Internet browsing.

## Here's how it works

Firefox uses square brackets `[ ]` to denote IPv6 addresses, but this notation also works to describe IPv4 addresses (I'm not sure exactly why).

So, if we embed an image with `src="http://[74.207.246.197]/pic.jpg"` into a page, Firefox automatically resolves `[74.207.246.197]` into the IP address `74.207.246.197`.

However, if the user is browsing through a proxy, this automatic resolution doesn't happen. Instead, Firefox asks the proxy to do a DNS lookup for the "domain" `[74.207.246.197]`, which obviously fails since it's not a valid domain name.

Most proxies don't know how to handle the bracketed domain, so the DNS lookup fails. I've tested this on [Tor](http://www.torproject.org) (popular proxy for anonymous Internet browsing), [PHP Proxy](http://sourceforge.net/projects/php-proxy/) and [CGI Proxy](http://www.jmarshall.com/tools/cgiproxy/) (the top two web-based proxies), and [Proxify](http://www.proxify.com) (popular commercial web proxy).

So, if the image fails to load, we know that the user is browsing through a proxy. Add some Javascript to detect when the image fails to load and you've got a working proxy detector.

**[View the demo](http://feross.org/hacks/detect-proxy/).**
(Works in: Firefox 3, Safari 5)

This, of course, assumes that the user is not blocking cross-domain requests. Also, my implementation requires Javascript to be enabled, but that's not a necessity.

## Read more about this

On [my blog](http://feross.org/detect-proxy-usage-in-firefox/).

## MIT License

Copyright (c) 2012 Feross Aboukhadijeh 

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
