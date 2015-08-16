---
title: Adjust Photo Timestamps with exiftool
layout: post
---

Shift the dates of photos taken by a Canon camera by 1:10:

{% highlight bash %}
  $ exiftool -if '$make eq "Canon"' -AllDates+=1:10 *
{% endhighlight %}

Rename the files according to the new creation date:

{% highlight bash %}
exiftool -if '$make eq "Canon"' "-FileName<CreateDate" -d "adamello_%Y%m%d_%H%M%S.%%e" *.jpg
exiftool -if '$make eq "Canon"' "-FileName<CreateDate" -d "adamello_%Y%m%d_%H%M%S.%%e" *.mov
rm *_original
{% endhighlight %}


Special case photos that would overwrite another one. Shift their creation date by one second.

{% highlight bash %}
exiftool -if '$make eq "Canon"' -AllDates+=0:0:1 adamello_20150810_163212.jpg
exiftool -if '$make eq "Canon"' "-FileName<CreateDate" -d "adamello_%Y%m%d_%H%M%S.%%e" adamello_20150810_163212.jpg
rm *_original
{% endhighlight %}