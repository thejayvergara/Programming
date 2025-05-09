# VECTORS
## Member Functions
**ITERATORS:**
`begin()` -- Return iterator to the first element in the vector  
`end()`  -- Return iterator to the last element in the vector  
`rbegin()` -- Return iterator to the last element in the vector and iterate towards the first element  

**CAPACITY:**  
`capacity()` -- Allocated size for the vector  
`size()` -- Number of elements currently stored in the vector  
`empty()` -- Returns a boolean of whether the vector is empty or not  
`shrink_to_fit()` -- Shrink the capacity to the size of the vector  

**ELEMENT ACCESS::**  
`at()` -- Access element at a specific position  
`front()` -- Access the first element in the vector  
`back()` -- Access the last element in the vector

**MODIFIERS:**  
`assign()` -- Assigns a value to an element in the vector  
`push_back()` -- Add element to the end of the vector  
`insert()` -- Add element to a specific position in the vector  
`emplace_back()` -- Construct and add element to the end of the vector  
`emplace()` -- Construct and add element to a specific position in the vector    
`pop_back()` -- Remove last element in the vector  
`clear()` -- Remove all elements in the vector  

***WARNING:*** *These member functions are ones I commonly use and allows me to do bulk of my work.
For a full detailed information on vectors, see [THIS LINK](https://cplusplus.com/reference/vector/vector)*

## Example
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers;

    std::cout << "Adding 5 integers into the vector..." << std::endl;
    for (unsigned int i = 0; i < 5; ++i) {
        numbers.push_back(i);
    }

    std::cout << "This vector contains the following integers:" << std::endl;
    for (unsigned int& number : numbers) {
        std::cout << number << std::endl;
    }

    std::cout << std::endl;

    std::cout << "The capacity of this vector is " << numbers.capacity() << std::endl;
    std::cout << "The size of this vector is " << numbers.size() << std::endl;

    std::cout << std::endl;

    std::cout << "Removing integers from the vector..." << std::endl;
    for (unsigned int i = 0; i < numbers.size(); ++i) {
        numbers.pop_back(i);
    }

    std::cout << std::endl;

    std::cout << "The new capacity of this vector is " << numbers.capacity() << std::endl;
    std::cout << "The new size of this vector is " << numbers.size() << std::endl;

    std::cout << std::endl;
}
```

## WAYS TO LOOP THROUGH VECTORS
### RANGE-BASED FOR LOOP
Simplest way to loop through vectors with less flexibility.
```cpp
for (std::vector<int>& number : numbers) {
    std::cout << number << std::endl;
}

// OR YOU CAN USE AUTO

for (auto& number : numbers) {
    std::cout << number << std::endl;
}
```

### ITERATOR LOOP
Loop through vector using iterators.
```cpp
for (std::vector<int>::iterator it = numbers.begin(); it != numbers.end(); ++it) {
    std::cout << *it << std::endl;
}

// OR YOU CAN USE AUTO

for (auto it = numbers.begin(); it != numbers.end(); ++it) {
    std::cout << *it << std::endl;
}
```

### FOR LOOP
Old and traditional style of looping through vectors.
```cpp
for (unsigned int i = 0; i < numbers.size(); ++i) {
    std::cout << "Position " << i << " contains " << numbers[i] << std::endl;
}
```