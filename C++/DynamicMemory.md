# DYNAMIC MEMORY
```cpp
#include <random>

// Generate a random number
int genRandInt() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> distrib(1,100);
    int randInt = distrib(gen);
    return randInt;
}

int main() {
    int numOfNumbers = 5;

    // Dynamically allocate memory for 5 numbers
    int* numbers = new numbers[numOfNumbers];

    // Add random numbers
    for (unsigned int i = 0; i < numOfNumbers; ++i) {
        numbers[i] = genRandInt();
    }

    // Free up allocated memory to prevent memory leak
    delete[] numbers;
    return 0;
}
```