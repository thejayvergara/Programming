# Creating Threads
## Function Pointer Thread Creation
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

## Lambda Thread Creation
### Example 1
```cpp
#include <thread>

int main() {
    auto runOnThread = [](unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
    std::thread t(runOnThread, 5);
    t.join();
    return 0;
}
```

### Example 2
```cpp
#include <thread>

int main() {
    std::thread t([](unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }, 5);
    t.join();
    return 0;
}
```

## Function Object Thread Creation
```cpp
class Base {
public:
    void operator()(unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
};

int main() {
    std::thread t((Base()), 10);
    t.join();
    return 0;
}
```