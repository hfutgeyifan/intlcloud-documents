## Overview

This document describes how to install the cloud-init service. Cloud-init allows you to customize configurations during the first initialization of a CVM instance. If an image does not have the cloud-init service installed, instances launched by using the image cannot be initialized properly. 
You can use either of the following methods to install cloud-init:
- [Manually downloading the cloud-init source package](#ManualDown) 
- [Using the cloud-init package from the software source](#SoftSources)

## Notes
Before importing a Linux image, ensure that you have properly installed the cloud-init service in the image.

## Prerequisites
The server on which you want to install cloud-init is connected to the internet.

## Directions
<dx-tabs>
::: Manual download[](id:ManualDown)

### Downloading the cloud-init source package



<dx-alert infotype="explain" title="">
- **cloud-init-17.1.tar.gz** is recommended. You can visit https://launchpad.net/cloud-init/+download to download other versions.
- If the installation fails, you can try the [portable cloud-init package](#greeninitCloudInit)
</dx-alert>


Run the following command to download the cloud-init source package:
```shellsession
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

### Installing cloud-init
1. Run the following command to decompress the cloud-init installation package:
<dx-alert infotype="explain" title="">
If you are using the Ubuntu operating system, run this command with the "root" account.
</dx-alert>
```shellsession
tar -zxvf cloud-init-17.1.tar.gz 
```
2. Run the following command to enter the directory of cloud-init installation package. **cloud-init-17.1** is used in this example.
```shellsession
cd cloud-init-17.1
```
3. Install Python-pip according to the operating system version.
  - For CentOS 6/7, run the following command:
```shellsession
yum install python3-pip -y
```
  - For Ubuntu, run the following command:
```shellsession
apt-get -y install python3-pip
```
During installation, if an error such as "failed to install" or "installation package not found" occurs, see [Resolving Python-pip installation failures](#updateSoftware).
4. Run the following command to upgrade pip.
```
python3 -m pip install --upgrade pip 
```
5. Run the following command to install dependencies:
<dx-alert infotype="notice" title="">
Python 2.6 is not supported when cloud-init uses requests 2.20.0 or later. If the Python interpreter installed in the image environment is Python version 2.6 or earlier, run the `pip install 'requests&lt;2.20.0'` command to install requests 2.20.0 or later before installing the cloud-init dependencies.
</dx-alert>
```shellsession
pip3 install -r requirements.txt
```
6. Install the cloud-utils components corresponding to your OS version.
  - For CentOS 6, run the following command:
```shellsession
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
  - For CentOS 7, run the following command:
```shellsession
yum install cloud-utils-growpart -y
```
  - For Ubuntu, run the following command:
```shellsession
apt-get install cloud-guest-utils -y
```
7. Run the following command to install cloud-init:
```shellsession
python3 setup.py build 
```
```shellsession
python3 setup.py install --init-system systemd
``` <dx-alert infotype="notice" title="">
Options of `--init-system` can be `systemd`, `sysvinit`, `sysvinit_deb`, `sysvinit_freebsd`, `sysvinit_openrc`, `sysvinit_suse` or `upstart` [default: None]. Configure parameters based on the auto-start service management method of the operating system. If incorrect parameters are configured, the cloud-init service cannot automatically start upon system startup. This document uses the `systemd` as an example.
</dx-alert>


### Modifying the cloud-init configuration file

1. Download cloud.cfg for your operating system.
  - [Ubuntu](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg)
  - [CentOS](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg)
2. Replace the content of `/etc/cloud/cloud.cfg` with that of the downloaded cloud.cfg file.


### Adding syslog user
Run the following command to add a syslog user:
```shellsession
useradd syslog
```


### Configuring the auto-start of the cloud-init service on boot
- **If your operating system uses the systemd auto-start service management method, run the following commands.**
<dx-alert infotype="explain" title="">
To check whether the operating system uses systemd, run the `strings /sbin/init | grep "/lib/system"` command, and you will receive a return message.
</dx-alert>
 1. **Run the following command in Ubuntu or Debian:**
```shellsession
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **Run the following commands in all operating systems:**
```shellsession
systemctl enable cloud-init-local.service 
systemctl start cloud-init-local.service
systemctl enable cloud-init.service
systemctl start cloud-init.service
systemctl enable cloud-config.service
systemctl start cloud-config.service
systemctl enable cloud-final.service
systemctl start cloud-final.service
systemctl status cloud-init-local.service
systemctl status cloud-init.service
systemctl status cloud-config.service
systemctl status cloud-final.service
```
 3. **Run the following command in CentOS or Redhat.**
 Replace the content of `/lib/systemd/system/cloud-init-local.service` with the following:
```shellsession
[Unit]
Description=Initial cloud-init job (pre-networking)
Wants=network-pre.target
After=systemd-remount-fs.service
Before=NetworkManager.service
Before=network-pre.target
Before=shutdown.target
Conflicts=shutdown.target
RequiresMountsFor=/var/lib/cloud
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init --local
ExecStart=/bin/touch /run/cloud-init/network-config-ready
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
Replace the content of `/lib/systemd/system/cloud-init.service` with the following:
```shellsession
[Unit]
Description=Initial cloud-init job (metadata service crawler)
Wants=cloud-init-local.service
Wants=sshd-keygen.service
Wants=sshd.service
After=cloud-init-local.service
After=systemd-networkd-wait-online.service
After=networking.service
After=systemd-hostnamed.service
Before=network-online.target
Before=sshd-keygen.service
Before=sshd.service
Before=systemd-user-sessions.service
Conflicts=shutdown.target
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
- **If your operating system uses the sysvinit auto-start service management method, run the following commands:**
<dx-alert infotype="explain" title="">
To check whether the operating system uses sysvinit, run the `strings /sbin/init | grep "sysvinit"` command, and you will receive a return message.
</dx-alert>
```shellsession
chkconfig --add cloud-init-local
chkconfig --add cloud-init
chkconfig --add cloud-config
chkconfig --add cloud-final
chkconfig cloud-init-local on 
chkconfig cloud-init on 
chkconfig cloud-config on 
chkconfig cloud-final on 
```
:::
::: Using software source[](id:SoftSources)
### Installing cloud-init

Run the following command to install cloud-init:
```shellsession
apt-get/yum install cloud-init
```
<dx-alert infotype="explain" title="">
When you run `apt-get` or `yum` to install cloud-init, the version of cloud-init defaults to the version in the software source configured for the operating system. Note that in this case, the instances launched with the image may not be initialized as expected. Therefore, we recommend that you install the cloud-init by [manually downloading the cloud-init source package](#ManualDown).
</dx-alert>



### Modifying the cloud-init configuration file
1. Download cloud.cfg for your operating system.
 - [Ubuntu](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg)
 - [CentOS](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg)
2. Replace the content of `/etc/cloud/cloud.cfg` with that of the downloaded cloud.cfg file.
:::
</dx-tabs>



## Related Operations


<dx-alert infotype="notice" title="">
Do not restart the server after performing the following operations. Otherwise, you will need to perform them again.
</dx-alert>


1. Run the following commands to check whether the cloud-init configuration is successful.
```shellsession
cloud-init init --local
```
If the following information is returned, it indicates that the cloud-init has been successfully configured.
```shellsession
Cloud-init v. 20.1 running 'init-local' at Fri, 01 Apr 2022 01:26:11 +0000. Up 38.70 seconds.
```
2. Execute the following command to delete the cache records of cloud-init.
```shellsession
rm -rf /var/lib/cloud
```
3. Run the following command in Ubuntu or Debian:
``` shellsession
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
4. For Ubuntu or Debian, replace the content of `/etc/network/interfaces` with the following:
```shellsession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## See Also

### Portable cloud-init package[](id:greeninitCloudInit)
If the cloud-init service fails to be installed by [manually downloading the cloud-init source package](#ManualDown), complete the following steps to install cloud-init:
1. [Click here](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz) to obtain the portable cloud-init package.
2. Run the following command to decompress the portable cloud-init package:
```shellsession
tar xvf greeninit-x64-beta.tgz 
```
3. Run the following command to enter the decompressed portable cloud-init package directory. **greeninit** is used here.
```shellsession
cd greeninit
```
4. Run the following command to install cloud-init:
```shellsession
sh install.sh 
```

### Python-pip installation failure[](id:updateSoftware)
During installation, if an error such as "failed to install" or "installation package not found" occurs, troubleshoot it based on the operating system as follows:
<dx-tabs>
::: CentOS 6/7:
  1. Run the following command to configure the EPEL storage repository.
```shellsession
yum install epel-release -y
```
  2. Run the following command to install Python-pip.
```shellsession
yum install python3-pip -y
```
:::
::: Ubuntu:
  1. Run the following command to clear the cache.
```shellsession
apt-get clean all
```
  2. Run the following command to update the software package list.
```shellsession
apt-get update -y
```
  3. Run the following command to install Python-pip.
```shellsession
apt-get -y install python3-pip
```
:::
</dx-tabs>
