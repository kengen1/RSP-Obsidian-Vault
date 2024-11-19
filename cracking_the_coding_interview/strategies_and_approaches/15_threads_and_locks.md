# Threads and Locks

### Basic Thread Use
- threads can be created throuhg the use of `std::thread` class

```cpp
#include <iostream>
#include <thread>

void printMessage() {
    std::cout << "Hello from thread!" << std::endl;
}

int main() {
    std::thread t(printMessage);  // Create a thread running `printMessage`
    t.join();  // Wait for the thread to finish
    return 0;
}
```

- Important Methods:
    - `.join()`: Blocks until the thread finishes execution
    - `.detach()`: Makes the thread run independently (not recommended unless necessary)

### Common Problems with Threads
- **Race Conditions**: Occur when two or more threads modify shared memory simultaneously without synchronization
- **Deadlocks**: Occur when two or more threads wait indefinitely for resources held by each other


### Synchronization Mechanisms

#### Mutex (Mutual Exclusions)
Used to protect shared resources from simultaneous access by multiple threads

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void printSafe(const std::string& msg) {
    mtx.lock();  // Lock the mutex
    std::cout << msg << std::endl;
    mtx.unlock();  // Unlock the mutex
}

int main() {
    std::thread t1(printSafe, "Thread 1");
    std::thread t2(printSafe, "Thread 2");

    t1.join();
    t2.join();
    return 0;
}

```

- `std::lock_guard` ensures the mutex is released even if an exception occurs

```cpp
void printSafe(const std::string& msg) {
    std::lock_guard<std::mutex> lock(mtx);  // Locks and unlocks automatically
    std::cout << msg << std::endl;
}
```

---

#### Condition Variables
Allows threads to wait for specific conditions to be met

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void workerThread() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, [] { return ready; });  // Wait until `ready` becomes true
    std::cout << "Worker thread is running!" << std::endl;
}

int main() {
    std::thread worker(workerThread);

    {
        std::lock_guard<std::mutex> lock(mtx);
        ready = true;
    }
    cv.notify_one();  // Notify the worker thread

    worker.join();
    return 0;
}
```
### Deadlock Prevention

- A deadlock is where a thread is waiting for an object lock that another thread holds
- This second thread is waiting for an object that the first thread holds (this problem can scale with several threads)
- Since each thread is waiting for the other thread to reliquish a lock, they both remain waiting forever (deadlocked)

- In order for a deadlock to occur, there are 4 conditions that must be met:
1. Mutual Exclusion: Only one process can access a resource at a given time
2. Hold and Wait: : Processes already holding a resource can request additional resources, without relinquishing their current resources.
3. No Preemption: One process cannot forcibly remove another process' resource.
4. Circular Wait: Two or more processes form a circular chain where each process is waiting on another
resource in the chain.

- Deadlock prevention involves removing any of the above conditions

---

- Consistent Lock Ordering: Always lock resources in the same order across threads
- Try Locks: Use `std::try_lock` to avoid blocking indefinetly 

```cpp
if (mtx.try_lock()) {
    // Do work
    mtx.unlock();
} else {
    // Handle lock failure
}
```

- Scope Locks: `std::scoped_lock` for multiple mutexes
```cpp
std::scoped_lock lock(mtx1, mtx2);  // Prevents deadlocks by locking in one call
```