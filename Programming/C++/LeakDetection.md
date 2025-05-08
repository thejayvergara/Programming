# LEAK DETECTION
Used for memory leak detection when in debug mode.
```cpp
#if defined _MSC_VER && defined _DEBUG
	#include <crtdbg.h>
#include <functional>
	#define new new(_NORMAL_BLOCK, __FILE__, __LINE__)
	#define ENABLE_LEAK_DETECTION() _CrtSetDbgFlag(_CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF)
#else
	#define ENABLE_LEAK_DETECTION()
#endif

int main() {
    ENABLE_LEAK_DETECTION()
    return 0;
}
```