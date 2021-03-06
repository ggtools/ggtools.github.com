---
title: "Download and install"
layout: lrsync
---

Downloads
---------

LRSync is released under the terms of [GNU General Public License v3](http://www.gnu.org/licenses/gpl-3.0.html). It is available in either [zip](https://github.com/ggtools/LRSync/zipball/master) or [tar.gz](https://github.com/ggtools/LRSync/tarball/master) formats.

### Third party downloads

No special installation is required on MacOS X as `sqlite3` and `rsync` are installed by the system. However on Windows with Cygwin you'll need to install the `sqlite3` and `rsync` packages.

Installation
------------

As a bash script, LRSync will be a little be more tricky to use and install than the use Mac OS X applications. Some skills with the terminal is definitly a good thing.

1. Unzip/untar LRSync to a _convenient_ location for instance `/opt/LRSync` for a system wide installation or `~/Applications/LRSync` for a user only installation.

1. Rename the extracted folder or create a symbolic link.

1. Add the LRSync directory to your PATH.

1. Check LRSync is accessible.

For instance in a user only installation with a symlink:

{% highlight bash %}
$ mkdir -p ~/Applications/LRSync
$ cd ~/Applications/LRSync
$ tar -xzf ~/Downloads/ggtools-LRSync-0.2.0-0-g9fa4867.tar.gz
$ ln -sf ggtools-LRSync-9fa4867 LRSync-current
$ PATH="$PATH:~/Applications/LRSync/LRSync-current"
$ lrsync.sh -h
{% endhighlight %}
Which should gave an output similar to:
{% highlight text %}
lrsync -c catalog [-q] [-r repo_dir] operation

	-c catalog  : the catalog to be converted, must be declared in lrsync.ini
	-f          : force conversion even if source is older than destination or
                  if the post conversion tests fail.
	-q          : remove output during conversion
	-r repo_dir : directory containing the reference catalogs
	
	operation   : fromRepo or toRepo to synchronize a catalog from or to the repo.
	              display to display a list of the root folders of the catalog.
{% endhighlight %}
