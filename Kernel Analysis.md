## CUDA Program Analysis

#### Nvidia Visio profiler

nvprof  ./app input file   

##### simple compile process

.cu      ->      .ptx        ->      .cubin    ->exe

#### you can use "nvcc -keep" to 

#### --ptxas-option=-v to see verbose compilation output

​	number of registers used

​	shared memory bytes

​	local memory in bytes

### cuobjdump

​	a disassemble tool

​	static inst

### cuda timing functions

eg.

```
cudaEvent_t start,stop;

float elapsed ;

cudaEventCreate(&start);

cudaEventCreate(& stop);

cudaEventRecord(start,0);

fool_kernel<<<grid,block>>>();

cudaEventRecord(stop,0);

cudaEventSynchronize(stop);

cudaEventElapsedTime(&elapsed,start,stop);

printf("elapsed time %f (seconds) \n",elapsed/1000);


```



 