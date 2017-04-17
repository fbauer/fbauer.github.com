---
title: Adjust Photo Timestamps with Exiftool and Shotwell
layout: post
---

A semi-interactive workflow that I came up with to adjust timestamps
in photos taken with different cameras whose clocks were not in sync.

First, tag all photos with the camera model:

{% highlight bash %}
  $ exiftool "-Keywords<Model" .
{% endhighlight %}

This enables filtering photos by camera model in Shotwell, as
Shotwell does not allow filtering by EXIF tags.

Then adjust timestamps in the shotwell db, without changing the
photos until they are sorted correctly. Search for photos of the
same event taken by multiple cameras, give them a temporary tag and
use these tagged events to align the timestamps in the photos. 
Mark all photos tagged with a camera model and use the adjust
timestamp feature to shift the timestamps of all photos by the same
event. Don't update the image metadata until the result looks right,
then do a final pass and store the information in the photo.

Rename the photos using their new EXIF timestamps.

{% highlight bash %}
  $ exiftool "-FileName<CreateDate" -d 'description_%Y%m%d_%H%M%S%%-c.%%e' .
{% endhighlight %}

