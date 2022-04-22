+++
title = "数组传参退化(待续。。。)"
author = ["hengist"]
date = 2022-04-23T00:00:00+08:00
lastmod = 2022-04-23T02:31:09+08:00
tags = ["C/C++"]
draft = false
+++

有一个需求就是求一个数组有多少个元素,这个在C++下实现起来很简单,不过我暂时也还不知道为啥这样写能够实现,待我研究一番

```cpp
template<class T>
int length(T& data)
{
    return sizeof(data)/sizeof(data[0]);
}
```

但是在C下实现起来就有BUG,其实就是数组作为函数参数传递时会自动退化为同类型的指针

```C
int get_size(int a[])
{
    return sizeof(a)/sizeof(a[0]);
}

int a[] = {1, 2, 3, 4, 5};
int c = get_size(a); //==>8传出来是一个指针的大小(64-bit)
//可以发现这里并不是我们所期望的
```
