# BINARY SEMAPHORE
Used to control shared resources through signaling.
```cpp
#include <semaphore>

// Initialize semaphore signals
std::binary_sempahore signalObj{0};

void runOnThread() {
    signalObj.acquire();   // Send signal that you have locked control over shared resources
    signalObj.relase();    // Send signal that you have allowed control over shared resources
}

int main() {
    std::thread threadObj(runOnThread);     // Execute runOnThread on a thread
    signalObj.release();   // Send signal that you have allowed control over shared resources
    signalObj.acquire();   // Send signal that you have locked control over shared resources
    if (threadObj.joinable()) threadObj.join();     // Wait for threadObj to finish executing
    return 0;
}
```