```c++
#include <iostream>
#include <cstdio>
#include <vector>
#include <algorithm>
using namespace std;

int n;
int a, b, c, d; //+,-,*,/
vector<int> num;
int max_value, min_value;
int answer;

void init() {
	max_value = -100000001;
	min_value = 100000001;
	num.clear();
}
void dfs(int depth, int _a, int _b, int _c, int _d,int ret) {

	if (depth == n - 1) {

		min_value = min(min_value, ret);
		max_value = max(max_value, ret);

		return;
	}

	if (_a > 0) {
		dfs(depth + 1, _a - 1, _b, _c, _d, ret + num[depth + 1]);
	}
	if (_b > 0) {
		dfs(depth + 1, _a, _b - 1, _c, _d, ret - num[depth + 1]);
	}
	if (_c > 0) {
		dfs(depth + 1, _a, _b, _c - 1, _d, ret * num[depth + 1]);
	}
	if (_d > 0) {
		dfs(depth + 1, _a, _b, _c, _d - 1, ret / num[depth + 1]);
	}
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		scanf("%d", &n);
		init();
		scanf("%d %d %d %d", &a, &b, &c, &d);
		for (int i = 0; i < n; i++) {
			int x;
			scanf("%d",&x);
			num.push_back(x);
		}
		dfs(0, a, b, c, d, num[0]);
		answer = max_value - min_value;
		printf("#%d %d\n",test_case, answer);

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

