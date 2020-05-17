Concurrency and Race conditions:
- It happens when system tries to do more then one thing at once
- Due to multiprocessing processor chances of concurrent access has increased.
- Race condition means uncontrolled access to data which is shared
- It could cause memory leak, as data is overwritten and original data is lost
Semaphores and mutex
- Process requests for resources/memory and check if semaphore value is greater than 0.
- It the value os greater than zero, it decrements the value and continues process (locking. It until process is using this).
- It the value is less than or 0, it means some other process is using resource so it waits
Difference between semaphore and mutex
- Both are used to lock down the resource while a process is sign it 
- Mutex can only be 0 or 1 whereas semaphore can have other values as well
Other resources available:
- Completions: Allows one thread to tell another thread that task is done
- Spinlocks: Just like semaphores but they are used for code which. Can not sleep for example interrupt handlers
