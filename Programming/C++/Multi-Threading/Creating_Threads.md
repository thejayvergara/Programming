# CREATING THREADS
## FUNCTION POINTER THREAD CREATION
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

## LAMBDA THREAD CREATION
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

## FUNCTION OBJECT THREAD CREATION
```cpp
#include <thread>

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

## NON-STATIC FUNCTION MEMBER THREAD CREATION
```cpp
#include <thread>

class Base {
public:
    void runOnThread(unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
};

int main() {
    Base b;
    std::thread t(&Base::runOnThread, &b, 10);
    t.join();
    return 0;
}
```

## STATIC FUNCTION MEMBER THREAD CREATION
```cpp
#include <thread>

class Base {
public:
    static void runOnThread(unsigned int repeat) {
        for (unsigned int i = 0; i < repeat; ++i) {
            std::cout << "Hello World!" << std::endl;
        }
    }
};

int main() {
    Base b;
    std::thread t(&Base::runOnThread, 10);
    t.join();
    return 0;
}
```