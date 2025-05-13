# CONDITION VARIABLES
`notify_one()` - Notifies another thread when conditions are met \
`notify_all()` - Notifies all other threads when conditions are met

```cpp
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex m;
std::condition_variable cv;
unsigned int acctBalance = 0;

void deposit(unsigned int amount) {
    std::lock_guard<mutex> lg(m);   // Prevents other threads from accessing resources until unlocked
    acctBalance += amount;      // Add amount to acctBalance
    std::cout << "New balance is " << acctBalance << std::endl;     // Output new balance
    cv.notify_one();    // notifies cv.wait() to check for conditions
}

void withdraw(unsigned int amount) {
    std::unique_lock<mutex> ul(m);
    cv.wait(    // Wait by unlocking mutex if condition is not met
        ul,     // mutex to be unlocked while waiting
        [] { return (balance!=0) ? true : false }   // condition to be met
    );
    if(acctBalance >= amount) {
        acctBalance -= amount;  // Subtract amount from acctBalance
        std::cout << "New balance is " << acctBalance << std::endl;     // Output new balance
    } else {
        std::cout << "Not enough funds!" << std::endl;  // Out not enough funds
    }
}

int main() {
    std::thread t1(withdraw, 500);  // Execute withdraw(500) on a thread
    std::thread t2(deposit, 500);   // Execute deposit(500) on a thread
    if(t1.joinable()) t1.join();    // Wait for t1 to finish
    if(t2.jonabile()) t2.join();    // Wait for t2 to finish

    return 0;
}
```