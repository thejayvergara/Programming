# STARTING GUN LOGIC
Starting gun logic sample for one of my assignments.
```cpp
#include <thread>
#include <mutex>
#include <condition_variable>
#include <vector>
#include <stdio.h>

struct ThreadProps {
    int id = 0;
    struct ThreadPool* pThreadPool = nullptr;
};

struct ThreadPool {
    ThreadProps* pThreadProps = nullptr;

    int* pNumOfThreads = nullptr;
    int readyThreadCount = 0;
    bool threadsReady = false;

    std::mutex threadCountMutex;
    std::condition_variable threadCountVar;

    std::mutex threadGunMutex;
    std::condition_variable threadGunVar;
};

void runOnThread(ThreadProps* pThreadProps) {
    printf("Thread %d waiting on starting gun\n", pThreadProps->id);

    // Let main know there's one more thread running
    std::unique_lock<std::mutex> lockThreadGun(pThreadProps->pThreadPool->threadGunMutex);
    {
        std::lock_guard<std::mutex> lockThreadCount(pThreadProps->pThreadPool->threadCountMutex);
        pThreadProps->pThreadPool->readyThreadCount++;
        pThreadProps->pThreadPool->threadCountVar.notify_all();
    }
    printf("Thread %d ready\n", pThreadProps->id);

    // Wait until all threads are ready
    pThreadProps->pThreadPool->threadGunVar.wait(lockThreadGun, [&pThreadProps] {
        return pThreadProps->pThreadPool->threadsReady;
    });
    lockThreadGun.unlock();

    printf("Thread %d running\n", pThreadProps->id);

    // Let main know there's one less thread running
    {
        std::lock_guard<std::mutex> lockThreadCount(pThreadProps->pThreadPool->threadCountMutex);
        pThreadProps->pThreadPool->readyThreadCount--;
        pThreadProps->pThreadPool->threadCountVar.notify_all();
    }
}

int main() {
    int numOfThreads = 3;

    ThreadProps* pPerThreadProps;
    ThreadPool poolOfThreads;

    printf("Starting %d threads\n", numOfThreads);

    // Allocated an array for thread properties
    pPerThreadProps = new ThreadProps[numOfThreads];

    // Initialize thread properties
    poolOfThreads.pThreadProps = pPerThreadProps;
    poolOfThreads.pNumOfThreads = &numOfThreads;

    // Initialize id for each thread
    for (int i = 0; i < numOfThreads; ++i) {
        pPerThreadProps[i].id = i;
        pPerThreadProps[i].pThreadPool = &poolOfThreads;
    }

    // Start threads 
    std::unique_lock<std::mutex> lockThreadCount(poolOfThreads.threadCountMutex);
    for (int i = 0; i < numOfThreads; ++i) {
        std::thread(runOnThread, &pPerThreadProps[i]).detach();
    }

    // Wait for all threads to be ready
    poolOfThreads.threadCountVar.wait(lockThreadCount, [&poolOfThreads, numOfThreads] {
        return poolOfThreads.readyThreadCount == numOfThreads;
    });
    poolOfThreads.threadCountVar.notify_all();
    lockThreadCount.unlock();

    // Notify all waithing threads that they can start
    {
        std::lock_guard<std::mutex> lockGun(poolOfThreads.threadGunMutex);
        poolOfThreads.threadsReady = true;
        poolOfThreads.threadGunVar.notify_all();
    }

    // Wait for all detached threads to complete
    lockThreadCount.lock();
    poolOfThreads.threadCountVar.wait(lockThreadCount, [&poolOfThreads] {
        return poolOfThreads.readyThreadCount == 0;
    });

    printf("All threads finished\n");

    delete[] pPerThreadProps;

    return 0;
}
```