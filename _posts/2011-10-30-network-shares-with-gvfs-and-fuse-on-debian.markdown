--- 
layout: post
title: Network shares with GVFS and FUSE on Debian
published: false
---

If you use Debian and want to mount Windows network shares in the path ~/.gvfs/pathtoshare, you have to install the packages gvfs-mount, fusesmb and fuse (should already be installed). Then add your user to the group 'fuse'. After a reboot, the shares should be mounted in your home folder, if you browse them with Nautilus.
