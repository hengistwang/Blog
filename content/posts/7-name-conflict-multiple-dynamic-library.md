+++
title = "name conflict multiple dynamic library"
author = ["hengist"]
date = 2023-07-06T00:00:00+08:00
lastmod = 2023-07-06T00:51:45+08:00
tags = ["cpp"]
draft = false
+++

```cpp
/*func_A.c*/
#include <stdio.h>
int sayHi() {
  printf("Hi,this is AAAAA\n");
  return 0;
}
int sayOut() {
  sayHi();
  printf("Use this to introduce AAAAA\n");
  return 0;
}

```

```cpp
/*func_B.c*/
#include <stdio.h>
int sayHi() {
  printf("Hi,this is BBBBB\n");
  return 0;
}
int sayOut() {
  sayHi();
  printf("Use this to introduce BBBBB\n");
  return 0;
}

```

```cpp

```

```cpp

```

```cpp

```

```cpp

```

```cpp

```

```cpp

```
