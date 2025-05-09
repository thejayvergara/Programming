# ARRAYS
## SINGLE DIMENSION
```cpp
#include <iostream>

int main() {
    // Initialize Array
    int numArray[5] = {1, 2, 3, 4, 5};

    // Output Array
    for (int i = 0; i < sizeof(numArray); ++i) {
        std::cout << numArray[i] << " ";
    }
    
    return 0;
}
```

## MULTIDIMENSIONAL
```cpp
#include <iostream>

int main() {
    // Initialize 2D Array
    int num2DArray[2][3] = {
        {11, 12, 13},
        {21, 22, 23}
    }

    // Output 2D Array
    for (int i = 0; i < 2; ++i) {
        for (int j = 0; j < 3; ++j) {
            std::cout << num2DArray[i][j] << " ";
        }
        std::cout << std::endl;
    }

    // Initialize 3D Array
    int num3DArray[3][3][3] = {
        {},
        {},
        {}
    }

    // Output 3D Array
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            for (int k = 0; k < 3; ++k>) {
                std::cout << num3DArray[i][j][k] << " ";;
            }
            std::cout << std::endl;
        }
        std::cout << std::endl;
    }


    return 0;
}
```