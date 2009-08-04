---
layout: post
title: Environment Setup
---

I've had scattered notes on setting up a new development computer from
scratch in Backpack for years now. Hopefully collecting them here will
make it more likely that they'll stay up-to-date. This is *my*
environment, probably not what I'd suggest for you.

I don't necessarily install all of these all the time (MySQL), but I'd
still rather have all the instructions in one place.

These notes assume Mac OS X Leopard, with the developer tools
installed.

## Fundamental Stuff

* [1Password][1p]. It knows all.
* [Dropbox][db]. Sync folders transparently.
* [Emacs][em]. I'm building [Emacs 23 from source][es].
* [Inconsolata][in]. My favorite programming font.
* [LaunchBar][lb]. Useless without it.
* [MacPorts][mp]. I use this to manage as much dev stuff as I can.
* [Things][th]. What am I supposed to be doing right now?

## Important Stuff

* [Adium][ad]. I like talking on the digital internets.
* [FireFox][ff]. I use Safari for daily browsing, but FF for lots of dev.
* [Growl][gr]. I turn off most notifications, but it's still good to have.
* [Mail Unread Menu][mu]. Since I hide the dock and mute everything.
* [Parallels][pa]. Only for testing stuff on Windows.
* [Shimo][sh]. VPNs are dumb, but Shimo is pretty.
* [Transmit][tr]. FTP, SFTP, S3.
* [Tweetie][tw]. WHAT ARE YOU DOING?!
* [Xmarks][xm]. Cross-browser, cross-machine bookmark syncing.

## Nice Stuff

* [FuzzyClock][fc]. Normal clocks are boring.
* [GitNub][gn]. Good for quick repo history scans.
* [Skitch][sk]. Screenshots + sharing.

## Profile, Emacs Configuration, etc.

I keep most of my dotfiles in a [Git repository][df] and symlink
them. I do the same thing with Dropbox for 1Password and Things.

## RubyGems

    $ sudo gem update --system

## Git

    $ sudo port install git-core +svn +doc
    $ git config --global user.name John Barnette
    $ git config --global user.email jbarnette@gmail.com

## MySQL

    $ sudo port install mysql5-server
    $ sudo mysql_install_db5 --user=mysql
    $ sudo port load mysql5-server

Add `/opt/local/lib/mysql5/bin` to your path, and this should work:

    $ mysql -uroot

### MySQL Ruby Bindings

    sudo gem install mysql --                                    \
      --with-mysql-include=/opt/local/include/mysql5             \
      --with-mysql-lib=/opt/local/lib/mysql5                     \
      --with-mysql-config=/opt/local/lib/mysql5/bin/mysql_config

[1p]: http://agilewebsolutions.com/products/1Password
[ad]: http://adium.im
[db]: https://www.getdropbox.com
[df]: http://github.com/jbarnette/dotfiles
[em]: http://www.gnu.org/software/emacs
[es]: http://www.emacswiki.org/emacs/EmacsOnMacOS#toc2
[fc]: http://www.objectpark.org/FuzzyClock.html
[ff]: http://getfirefox.com
[gn]: http://wiki.github.com/Caged/gitnub
[gr]: http://growl.info
[in]: http://www.levien.com/type/myfonts/inconsolata.html
[lb]: http://www.obdev.at/products/launchbar/index.html
[mp]: http://www.macports.org
[mu]: http://www.loganrockmore.com/MailUnreadMenu
[pa]: http://www.parallels.com
[sh]: http://www.shimoapp.com
[sk]: http://skitch.com
[th]: http://culturedcode.com/things
[tr]: http://www.panic.com/transmit
[tw]: http://www.atebits.com/tweetie-mac
[xm]: http://www.xmarks.com
