---
title: Serialize
date: 2021-1-24 
description: 序列化和反序列化，终于还是下手了
category: 信息安全
tags:
  - CTF
  - Web
  - Serialize
---
# serialize and unserialize
举个栗子 `O:4:"xctf",1,{s:4:"flag";s:3:"111"}`(攻防世界unserialize3的payload)  
原本是长这个样子的
```php

```
`O:4`中O代表对象（Object），4表示名字长度为4  
`"xctf"`为类名  
`1`表示有1个属性  
`s`代表字符串  
`4`表示字符串的长度  
`flag`是属性名  
`111`是属性值
