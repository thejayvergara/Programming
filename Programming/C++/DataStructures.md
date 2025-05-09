# DATA STRUCTURES (STRUCTS)
```cpp
#include <iostream>
#include <string>

struct person {
    int age = -1;
    std::string firstName;
    std::string lastName;
}

int main() {
    person p1, p2;

    p1.age = 28;
    p1.firstName = "Jay";
    p1.lastName = "Vergara";

    p2.age = 24;
    p2.firstName = "Kaitlin";
    p2.lastName = "Bondurant";

    std::cout << p1.firstName << p1.lastName << " is " << p1.age << " years old." << std::endl;
    std::cout << p2.firstName << p2.lastName << " is " << p2.age << " years old." << std::endl;
}
```