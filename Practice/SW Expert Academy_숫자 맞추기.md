```c++
//&연산자 유추하기.
//--> 모든 답에 대해 or 연산을 수행함으로써 역으로 구할 수 있음.
#include <cstdio>

using namespace std;
int n;
int main() {

	int T;
	scanf("%d", &T);
	for (int testcase = 0; testcase < T; testcase++) {
		scanf("%d", &n);
		int answer = 0;
		for (int i = 0; i < n; i++) {
			int m, k;
			scanf("%d %d", &m, &k);
			answer = answer | k;
		}
		printf("#%d %d\n",testcase+1, answer);
	}
	
	return 0;
}
```

