```c++
//무선 단속 카메라
#include <iostream>
#include <cstdio>
#include <algorithm>

using namespace std;

int n, k;
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		int a[100001];
		int b[100001];
		long long answer = 0;
		scanf("%d", &n);
		scanf("%d", &k);

		for (int i = 0; i < n; i++) {
			scanf("%d", &a[i]);
		}

		sort(a, a + n);

		int j = 0;
		for (int i = 0; i < n - 1; i++) {
			if (a[i] != a[i + 1]) {
				b[j] = a[i + 1] - a[i];
				j++;
			}
		}
		sort(b, b + j);
		int selection_cnt = j - (k - 1);

		if (selection_cnt <= 0) 
			selection_cnt = 0;
		
		for (int i = 0; i < selection_cnt; i++) {
			answer += b[i];
		}

		printf("#%d %lld\n", test_case, answer);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

