---
layout: article
title: Cryptopals Set 1思路
category: 网安杂记
---
## 类型转换函数归纳：
bytes.fromhex(hex_string) 输入十六进制字符串，返回一个表示转换后的字节对象
字节变量.decode("utf-8") 将字节变量以utf-8方式（或其他编码）解码为字符串
整型变量.to_bytes(length, byteorder) 将整型变量转为字节序列
int(hex_string, 16) 将十六进制字符串转十进制整数
hex(number) 将十进制整数转十六进制字符串

## 1、Convert hex to base64
![图片](/assets/png/2024-10-1.png)  
如果直接将原始数据进行base64转换，得到的并不是答案，原因是原始数据为hex编码，一般的base64转换函数是由字符串编码转换为base64编码，因此要预处理原始数据。写一段python以实现该功能：
```python
def hex_to_string(hex_string):
    #bytes.fromhex()将十六进制字符串对象转为字节对象，忽略ASCII空白符
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
 或者使用base64库中的b64encode()函数，输入一个字节对象后可返回其base64编码后的字节对象。

## 2、Fixed XOR
![图片](/assets/png/2024-10-4.png)  
用python实现对两个hex型字符串异或运算：
```python
string_1 =input()
string_2 =input()
bytes_1=bytes.fromhex(string_1)
bytes_2=bytes.fromhex(string_2)
#生成器表达式基本语法：(expression for item in iterable),返回结果为一个迭代器
result=bytes(a ^ b for a,b in zip(bytes_1,bytes_2))
print(result.hex())
```
## 3、Single-byte XOR cipher
![图片](/assets/png/2024-10-5.png)
单字节密钥长度为1 byte（8位），范围是0~255，可通过暴力枚举破解，通过统计字母频度来确认该情况的合理性
