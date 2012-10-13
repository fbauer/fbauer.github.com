---
title: Proxy settings on Windows 7
tags: [emacs, windows, python]
layout: post
---

A quick reminder for myself on how to configure proxy settings on
windows for the Emacs package manager and python virtualenv / pip.

## Emacs proxy for elpa

Add this to custom-set-variables in your .emacs. This is the proxy for the
 URL package which can also be configured from the configuration menu. 

{% highlight clojure %}
(custom-set-variables
 '(url-proxy-services (quote (("http" . "<url>:<port>"))))
)
{% endhighlight %}

## pip and easy_install

Either on the console

{% highlight shell %}
set http_proxy=http://<url>:<port>
{% endhighlight %}

or set permanently in environment variables under 
Control Panel/System/Advanced/Environmental Variables.
