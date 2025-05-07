# CREATING THREADS
## FUNCTION POINTER THREAD CREATION
```cpp
#include <thread>

// Displays "Hello World!" multiple times based on the passed argument
void runOnThread(int repeat) {
    for (unsigned int i = 0; i < repeat; ++i) {
        std::cout << "Hello World!" << std::endl;
    }
}

int main() {
    std::thread t(runOnThread, 5);  // Execute runOnThread(5) on a thread
    if (t.joinable()) {t.join();}   // Wait for thread to finish executing
    return 0;
}
```

## LAMBDA THREAD CREATION
### Example 1
```cpp
#include <thread>

int main() {
    // Displays "Hello World!" multiple times based on the passed argument
    auto runOnThread = [](unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
    std::thread t(runOnThread, 5);  // Execute runOnThread(5) on a thread
    if (t.joinable()) {t.join();}   // Wait for thread to finish executing
    return 0;
}
```

### Example 2
```cpp
#include <thread>

int main() {
    // Displays "Hello World!" 5 times directly on thread
    std::thread t([](unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }, 5);
    if (t.joinable()) {t.join();}   // Wait for thread to finish executing
    return 0;
}
```

## FUNCTION OBJECT THREAD CREATION
```cpp
#include <thread>

class Base {
public:
    // Displays "Hello World!" multiple times based on the passed argument
    void operator()(unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
};

int main() {
    std::thread t((Base()), 10);    // Execute Base Class function overload on a thread
    if (t.joinable()) {t.join();}   // Wait for thread to finish executing
    return 0;
}
```

## NON-STATIC FUNCTION MEMBER THREAD CREATION
```cpp
#include <thread>

class Base {
public:
    // Displays "Hello World!" multiple times based on the passed argument
    void runOnThread(unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
};

int main() {
    Base b; // Create an instance of Base Class
    std::thread t(&Base::runOnThread, &b, 5);  // Execute Base Class' runOnThread(5) non-static function
    if (t.joinable()) {t.join();}   // Wait for thread to finish executing
    return 0;
}
```

## STATIC FUNCTION MEMBER THREAD CREATION
```cpp
#include <thread>

class Base {
public:
    // Displays "Hello World!" multiple times based on the passed argument
    static void runOnThread(unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
};

int main() {
    Base b; // Create an instance of Base Class
    std::thread t(&Base::runOnThread, 10);  // Execute Base Class' runOnThread(5) static function
    if (t.joinable()) {t.join();}   // Wait for thread to finish executing
    return 0;
}
```