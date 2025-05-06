# C++ Cheatsheat



## CLASSES




## VECTORS
```
std::vector<unsigned int> vectNumbers;
```





## MULTI-THREADING
### General Example
```cpp
#include <threads>
#include <mutex>

// Function to be ran by each thread
void FunctionOnThread(int repeatCount) {
    for (int i = 0; i < repeatCount; i++)
    std::cout << "Hello World!" << std::endl;
}

// Main Function
int main() {
    std::thread t(FunctionOnThread, 3)
}

// Wait for all threads to complete execution before moving on
for () {
    t.join();
}
```

### Other methods
```
t.detach();
t.joinable;
```