---
layout: article
title: Cryptopals Set 1思路
category: 网安杂记
---
## 1、Convert hex to base64
![图片](/assets/png/2024-10-1.png)  
如果直接将原始数据进行base64转换，得到的并不是答案，原因是原始数据为hex编码，一般的base64转换函数是由字符串编码转换为base64编码，因此要预处理原始数据。写一段python以实现该功能：
```python
def hex_to_string(hex_string):
    byte_data = bytes.fromhex(hex_string)
    string_data = byte_data.decode('utf-8')
    return string_data

input_string = input("原始hex数据：")
result = hex_to_string(input_string)
print(result)
```
运行结果：  
![图片](/assets/png/2024-10-2.png)   
再将得到的字符串base64编码，得到答案：
![图片](/assets/png/2024-10-3.png) 
