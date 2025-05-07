# MUTEX: MUTUAL EXCLUSION
Protects mutually accessed variables from threads. Used to avoid race conditions.
## lock() and unlock()
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

## try_lock()
This will only increase counter to roughly 1000 (it will vary) instead of 2000 even though 2 threads are increasing counter due to try_lock skipping when it can't lock the variable.
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