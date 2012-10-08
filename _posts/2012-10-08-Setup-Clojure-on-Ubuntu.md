---
title: Setting up Clojure on Ubuntu
layout: post
---

I have been a happy Python user for many years now, both in my day job
and for recreational programming.  However, I decided to learn
Clojure, mainly because I am fascinated by Lisps since a long time.
This post describes my setup.

I started out installing Clojure 1.2 and Leiningen 1.x as these are
available in the apt repository for Ubuntu 12.04.  These were enough
to get my feet wet.  For the first project I wanted to switch
to Clojure 1.4.  The easiest way to get a new Clojure version
installed is to add it as a dependency to the project.clj file:

{% highlight clojure %}
  :dependencies [[org.clojure/clojure "1.4.0"]]
{% endhighlight %}

The next time you run lein, eg lein repl, Leiningen installs the
requested clojure version first.  Pretty cool. I wish one of the
Python build tools could do this.

## Upgrade to Emacs 24

While not strictly neccessary, I took the opportunity to upgrade to
Emacs 24.  I used [Damien Cassous
PPA](https://launchpad.net/~cassou/+archive/emacs) and added the
Marmalade package archive to my .emacs:

{% highlight elisp %}

(setq package-archives '(("gnu" . "http://elpa.gnu.org/packages/")

			 ("marmalade" . "http://marmalade-repo.org/packages/")
			 ("melpa" . "http://melpa.milkbox.net/packages/")))

{% endhighlight %}

This makes it really easy to install nREPL mode, which is [apparently
the recommended Clojure REPL these days](http://technomancy.us/163).
Simply open the Emacs package manager (`M-x list-packages`) and select
`nREPL` and `clojure-mode` from the list.

One final snag I hit was that nREPL needs Leiningen 2, while Ubuntu
12.04 comes with Leiningen 1.  I followed the [upgrade
guide](https://github.com/technomancy/leiningen/wiki/Upgrading) which
was straightforward.

