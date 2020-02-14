---
layout: single
title:  "Google Analytics for Jekyll themed github webpages"
date:   2020-02-14
---

Google analytics can be used for free to add tracking to your jekyll themed github website. In this post I am gonna show you a simple configuration using a javascript code snippet to add analytics to your website.

The reason for putting this post is I couldn't find a simple instruction on how to add tracking to my website. Either the posts were outdated or few things weren't working for me. 

#### Requirements:
   - You have google account
   - You have jekyll theme github website (obviously)

### STEPS:

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">1. Javascript code snippet for analytics</h2>

<!-- Copy the below snippet to your `analytics.html` page at the very end. -->
```javascript
<script>
  window.ga = window.ga || function () { (ga.q = ga.q || []).push(arguments) }; ga.l = +new Date;
  ga('create', '{{ site.google_analytics }}', 'auto');
  ga('send', 'pageview');
</script>
<script async src='https://www.google-analytics.com/analytics.js'></script>
```

> The `analytics.html` page would be in `_includes` directory.
> If it is not there for your project, better search for it in another directory or just create it in your `_includes` directory.

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">2. Code snippet for applying analytics on all pages</h2>

_OPTION 1:_

Copy the below snippet to your `default.html` page under the `<head>` section after the `% include analytics.html` 

```javascript
{% if site.google_analytics and jekyll.environment == 'production' %}
{% include analytics.html %}
{% endif %}

```

My head section looks something like this after copying the code snippet

```javascript

{% include head.html %}
{% include head/custom.html %}
{% if site.google_analytics and jekyll.environment == 'production' %}
{% include analytics.html %}
{% endif %}

```

> The `default.html` page would be in `_layouts` directory.

_OPTION 2:_

Ideally, the above code snippet should go in `head.html` under its `<head>` section.
But for some, the `head.html` does not exist.
In my case, the `head.html` was there but didn't have a boilerplate head section already defined. So, I didn't bother to create the tag and copy paste there.

If you have it then you can copy paste there or try and create the tag and then paste it. It should work but I haven't tried that.

> __Important:__ Put the snippet under `<head>` section.

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">3. Get Tracking ID from Google Analytics Website</h2>

The next step is to go to (analytics.google.com/)[https://analytics.google.com/] and create a _tracking ID_.

To create a tracking ID for your website you need to register your website.
To do that create a property and fill the simple details asked.

<h2 style="color: #55acee; font-size:26px; font-family: 'Lucida Grande'">4. Copy the Tracking ID</h2>

Go back to your project and paste the newly created tracking ID from your google analytics page to `_config.yml`

> The `_config.yml` would be under the parent directory of your github.io project directory.

Mine looks somewhat like this
```
# Analytics
analytics:
  provider               : "google"
  google:
    tracking_id          : "UA-XXXXXXXX-X"
    anonymize_ip         : # true, false (default)
```

> Please mind that you need to replace the placeholder if already there with your new tracking ID. (you would say, obviously ;)).

If you managed to follow me till here, then CONGRATULATIONS!!!
Theoretically it should work now :P. You can push your changes to production and see for yourself.

Cheers and happy hacking.



