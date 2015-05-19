---
published: true
layout: post
category: linux
tags: 
  - recovery
  - rescue
  - ext4
---


# Data Recovery

first thing is to detach file system

    sudo unmount -l /dev/sda1

## debugfs
* ref. [Debug a file system](http://users.nccs.gov/~fwang2/linux/lk_debugfs.html)
* ref. [debugfs Command Examples](http://www.cs.montana.edu/courses/309/topics/4-disks/debugfs_example.html)

Find inode of file

    % ls -li testfile
    5505914 -rw-rw-r-- 1 k100 k100 0  5月 19 10:42 testfile

If inode is available, use **cat** or **dump** to dump file

    % sudo debugfs /dev/sdb1
    debugfs 1.42.9 (4-Feb-2014)
    debugfs:  cat <5505914>
    debugfs:  dump <5505914> /tmp/testfile

Use grep to find data block, and find inode from data block by **icheck**

    % grep --only-matching --byte-offset --binary --text --perl-regexp "\x51\x46\x49" /dev/sda1
    25165824:QFI
    222100898:QFI

    % sudo debugfs /dev/sdb1
    debugfs 1.42.9 (4-Feb-2014)
    debugfs:  icheck 25165824

## Ext4magic

* [Official Site](http://ext4magic.sourceforge.net/ext4magic_en.html)
* Based on ext3grep and extundelete
* example: [ext4 recover deleted files (undelete) using ext4magic on CentOS 6](http://source.kohlerville.com/2013/02/ext4-recover-deleted-files-undelete-using-ext4magic-on-centos-6/)

## Reference

* [深入理解ext4（一）----extent區段](http://blog.csdn.net/sara4321/article/details/8609610)
* [EXT4介紹與分析](http://blog.csdn.net/robinlovesnow/article/details/7567037)
