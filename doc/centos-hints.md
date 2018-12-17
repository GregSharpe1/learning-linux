
# Problem: First install did not have access to the web

## Fix: Make sure the service is running

### ```$ service network start```

## Hints

* ```$ vi /etc/sysconfig/network-scripts/ifcfg-enp0s3``` set `ONBOOT=yes`

## Links used [Network setup CentOS7 minimal](https://lintut.com/how-to-setup-network-after-rhelcentos-7-minimal-installation/)

# Problem: Keyboard wasn't set correctly

## Fix: US keyboard layout (Macbook)

### ```$ loadkeys us```

## Links used [Change keyboard layout](https://linuxconfig.org/how-to-change-system-keyboard-keymap-layout-on-centos-7-linux)