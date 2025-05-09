# MUTEX: MUTUAL EXCLUSION
Protects shared resources and critical regions of your code . Used to avoid race conditions.
## std::mutex::lock() and std::mutex::unlock()
Other threads will wait for the variable to be unlocked in order to continue.
```cpp
#include <thread>
#include <mutex>

unsigned int acctBalance = 100;
std::mutex m;

// Add passed amount to acctBalance
void deposit(unsigned int amount) {
    m.lock();   // Prevent other threads from accessing variables between lock() and unlock()
    acctBalance += amount;  // Add amount to acctBalance
    m.unlock(); // Allow other threads from accessing variables between lock() and unlock()
}

int main() {
    std::thread t1(deposit, 10);    // Execute deposit(10) on a thread
    std::thread t2(deposit, 15);    // Execute deposit(15) on a thread
    if(t1.joinable) t1.join();     // Wait for t1 to finish executing
    if(t2.joinable) t2.join();     // Wait for t2 to finish executing
    std::cout << acctBalance << std::endl;  // Output final acctBalance
    return 0;
}
```

## std::mutex::try_lock()
The final counter will vary instead of getting 2000 due to try_lock() skipping (returning `false`) when it can't lock the variable.
```cpp
#include <thread>
#include <mutex>

unsigned int counter = 0;
std::mutex m;

void increaseCounter() {
    // Increase counter 1000x
    for (unsigned int i = 0; i < 1000; ++i) {
        if(m.try_lock()) {  // Prevent other threads from accessing variables between try_lock() and unlock() if not locked
            ++counter;  // Increase counter by 1
            m.unlock(); // Allow other threads from accessing variables between try_lock() and unlock()
        }
    }
}

int main() {
    std::thread t1(increaseCounter);    // Execute increaseCounter on a thread
    std::thread t2(increaseCounter);    // Execute increaseCounter on a thread
    if(t1.joinable()) t1.join();      // Wait for t1 to finish executing
    if(t2.joinable()) t2.join();      // Wait for t2 to finish executing
    std::cout << "Counter increased up to:" << counter << std::endl;   // Output what the counter increased up to
    return 0;
}
```

## std::mutex::lock_guard()
```cpp
#include <thread>
#include <mutex>

void runOnThread(unsigned int acctBalance) {
    std::lock_guard<std::mutex> lg(m);
    acctBalance += 50;
}

int main() {
    std::mutex m;
    unsigned int numOfThreads = 3;
    unsigned int acctBalance = 0;

    std::vector<std::thread> threads;
    for (unsigned int i = 0; i < numOfThreads; ++i) {
        threads.emplace_back(runOnThread, acctBalance);
    }

    for (std::vector<std::thread>& thread : threads) {
        if (thread.joinable()) thread.join();
    }
}
```

## std::mutex::unique_lock()
Mutex ownership wrapper and a more flexible version of lock_guard.

Locking Strategies (by default uses `lock()`):
1. `defer_lock` - do not acquire ownership of mutex
2. `try_to_lock` - try to acquire ownership of mutex without blocking
3. `adopt_lock` - assume the calling thread already has ownership of the mutex
### Example 1
```cpp
#include <thread>
#include <mutex>

std::mutex m;

void task(const char* threadNumber) {
    std::unique_lock<mutex> ul(m);  // locks variable and automatically unlocks with destructor
    // Displays thread number and "Hello World!" 5 times
    for(unsigned int i = 0; i < 5; ++i) {
        std::cout << threadNumber << "Hello World!" << std::endl;
    }
}

int main() {
    std::thread t1(task, "T1 ");    // Execute task() with a thread name of T1
    std::thread t2(task, "T2 ");    // Execute task() with a thread name of T2
    if (t1.joinable()) t1.join();   // Wait for t1 to finish executing
    if (t2.joinable()) t2.join();   // Wait for t2 to finish executing

    return 0;
}
```

### Example 2
```cpp
#include <thread>
#include <mutex>

std::mutex m;

void task(const char* threadNumber) {
    std::unique_lock<mutex> ul(m, defer_lock);  
    // Allows for flexibility with code here over lock_guard()
    ul.lock();
    for(unsigned int i = 0; i < 5; ++i) {
        std::cout << threadNumber << "Hello World!" << std::endl;
    }
}

int main() {
    std::thread t1(task, "T1 ");
    std::thread t2(task, "T2 ");
    if (t1.joinable()) t1.join();
    if (t2.joinable()) t2.join();

    return 0;
}
```