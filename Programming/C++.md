# C++ CHEATSHEET

## CLASSES
### General Example
```cpp
```



## VECTORS
### General Example
```cpp
#include <vector>

// Vector initializations
std::vector<unsigned int> uintVect;
std::vector<std::thread> threadVect;
std::vector<std::vector<unsigned int>> uintVectVect;
```



## MULTI-THREADING
### General Example
```cpp
#include <thread>
#include <mutex>
#include <condition_variable>

// Protects shared data from being accessed at the same time
std::mutex m;

// Function to be ran by each thread
void runOnThread() {
    std::lock_guard<std::mutex> lock(m);
    unsigned int id = std::this_thread::get_id();
    std::cout << id << std::cout<< endl;
}

// Main Function
int main() {
    unsigned int numOfThreads = 3;

    std::thread* threads = new std::thread[numOfThreads];

    for (unsigned int i = 0; i < numOfThreads; i++) {
        threads[i] = std::thread(runOnThread);
    }

    // Wait for all threads to complete execution before moving on
    for (unsigned int i = 0; i < numOfThreads; i++) {
        threads[i].join();
    }

    return 0;
}
```

### Other Methods
```cpp
#include chrono
std::this_thread::sleep_for(std::chrono::milliseconds(10));

t.detach();
t.joinable();
```


### Function Pointer Thread Creation
```cpp
#include <thread>

void runOnThread(int repeat) {
    for (unsigned int i = 0; i < repeat; ++i) {
        std::cout << "Hello World!" << std::endl;
    }
}

int main() {
    std::thread t(runOnThread, 5);
    t.join();
    return 0;
}
```