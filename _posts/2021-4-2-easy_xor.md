---
title: easy_xor
date: 2021-4-2
description: xor的简单操作，就是为了记录一下该怎么操作的
category: 信息安全
tags:
  - CTF
  - Crypto
---
# 入门的xor
  题目给出了密文和密钥，密文是`AQ0eFhsHBCM2IysqHSA8MHl+Oz0gHS82HRghJyYu`，key是`BXSBXSBXSBXSBXSBXSBXSBXSBXSBXS`  
  
  讲道理，密文里这么大的`+`，这么明显的特征，base64又没认出来  
  
  ```python
from libnum import s2n
from base64 import *
key='BXSBXSBXSBXSBXSBXSBXSBXSBXSBXS'
cipertext=b"AQ0eFhsHBCM2IysqHSA8MHl+Oz0gHS82HRghJyYu"
plaintext=bytes.fromhex(hex(int.from_bytes(b64decode(cipertext),byteorder='big')^s2n(key))[2:])
print(plaintext)
  ```
  其中，`b64decode`解码base64为bytes，`int.from_bytes`把bytes类型转化为十进制整数，然后把结果直接和`s2n(key)`的结果`^`，`s2n`是把字符串转化为十进制整数  
  
  再然后转化为十六进制再转为bytes类型，`[2:]`截掉前面表示十六进制的`0x`  
  
  本来感觉这种方法好蠢，直接用`int.to_bytes`多好，非要从十六进制绕一圈干嘛，后来发现这种方法没那么好用  
  
  `int.to_bytes`格式为`int.to_bytes(num,length=40,byteorder='big',signed=False)`，大端序就是正常的顺序，无符号数  
  
  所以本题中解密语句即为
  ```python
plaintext=int.to_bytes(int.from_bytes(b64decode(cipertext),byteorder='big')^s2n(key),length=40,byteorder='big',signed=False)
  ```
  其中`length`属性是未知的，数字设小了会报错，设大的话前面会用`\x00`填充
    
  
  
  
  