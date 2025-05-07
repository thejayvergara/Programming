# MUTEX: MUTUAL EXCLUSION
Protects mutually accessed variables from threads. Used to avoid race conditions.
## lock() and unlock()
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
    if(t1.joinable){t1.join()};     // Wait for t1 to finish executing
    if(t2.joinable){t2.join()};     // Wait for t2 to finish executing
    std::cout << acctBalance << std::endl;  // Output final acctBalance
    return 0;
}
```

## mutex::try_lock()
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
    if(t1.joinable()) {t1.join();}      // Wait for t1 to finish executing
    if(t2.joinable()) {t2.join();}      // Wait for t2 to finish executing
    std::cout << "Counter increased up to:" << counter << std::endl;   // Output what the counter increased up to
    return 0;
}
```

## std::try_lock()
On success locking all mutexes, returns `-1`. If one mutex fails to lock, it returns a 0-based mutex index number of which it could not lock.
If it fails lock lock one of the mutexes, it will unlock all the other mutexes that were locked.
```cpp
```