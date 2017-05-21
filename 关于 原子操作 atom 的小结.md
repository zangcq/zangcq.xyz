### 关于 原子操作 atom 的小结

**atom**

Atomic reduction operations for thread-to-thread communication.

语法

```c
atom{.space}{.scope}.op.type d, [a], b; 

atom{.space}{.scope}.op.type d, [a], b, c; 

.space = { .global, .shared }; 

.scope = { .cta, .gpu, .sys }; 

.op = { .and, .or, .xor, // .b32, .b64
		.cas, .exch, // .b32, .b64
        .add, // .u32, .s32, .f32, .u64, .f64 
        .inc, .dec, // .u32 only 
        .min, .max }; // .u32, .s32, .u64, .s64 
        
.type = { .b32, .b64, .u32, .u64, .s32, .s64, .f32, .f64 };


```

描述

​	实际上，一次atom操作，即 read---motified---write 三步操作



eg  

```c
 atom.global.inc.s32  d,[a],n;
```

​	1.从 a 的地址里读到 d 中，                      read/load

​	2.根据inc的定义                                         motified

​		计算 ((d >= n) ? 0 : (d+1))；

​	3.然后把 算出的值 再写回 a 的地址里。write/store

​	inc其含义，就是当 a 增长到 n 时，置a = 0；	

[atomiclnc（）]: http://stackoverflow.com/questions/18008975/atomicinc-is-not-working

https://docs.nvidia.com/cuda/cuda-c-programming-guide/#arithmetic-functions
