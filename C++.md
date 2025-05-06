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

// Protects shared data from being accessed at the same time
std::mutex variableLock;

// Function to be ran by each thread
void runOnThread() {
    std::lock_guard<std::mutex> lock(variableLock);
    unsigned int id = std::this_thread::get_id();
    std::cout << id << std::cout<< endl;
}

// Main Function
int main() {
    unsigned int numOfThreads = 3;

    std::thread threads[numOfThreads];
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
std::this_thread::sleep_for(3s);
t.detach();
t.joinable;
```

## SORTING METHODS
### Bubble Sort
```cpp
```