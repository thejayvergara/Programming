# C++ Cheatsheat



## CLASSES




## VECTORS
```
std::vector<unsigned int> vectNumbers;
```





## MULTI-THREADING
### General Example
```
#include <threads>
#include <mutex>

void FunctionOnThread(int repeatCount) {
    for (int i = 0; i < repeatCount; i++)
    std::cout << "Hello World!" << std::endl;
}

int main() {
    std::thread t(FunctionOnThread, 3)
}

for () {
    t.join();
}
```

### Other methods
```
t.detach();
t.joinable;
```