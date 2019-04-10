---
layout: post
title: MacOS - Your disk space is critically low 
---

I've been receiving _Your disk space is critically low_ messages for the past couple months. 

It always occurs at a bad time, so I'd do the minimum. Clear downloads, empty the bin & sometimes reboot. This usually gave me about 10Gb free, which would last another few weeks, before I needed to repeat the process.

Annoyingly, most of the disk was used by the System.

> Time for a proper disk clean up!

There are plenty of commercial tools that will help. But, wearing my engineer's hat, I prefer to know how things work and wanted to do it manually. 

![macos-storage]({{ site.baseurl }}/images/macos-storage.png)

Running through the process below, I was able to free up more than 50Gb of space.

1. Table of contents
{:toc}



# The basics

Click on the *Apple* icon in the menu, select *About this mac* & then click on *Storage*.

This gives a quick overview of what's using your disk space.

Click the *Manage...* button and follow the recommendations. 

# Disk Usage command

It's easy to see what folders are using up disk space - either by the command line or Finder GUI.

In a terminal, use the `du` command to print out the disk usage of a folder or all folders. 

List disk space and in human readable form `-h` and summarize `-s`

```
du -sh .
```

Finder also has a feature which displays folder sizes. 

Open Finder, press *(⌘) + J* or select *View* > *Show View Options* from the menu. Then select the *Calculate all sizes* options. The size column will now show folder sizes.

![macos-storage]({{ site.baseurl }}/images/macos-finder-size.png)

# System Files - Cache 

My user cache in `~\Library\Caches` was very large.

```
du -sh ~/Library/Caches/
```

Quit all apps before clearing anything in the cache. It's apparently better to delete the contents of folders that the folders themselves - but I haven't properly researched whether this is true. If you're feeling lucky - clear it all, otherwise research the implications. I felt lucky & just deleted everything.

# Node / yarn / npm

If you're using Nodejs, npm or yarn you may find a large cache has built up over time. I found my `yarn` cache was over 8Gb and full of older packages. 

Time for a clean:

```
yarn cache clean
```

# Xcode Junk

## Archives 

If you're building and deploying iOS apps, you may have built up a large number of archives. I had 11Gb or archives - which was only about 5 months! These archives are only needed if the apps are still installed on customer devices (and then only if you haven't pushed the symbols to your error tracking service - eg. Firebase/crashlytics/bugsnag/instabug etc.)

Head to `~\Library\Developer\Xcode\Archives` and remove any folders you no longer need.

## Support for older devices

I had 15Gb of iOS Device Support. Most of these were for older iOS versions that we can safely delete.

Browse to `~\Library\Developer\Xcode\iOS DeviceSupport` and remove older iOS version folders. 

