## Overview

- Manufacturer's website information：https://www.totolink.net/
- Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/206/ids/36.html

## Affected version

N350RT V9.3.5u.6139_B20201216

## Vulnerability details

In TOTOLINK N350RT V9.3.5u.6139_B20201216, an attacker can obtain the apmib configuration file without authorization through /cgi-bin/ExportSettings.sh. When making a request to `/cgi-bin/ExportSettings.sh`, the attacker can obtain the `apmib` configuration file Config--xxxxxxxx.dat without authorization. The username and password can be found in the decoded file.

## POC

![image-20240719214410842](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240719214410842.png)
