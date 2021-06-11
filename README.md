# thread-safe-counter

#### - Class of Professor JongChan Kim.

#### - Project : Thread-Safety by Semaphore

#### - OS version : Ubuntu Linux 18.04 

- file [tscounter.c] is original file by mutex method, file [semaphore_tscounter.c] is fixed file by semaphore method.
- using time command    *ex> time ./a.out 10000*
--------------------------------------------------------

## Compare Performance

### by Mutex
<img src="https://user-images.githubusercontent.com/68265609/121745519-5dae1500-cb3f-11eb-87d9-6f3ede92f05e.png" width="700" height="420">

### by Semaphore
<img src="https://user-images.githubusercontent.com/68265609/121745533-63a3f600-cb3f-11eb-8864-3aa3fc98d54b.png" width="700" height="420">

#### -The table below shows the time taken according to the given count. The time is in order [real / user / sys].
|**Method**|**count : 10000**|**count : 100000**|**count : 100000**|
|:------:|:------:|:------:|:------:|
|**MUTEX**|[0.004 / 0.006 / 0.000]|[0.029 / 0.025 / 0.029]|[0.186 / 0.204 / 0.164]|
|**SEMAPHORE**|[0.061 / 0.006 / 0.080]|[0.443 / 0.059 / 0.571]|[4.715 / 0.468 / 6.237]|
