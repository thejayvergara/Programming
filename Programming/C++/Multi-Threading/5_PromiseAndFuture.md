# PROMISE AND FUTURE
```cpp
#include <thread>
#include <future>
#include <iostream>

unsigned int yourAge = -1;

void ageInput(std::promise<yourAge>&& yourAgePromise) {
    std::cout << "Enter your age: ";
    std::cin >> yourAge;
    yourAgePromise.set_value(yourAge);
}

int main() {
    std::promise<yourAge> providingYourAge;
    std::future<yourAge> requestingYourAge = providingYourAge.get_future();

    std::thread threadObj(ageInput, std::move(providingYourAge));

    std::cout << "Your age is " << requestingYourAge.get() << "!" << std::endl;
    if (threadObj.joinable()) threadObj.join();
    return 0;
}
```