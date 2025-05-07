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
    m.lock();   // Prevent other threads from accessing acctBalance (or any other variables in between lock() and unlock())
    acctBalance += amount;  // Add amount to acctBalance
    m.unlock(); // Allow other threads from accessing acctBalance (or any other variables in between lock() and unlock())
}

int main() {
    std::thread t1(deposit, 10);    // Execute deposit(10)
    std::thread t2(deposit, 15);    // Execute deposit(15)
    if(t1.joinable){t1.join()};     // Wait for t1 to finish executing
    if(t2.joinable){t2.join()};     // Wait for t2 to finish executing
    std::cout << acctBalance << std::endl;  // Output final acctBalance
    return 0;
}
```

## try_lock()