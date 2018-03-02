```c++
//완전탐색 -> 오히려 이 방식이 재귀보다 직관적인 방법, 우선 더할 경우엔..
//n이 말도 안되게 클 때는 재귀, 조합 쓰지 않기.
#include <cstdio>
#include <iostream>
#include <cstring>
#include <vector>
using namespace std;

int n;
int a[101];
int chk[10001];
int answer;
vector<int> tmp;
void init() {
	for (int i = 0; i < n; i++) {
		memset(chk, 0, sizeof(chk));
	}
	tmp.clear();
}
int main() {

	int T;
	scanf("%d", &T);
	for (int tc = 1; tc <= T; tc++) {
		scanf("%d", &n);
		init();
		int sum = 0;
		for (int i = 0; i < n; i++) {
			scanf("%d", &a[i]);
		}
        //0 먼저 체크
		chk[0] = 1;
		tmp.push_back(0);
		for (int i = 0; i < n; i++) {
			int size = tmp.size();
            //체크 배열에 있는 것들을 현재 선택 된 a[i]값과 더해줌
			for (int j = 0; j < size; j++) {
				int idx = a[i] + tmp[j];
				if (chk[idx] == 0) {
					tmp.push_back(a[i] + tmp[j]);
					chk[idx] = 1;
				}
			}
		}
		printf("#%d %d\n", tc, tmp.size());
	}
	return 0;
}
```

