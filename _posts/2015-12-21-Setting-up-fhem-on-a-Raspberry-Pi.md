---
title: Setting up fhem on a Raspberry Pi
layout: post
---

Login to the pi 

{% highlight bash %}
  $ ssh pi@<network address>
{% endhighlight %}

## Clean up some space

List installed packages sorted by size

{% highlight bash %}
   $ aptitude -O installsize -F'%p %I' search '~i'
{% endhighlight %}

sudo aptitude remove scratch libraspberrypi-doc
sudo aptitude remove gnome-icon-theme gnome-themes-standard-data gnome-accessibility-themes
pi@raspberrypi ~ $ sudo aptitude remove --purge desktop-base
sudo aptitude remove libwebkitgtk-1.0-common libwebkitgtk-3.0-common 
sudo aptitude remove --purge squeak-vm

Update raspian and configure unattended updates.
{% highlight bash %}
  $ pi@raspberrypi ~ $ sudo apt-get update
{% endhighlight %}

wget  http://fhem.de/fhem-5.7.deb
sudo dpkg -i fhem-5.7.deb 