```c++
// vector 아이템 find
// <algorithm> std::find
// std::find(vector.begin(), vector.end(), item) != vector.end() )
// return : 존재 -> true, 존재 X -> false


#include <algorithm>

if ( std::find(vector.begin(), vector.end(), item) != vector.end() )
   do_this();
else
   do that();

// iteration 활용
v.push_back(20);
vector<int>::iterator iter;
iter = find(v.begin(), v.end(), 20);
cout << *iter << endl;
// print 20

iter = find(v.begin(), v.end(), 100);
// item 찾지 못했을 경우, iter == v.end()
```

