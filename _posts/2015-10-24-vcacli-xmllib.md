---
layout: post
title: "vCloud Air vca-cli LIBXML2_2.9.0 Error"
date: 2015-10-24
excerpt: "vCloud Air CLI runtime error LIBXML2_2.9.0 not found"
---

This error appears when [vca-cli](https://github.com/vmware/vca-cli) version 14 is installed on Ubuntu 12

```shell
$ vca
Traceback (most recent call last):
  File "/usr/local/bin/vca", line 7, in <module>
    from vca_cli.vca_cli import cli
  File "/usr/local/lib/python2.7/dist-packages/vca_cli/vca_cli.py", line 22, in <module>
    from cmd_proc import CmdProc
  File "/usr/local/lib/python2.7/dist-packages/vca_cli/cmd_proc.py", line 21, in <module>
    from pyvcloud.vcloudair import VCA
  File "/usr/local/lib/python2.7/dist-packages/pyvcloud/vcloudair.py", line 36, in <module>
    from pyvcloud.schema.vcd.v1_5.schemas.vcloud import sessionType, organizationType, \
  File "/usr/local/lib/python2.7/dist-packages/pyvcloud/schema/vcd/v1_5/schemas/vcloud/vdcTemplateListType.py", \
line 25, in <module>
    from lxml import etree as etree_
ImportError: /usr/lib/x86_64-linux-gnu/libxml2.so.2: version `LIBXML2_2.9.0' not found \
(required by /usr/local/lib/python2.7/dist-packages/lxml/etree.so)

```

#### Reason:
There is a dependency on libxml-dev version 2.9.0 and Ubuntu 12 ships with version 2.7.8

The current installed version can be confirmed running the following command

```shell
sudo dpkg --list | grep libxml2
ii  libxml2                             2.7.8.dfsg-5.1ubuntu4.11            GNOME XML library
ii  libxml2-dev                         2.7.8.dfsg-5.1ubuntu4.11            Development files for the GNOME XML library
```


#### Solutions:

###### Option 1 - Install and use an  older release of vca-cli 

```shell
sudo pip install vca-cli==13
```

###### Option 2 - Upgrade Ubuntu to release 14 and then use the latest release of vca-cli

```shell
sudo -i
apt-get update
do-release-upgrade -f DistUpgradeViewNonInteractive
reboot
```
