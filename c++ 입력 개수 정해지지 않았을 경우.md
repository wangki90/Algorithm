```c++
// 입력 개수 모를 때,
#include <iostream>

using namespace std;

int main() {
    int n;
    
    do {
        
        cin >> n;
        cout << n << endl;
        
    } while (getc(stdin) == ' ');
    
    cout << "end";
    
    return 0;
}
```

