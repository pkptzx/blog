---
title: 
---
---
title: "python验证码在线识别"
date: 2022-03-10T00:15:47+08:00
draft: false
weight: 70
keywords: ["python,验证码"]
description: "python验证码在线识别"
tags: ["python"]
categories: ["python"]
author: "码魂"
url: "2022/03/10/python-captcha-discriminate-online-api"
---

```python
import requests
import base64
import json
from IPython.core.display import Image

# appKey ：2e35010c-a759-11eb-8dd8-7429af540200
# appSecret：632b36755e7963fbdb61b2529e410bc4
# http://api.yunshuck.com/api/captcha/simple-captcha
# type:603 数字加字母组合验证码
# type:601 数字验证码
# type:604 数字计算验证码

headers ={}
headers['Content-Type'] = 'application/json'  
headers['appKey'] = '8961d10c-aa79-11eb-942c-7429af540200'
headers['appSecret'] = 'baec542e97c499f75c419ea935079d00'
headers['Content-Type'] = 'application/json'
rst_code = 0
while(rst_code==0):
    response = requests.get("https://app.jisilu.cn/account/captcha/2198")
    img = response.content
    imgsave = img
    display(Image(img))
    
    img = bytes.decode(base64.b64encode(img))
    urlimg = "data:image/jpeg;base64," + img
    url = 'http://101.201.223.138:9188/api/captcha/simple-captcha'
    data = "{\"urlimg\": \"" + urlimg + "\", \"num\": 6, \"type\": \"603\",\"yzmurl\": \"" + url + "\"}"
    
    r = requests.post(url=url, headers=headers,
                      data=data)
    v_code_json = json.loads(r.text)
    print(v_code_json)
    rst_code = v_code_json['code']
str1 = str(v_code_json['v_code']).lower()
print(str1)
```
