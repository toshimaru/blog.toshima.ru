---
layout: post
title: How to install Disqus for AMP
tags: disqus
---

I've installed [Disqus](https://disqus.com/) to my blog.

[Comment is now available! \| Toshimaru’s Blog](/2020/01/05/add-disqus.html)

## Official setup instruction

[disqus-install-examples/google-amp at master · disqus/disqus-install-examples](https://github.com/disqus/disqus-install-examples/tree/master/google-amp)

## Create different domain

The domain of this blog is `blog.toshima.ru`. Firstly, You need to create another domain (FQDN) to host Disqus HTML.

I've created [disqus.toshima.ru](https://disqus.toshima.ru/) and put the Disqus HTML on it (Hosted by GitHub Pages).

## Disqus HTML

I made a little change to `disqus_config` function to build `identifier`, `url` and `title` values from query parameter.

```html
<div id="disqus_thread"></div>
<script>
window.addEventListener('message', receiveMessage, false);
function receiveMessage(event)
{
    if (event.data) {
        var msg;
        try {
            msg = JSON.parse(event.data);
        } catch (err) {
            // Do nothing
        }
        if (!msg)
            return false;

        if (msg.name === 'resize' || msg.name === 'rendered') {
            window.parent.postMessage({
              sentinel: 'amp',
              type: 'embed-size',
              height: msg.data.height
            }, '*');
        }
    }
}
</script>
<script>
/**
 *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
 *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables
 */
var disqus_config = function () {
    var params = new URLSearchParams(window.location.search);
    this.page.identifier = params.get("id");
    this.page.url = params.get("url");
    this.page.title = params.get("title");
};
(function() {  // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');

    s.src = 'https://toshimarusblog.disqus.com/embed.js';

    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
})();
</script>
```

Source code: <https://github.com/toshimaru/disqus.toshima.ru/blob/master/blog-toshima-ru.html>

## Disqus Config

| Config | Description |
| --- | --- |
| `identifier` | Tells the Disqus service how to identify the current page.<br>If this.page.identifier is undefined, the page's URL will be used. The URL can be unreliable, such as when renaming an article slug or changing domains. |
| `url`  | Tells the Disqus service the URL of the current page. |
| `title`  | Tells the Disqus service the title of the current page. |

ref. [JavaScript configuration variables | Disqus](https://help.disqus.com/en/articles/1717084-javascript-configuration-variables)

## Reference

- [Disqus for Google's AMP \| Disqus](https://help.disqus.com/en/articles/1717282-disqus-for-google-s-amp)
- [disqus-install-examples/google-amp at master · disqus/disqus-install-examples](https://github.com/disqus/disqus-install-examples/tree/master/google-amp)

## See Also

- [Get Query Parameters in JavaScript \| Toshimaru’s Blog](/2020/01/04/get-query-parameters-in-javascript.html)
