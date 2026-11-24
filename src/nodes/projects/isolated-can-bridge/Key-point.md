1. memcpy->进行内存拷贝(本质是宏定义)

```C
 memcpy(buffer + writeIndex, data, length)
```

参数1: 目的地址

buffer + writeIndex = &buffer[writeIndex]

参数2：原地址

data

参数3：拷贝内容的长度

length


> 使用场景： 串口软件层缓冲区设计时，缓冲区写入函数调用memcpy（），将数据写入缓冲区。
[循环缓冲区例程-memcpy使用范例](./code/loop/command.c#L80)


2. __DMB() 是 CMSIS 对 ARM DMB（Data Memory Barrier，数据内存屏障） 指令的封装。在 cmsis_gcc.h:954 中展开为：

```C

__ASM volatile ("dmb 0xF" ::: "memory");

```