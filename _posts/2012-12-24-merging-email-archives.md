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

Google found [this
post](http://dovecot.org/list/dovecot/2008-March/029736.html) to the
dovecot mailing list by Aaron Gallagher with a link to a [conversion
script](http://habnabit.org/mb2md.py.gz).

I ran the python script attached to the post as 

{% highlight sh %}
python mb2md.py -i inbox.mbox -o inbox.maildir
{% endhighlight %}

which did the job.

## Merge the contents of the cur subfolders

I decided on having three mail folders to simplify merging: inbox,
sent and drafts. As a first step, I created a new folder merged_mails
and used nautilus to copy all maildir folders there (I checked "view
hidden files", as some maildir folders were hidden).  Nautilus per
default merges folders with the same name, and also can be told to
skip overwriting files with the same name (I am sure that equally
named mail files have the same content).  As a next step, I again used
Nautilus to merge all remaining inbox archive folders (named like
inbox_archive, inbox_2008 and the like) into the inbox folder. It is
sufficient to copy the cur, tmp and new subfolders; any index files
outside of those can be deleted.

## Remove duplicates

I used a python script called
[doublesdetector.py](http://sebsauvage.net/python/doublesdetector.py)
by sebsauvage to spit out a list of duplicated messages.

{% highlight sh %}
python -i doublesdetector.py .
{% endhighlight %}

I ran the script with the -i option to python, so python dropped me
into an interactive interpreter after running the script. The detected
duplicate files are stored in a global dict named doubles.  I deleted
all but the first file with the following snippet:

{% highlight python %}
>>> delete = [v[1:] for v in doubles.values()]
>>> import os
>>> for fns in delete:
...     for fn in fns:
...             os.remove(fn)
... 
{% endhighlight %}

python -i is a very powerful feature in cases where the usual output
of a script is human readable and hard to post-process, but an
internal data structure is available that can be accessed directly
from an interactive interpreter.  It is a good idea to always
strive for a code structure in scripts that allows this workflow.  I.e. provide a main routine that returns a result and a passes this result on to a reporting function inside an 'if __name__ == "__main__":' block.

