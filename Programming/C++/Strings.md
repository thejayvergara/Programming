# STRINGS
Using Null-Terminated Character Sequences (NTCS).  
## character array
```cpp
#include <iostream>

char myName [] = {'J','a','y',' ','V','e','r','g','a','r','a','\0'};
std::cout << "Hi " << myName << "!" << std::endl;
```

## character array using string-literals
```cpp
#include <iostream>

char myName [] = "Jay Vergara";
std::cout << "Hi " << myName << "!" << std::endl;
```

## std::string
```cpp
#include <iostream>
#include <string>

string myName = "Jay Vergara";
std::cout << "Hi " << myName << "!" << std::endl;
```