```c++
//완탐으로 풀려다가 n이 너무 커서 직관으로 푼 문제.
//인풋 받아서 -> 정렬 -> 홀수번째, 짝수번째 끼리 배열에 따로 저장 
//홀수 배열을 먼저 배열에 넣고 -> 그 뒤에 짝수 배열을 넣는다 -> 인접한 인덱스 높이 비교
#include <cstdio>
#include <algorithm>
using namespace std;

int n;
int a[10001];
int b[10001];
int c[10001];
int main() {
	int t;
	scanf("%d", &t);

	for (int tc = 1; tc <= t; tc++) {
		scanf("%d", &n);
		int cnt = 0, cnt2 = 0;
		for (int i = 0; i < n; i++) {
			scanf("%d", &c[i]);
		}
		sort(c, c + n);
		for (int i = 0; i < n; i++) {
			if (i % 2 == 0) {
				a[cnt] = c[i];
				cnt++;
			}
			else {
				b[cnt2] = c[i];
				cnt2++;
			}
		}
		for (int i = 0; i < cnt; i++)
			c[i] = a[i];
		for (int i = 0; i < cnt2; i++) {
			c[cnt + i] = b[cnt2 - i - 1];
		}
		int max_h = -1;
		for (int i = 1; i < n; i++)
			max_h = max(max_h, abs(c[i] - c[i - 1]));
		
		max_h = max(max_h, abs(c[n - 1] - c[0]));

		printf("#%d %d\n",tc, max_h);
	}


	return 0;
}
```

