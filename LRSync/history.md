---
title: History
layout: lrsync
---

Introduction
------------

I was using LightRoom for quite a while on my PC as this is probably the best tool for photographer when it comes to organize or process photos. The moment I had a Macbook I had to find out a way to be able to work on both computer as smoothly as possible. Smoothly meaning:

* being able to work without network connection on the laptop
* keep the development parameters from one computer to the other one
 
In addition to this, I don't want to use an external storage to plug on the _working_ computer. I (should) have backup(s) but external storages are prone to be lost or damaged.

Searching on internet I found out that the solution to keep in sync two computers belong to one of the following categories:

1. **Synchronize photos**. This is a basic synchronization as it involves synchronizing only the photos and use the *synchronize folder* feature in LightRoom.

1. **Share photos and catalog**. This category can be implemented either by using an external hard drive (for instance in [Adobe's FAQ](http://kb2.adobe.com/cps/333/333736.html#main_Can_I_have_more_than_one_catalog_)) or by using some synchronization tool such as [Rsync][], [Chronosync][], [Dropbox][], etc. (See a very detailled explaination with [Unison][] on [Stackexchange](http://photo.stackexchange.com/questions/1558/what-is-the-best-way-to-synchronize-adobe-lightroom-databases-between-two-comput)).

1. **Export/Import catalog**. This category requires the user to use the _Export as catalog_ and _Import catalog_ features of LightRoom. (See [this one](http://www.peachpit.com/articles/article.aspx?p=1664584) for more details).

To make it short, none of the methods above satisfied me: the first one didn't preserve the development settings even when flushing metadata to the `xmp` file; the second one required extra handling in Lightroom since I use a PC and a Mac and the last one worked fine when you want to dump a shooting session from the laptop onto the studio computer but was tricky to implement when two way synchronization was required.

Lightroom Synchronization
-------------------------

In order to synchronize Lightroom on two computers, you need to handle the photos (along with the optional `xmp` files) and the Lightroom catalog. Optionally, you may also want to synchronize the previews. Some like to synchronize the previews and some don't. Previews are huge compared to the catalogs but having up to date previews available make Lightroom more responsible and you can even make some work with the photos being unavailable.

The photos is the easy part and most synchronization tools will do the job. As Lightroom philosophy is _don't touch the negatives_ most changes will be the addition of new photos. As a consequence I didn't focus on this part and delegate it to the very capable [rsync][].

The catalog is an [SQLite][] database. Synchronization between my Mac and my PC requires to convert the catalog contents from the Mac structure to the PC structure and vice versa. Fortunately catalogs are compatible between Mac and PC and the conversion only requires to change the path to the _root folders_.

My setup
--------
 
My photos and the Lightroom catalogs are stored on a NAS. The PC is accessing the photos directly on the NAS while the catalog and the associated previews are replicated on a local drive using [Deltacopy](http://www.aboutmyip.com/AboutMyXApp/DeltaCopy.jsp) (a nice implementation of rsync for Windows). On the Mac side, I copy both photos, catalog and previews on the local drive using [rsync][].


[rsync]: http://en.wikipedia.org/wiki/Rsync
[chronosync]: http://econtechnologies.com/pages/cs/chrono_overview.html
[dropbox]: http://www.dropbox.com/
[unison]: http://www.cis.upenn.edu/~bcpierce/unison/
[sqlite]: http://www.sqlite.org/