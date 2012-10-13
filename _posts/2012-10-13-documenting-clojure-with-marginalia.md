---
layout: post
title: Documenting Clojure Code with Marginalia
tags: [clojure]
---

I like to use a code documentation tool that generates nice looking
html documentation.  For my Python code I generally use
[Sphinx](http://sphinx.pocoo.org), which is best suited to write
reference manual style documentation.  As a matter of taste, I prefer
this over the javadoc/doxygen style API documentation.  I was curious
to see which tools the clojure world uses and stumbled upon
[Marginalia](https://github.com/fogus/marginalia).  While I am not yet
sure whether I will like this documentation style in the end, it
certainly looks *different*.  Have a look at the [marginalia
documentation](http://fogus.me/fun/marginalia/) and see for yourself.

## Integration with Leiningen 2

Looking at the Marginalia Readme and following the installation instruction for Leiningen presented me with

{% highlight bash %}
flo@boeserwolf:~/development/dogsofdax$ lein marg
'marg' is not a task. See 'lein help'.
{% endhighlight %}

It took me longer than it probably should have to realize that I am using Leiningen 2 (lein2), which changes the format in which plugins are requested.

With lein2, you can either list the lein-marginalia plugin as part of your user profile in ~/.lein/profiles.clj,

{% highlight clojure %}
{:user {:plugins [[lein-marginalia "0.7.1"]
                  ]}}
{% endhighlight %}

or add it as a plugin to the defproject macro in project.clj:

{% highlight clojure %}
  :plugins [[lein-marginalia "0.7.1"]]  
{% endhighlight %}

