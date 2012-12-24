---
title: Merging Email Archives
layout: post
---

This year I decided to use the holiday season to clean up my hard
disk.  I found a couple of old email archive directories that I wanted
to merge.  They contain emails both in mbox and maildir format and
potentially duplicates.  First I want to merge them, then remove
duplicates, then potentially import them into Thunderbird.  My
Thunderbird email archive is still in mbox format, as I'm not sure how
reliable the newish maildir support is and whether it is possible to
set the archive directories to read-only.  Even though the end result will potentially be mbox archives, I decided to do the merging in maildir format, as this is a very easy format to work with.  A quick refresher: maildir stores each email in its own file, each mail folder is represented by a folder on the file system with 3 subfolders named cur, new and tmp.  While a mail program would move mail between these subfolders during normal operation, the final destination of emails is always the cur folder.  This means that a very simple workflow presents itself:

1. Convert all email to maildir format 
2. Merge the contents of the cur subfolders
3. Remove duplicates

## Convert all email to maildir format 

Google found this post to the dovecot mailing list http://dovecot.org/list/dovecot/2008-March/029736.html

I ran the python script attached to the post as 

{% highlight sh %}
python mb2md.py -i inbox.mbox -o inbox.maildir
{% endhighlight %}

which did the job.

## Merge the contents of the cur subfolders
## Remove duplicates