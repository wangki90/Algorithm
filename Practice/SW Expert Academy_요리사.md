```c++
#include <iostream>
#include <cstdio>
#include <vector>
#include <algorithm>
#include <string>
#include <cstring>

using namespace std;

int n;
int table[16][16];
int a[8],b[8];
int half;
int answer;
void dfs(int cur, int depth) {

	if (depth == half) {
		bool chk[16];
		memset(chk, false, sizeof(chk));
		for (int i = 0; i < half; i++) {
			chk[a[i]] = true;
		}
		int tmp = 0;
		for (int i = 0; i < n; i++) {
			if (!chk[i])
				b[tmp++] = i;
		}
		int sum_a = 0, sum_b = 0;
		for (int i = 0; i < half - 1; i++) {
			for (int j = i + 1; j < half; j++) {
				sum_a += table[a[i]][a[j]] + table[a[j]][a[i]];
				sum_b += table[b[i]][b[j]] + table[b[j]][b[i]];
			}
		}
		answer = min(answer, abs(sum_a - sum_b));
		return;
	}
	for (int i = cur; i < n; i++) {
		a[depth] = i;
		dfs(i + 1, depth + 1);
	}
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		answer = 999999999;
		scanf("%d", &n);
		half = n / 2;
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &table[i][j]);
			}
		}

		dfs(0, 0);
		printf("#%d %d\n", test_case, answer);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

