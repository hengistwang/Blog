+++
title = "name conflict multiple dynamic library"
author = ["hengist"]
date = 2023-07-06T00:00:00+08:00
lastmod = 2023-07-17T23:42:24+08:00
tags = ["Link"]
draft = false
+++

## Here is the Question {#here-is-the-question}

```c
/*A.c*/
#include <stdio.h>
int sayHi() {
  printf("Hi, this is AAAAA\n");
  return 0;
}
int sayOut() {
  sayHi();
  printf("Use this to introduce AAAAA\n");
  return 0;
}

```

```c
/*B.c*/
#include <stdio.h>
int sayHi() {
  printf("Hi, this is BBBBB\n");
  return 0;
}
int sayOut() {
  sayHi();
  printf("Use this to introduce BBBBB\n");
  return 0;
}

```

```c
#include <stdio.h>
extern int sayOut();

int main() {
  sayOut();
  return 0;
}

```

```bash
# if link A first
>gcc test.c -L. -lA -lB
>./a.out
Hi, this is AAAAA
Use this to introduce AAAAA
# if link B first
>gcc test.c -L. -lB -lA
>./a.out
Hi, this is BBBBB
Use this to introduce BBBBB
```


## First solution {#first-solution}

at first i use dlopen to explicitly load a dynamic library

```c
#include <stdio.h>
#include<dlfcn.h>
extern int sayOut();

typedef int (*func_pt)();


int main() {
    void *handle = NULL;
    func_pt func = NULL;
    if((handle = dlopen("./libA.so",RTLD_LAZY))== NULL)
    {
        printf("dlopen %s\n", dlerror());
        return -1;
    }
    func = dlsym(handle, "sayOut");
    func();
    dlclose(handle);

    if((handle = dlopen("./libB.so",RTLD_LAZY))== NULL)
    {
        printf("dlopen %s\n", dlerror());
        return -1;
    }
    func = dlsym(handle, "sayOut");
    func();
    dlclose(handle);
  return 0;
}

```

```bash
❯gcc test.c -L. -lA -lB
❯ ./a.out
Hi, this is AAAAA
Use this to introduce AAAAA
Hi, this is AAAAA
Use this to introduce BBBBB

❯ gcc test.c -L. -lB -lA
❯ ./a.out
Hi, this is BBBBB
Use this to introduce AAAAA
Hi, this is BBBBB
Use this to introduce BBBBB
```

we can see the outer func sayOut is load explicitly, however the inner function still related to linking order
it is because the inner function are exposed to the outside


## Second solution {#second-solution}

i use <span class="underline"><span class="underline">attrubute</span></span> to control if a function should expose to the outside
here is an example

```c
/*A.c*/
#include <stdio.h>
#define DLL_PUBLIC __attribute__((visibility("default")))
#define DLL_LOCAL __attribute__((visibility("hidden")))

DLL_LOCAL int sayHi() {
  printf("Hi, this is AAAAA\n");
  return 0;
}
DLL_PUBLIC int sayOut() {
  sayHi();
  printf("Use this to introduce AAAAA\n");
  return 0;
}

/*B.c*/
#include <stdio.h>

#define DLL_PUBLIC __attribute__((visibility("default")))
#define DLL_LOCAL __attribute__((visibility("hidden")))

DLL_LOCAL int sayHi() {
  printf("Hi, this is BBBBB\n");
  return 0;
}
DLL_PUBLIC int sayOut() {
  sayHi();
  printf("Use this to introduce BBBBB\n");
  return 0;
}

```

```bash
❯ gcc test.c -L. -lA -lB
❯ ./a.out
Hi, this is AAAAA
Use this to introduce AAAAA
Hi, this is BBBBB
Use this to introduce BBBBB

❯ gcc test.c -L. -lB -lA
❯ ./a.out
Hi, this is AAAAA
Use this to introduce AAAAA
Hi, this is BBBBB
Use this to introduce BBBBB
```


## Third solution {#third-solution}

The third way is only set outer function to visible
and compile it with -fvisibility=hidden argument

```c
/*A.c*/
#include <stdio.h>
#define DLL_PUBLIC __attribute__((visibility("default")))

int sayHi() {
  printf("Hi, this is AAAAA\n");
  return 0;
}
DLL_PUBLIC int sayOut() {
  sayHi();
  printf("Use this to introduce AAAAA\n");
  return 0;
}

/*B.c*/
#include <stdio.h>

#define DLL_PUBLIC __attribute__((visibility("default")))

int sayHi() {
  printf("Hi, this is BBBBB\n");
  return 0;
}
DLL_PUBLIC int sayOut() {
  sayHi();
  printf("Use this to introduce BBBBB\n");
  return 0;
}
```

```bash
and it worked as expected
❯ gcc test.c -L. -lA -lB
❯ ./a.out
Hi, this is AAAAA
Use this to introduce AAAAA
Hi, this is BBBBB
Use this to introduce BBBBB

❯ gcc test.c -L. -lB -lA
❯ ./a.out
Hi, this is AAAAA
Use this to introduce AAAAA
Hi, this is BBBBB
Use this to introduce BBBBB
```
