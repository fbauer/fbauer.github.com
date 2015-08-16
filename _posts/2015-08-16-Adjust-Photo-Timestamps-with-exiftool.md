---
title: Adjust Photo Timestamps with exiftool
layout: post
---

During the last trip, we took photos with multiple cameras. Back home
I noticed that the pictures taken by one camera had wrong timestamps.
Here's how I fixed that using exiftool.

Shift the dates of all photos taken by a Canon camera by 1:10:

{% highlight bash %}
  $ exiftool -if '$make eq "Canon"' -AllDates+=1:10 *
{% endhighlight %}

Rename the photos according to the new creation date:

{% highlight bash %}
 $ exiftool -if '$make eq "Canon"' "-FileName<CreateDate" -d "adamello_%Y%m%d_%H%M%S.%%e" *.jpg
 $ exiftool -if '$make eq "Canon"' "-FileName<CreateDate" -d "adamello_%Y%m%d_%H%M%S.%%e" *.mov
 $ rm *_original
{% endhighlight %}

exiftool knows not to overwrite existing pictures. To prevent having
two photos the same file name, I shifted the creation date of one of
them by one second.

{% highlight bash %}
 $ exiftool -if '$make eq "Canon"' -AllDates+=0:0:1 adamello_20150810_163212.jpg
 $ exiftool -if '$make eq "Canon"' "-FileName<CreateDate" -d "adamello_%Y%m%d_%H%M%S.%%e" adamello_20150810_163212.jpg
 $ rm *_original
{% endhighlight %}
