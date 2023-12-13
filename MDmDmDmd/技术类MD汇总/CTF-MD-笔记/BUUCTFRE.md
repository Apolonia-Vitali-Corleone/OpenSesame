## xor

这个题加深了我对xor的理解。 先输入33个数，第一个数不变，以后的数都变为它自己和上一个数异或的结果。 那么第一个数不变，现在的第二个数和第一个数异或，就得到了原来的第二个数 接着第三个数和原来的第二个数异或，就得到原来的第三个数。 就这样一直下去就好了。

 exp：

```python
s=[0x66, 0x0A, 0x6B, 0x0C, 0x77, 0x26, 0x4F, 0x2E, 0x40, 0x11,   0x78, 0x0D, 0x5A, 0x3B, 0x55, 0x11, 0x70, 0x19, 0x46, 0x1F,   0x76, 0x22, 0x4D, 0x23, 0x44, 0x0E, 0x67, 0x06, 0x68, 0x0F,   0x47, 0x32, 0x4F, 0x00] 
flag='f' 
for i in range(1,len(s)):
    flag += chr(s[i]^ s[i-1])
print(flag)
```

 shift+e可以export数据。 

## helloword

只是让你知道，有apk逆向这回事。

我们输入字符，然后进行base64加密，再然后，s[i]-i,然后等于  e3nifIH9b_C@n@dH

逆向就是，e3nifIH9b_C@n@dH  先减去 i，然后base64解密。

（但说实话，看代码真的是又累又难受，太复杂太难了。

我自己看的话，估计很难看出是base64加密）

exp：

```python
import base64

s="e3nifIH9b_C@n@dH"
flag=''
z=" "

for i in range(0,len(s)):
  flag+=chr(ord(s[i])-i)

print(base64.b64decode(flag))
```

