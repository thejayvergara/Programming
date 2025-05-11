# MUTEXES (MUTUAL EXCLUSIONS)
## STEP 1: INCLUDE HEADER
```cpp
#include <mutex>
```

## STEP 2: DECLARE MUTEX
```cpp
std::mutex mutex;
```

## STEP 3: LOCK AND UNLOCK MUTEX
### LOCK() AND UNLOCK() METHOD
```cpp
mutex.lock();
// TODO: Add critical region of code here
mutex.unlock();
```

### LOCK_GUARD METHOD
Automatically unlocks when you go out-of-scope. \
```cpp
std::lock_guard<std::mutex> lock(mutex);
// TODO: Add critical region of code here
```

### UNIQUE_LOCK METHOD
Automatically unlocks when you go out-of-scope. \
```cpp
std::unique_lock<std::mutex> lock(mutex);
// TODO: Add critical region of code here
```