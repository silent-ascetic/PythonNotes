# 位运算

**位运算是根据变量在内存中存储的二进制位进行运算，而不是其二进制数形式**

**-9的二进制数：-1001**

**-9在内存中的存储形式：11110111**


## 1. 按位与（&）

**参与运算的两个二进制位都为一，结果为一，其余情况都为零。**

**即：1&1 == 1    1&0 == 0   0&0 == 0**

**例：**

-9&9 == 1

**解析：**

11110111 &

00001001 ==

00000001

## 2. 按位或（|）

**参与运算的两个二进制位都为零，结果为零，其余情况都为一**

## 3. 按位异或（^）

**参与运算的两个二进制位不同时结果为一，相同时为零**

**即：1^1 == 0  1^0 == 1  0^0 == 0**

## 4. 取反（~）

**单目运算符，对参与运算的二进制位取反**

**即：~1 == 0   ~0 == 1**

**例：**

~(-9) == 8

**解析：**
```
~  111101111 

== 00001000
```
## 5. 左移（<<）

**将操作数在内存中存储的个二进制位都左移若干位，高位丢弃，低位补零**

**例：**

9<<3 == 72

**解析：**

00001001 << 3 == 

01001000

## 6. 右移（>>）

**将操作数在内存中存储的二进制位都右移若干，低位丢弃，操作数为负数时，高位补一，其余补零**
