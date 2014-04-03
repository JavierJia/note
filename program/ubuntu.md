# chinese input method
follow the intruction from this post :
    http://pinyinjoe.com/linux/ubuntu-12-chinese-setup.htm

# link eclipse on the sidebar
    http://www.comoke.com/index.php/2012/06/install-eclipse-in-launcher-ubuntu-12-04-unity/

# about locale:
https://help.ubuntu.com/community/Locale

# 12.04 enable remote desk
Search in the "dash" for remote; you will find an option for "Desktop Sharing"

# Check cpu info
```
cat /proc/cpuinfo
cat /proc/meminfo
dmesg
lspci
```

# change ulimit
http://hbase.apache.org/book.html#ulimit

If you are on Ubuntu you will need to make the following changes:

In the file /etc/security/limits.conf add a line like:
```
hadoop  -       nofile  32768
Replace hadoop with whatever user is running Hadoop and HBase. If you have separate users, you will need 2 entries, one for each user. In the same file set nproc hard and soft limits. For example:

hadoop soft/hard nproc 32000
```

In the file /etc/pam.d/common-session add as the last line in the file:

```
session required  pam_limits.so
```
Otherwise the changes in /etc/security/limits.conf won't be applied.

Don't forget to log out and back in again for the changes to take effect!
