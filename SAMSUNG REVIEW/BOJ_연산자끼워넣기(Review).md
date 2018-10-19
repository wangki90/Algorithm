```c++
#include <iostream>
#include <cstdio>
#include <cstring>
#include <utility>
#include <algorithm>
#include <vector>

using namespace std;
int n;
int oper[4];
vector<int> num;
int min_value;
int max_value;
void dfs(int depth, int sum) {

	if (depth == n - 1) {
		max_value = max(max_value, sum);
		min_value = min(min_value, sum);

		return;
	}

	for (int i = 0; i < 4; i++) {
		if (oper[i] > 0) {
			oper[i]--;
			if (i == 0) {
				dfs(depth + 1, sum + num[depth + 1]);
			}
			else if (i == 1) {
				dfs(depth + 1, sum - num[depth + 1]);
			}
			else if (i == 2) {
				dfs(depth + 1, sum * num[depth + 1]);
			}
			else {
				dfs(depth + 1, sum / num[depth + 1]);
			}
			oper[i]++;
		}
	}
}
int main() {
	max_value = -2000000000;
	min_value = 2000000000;
	scanf("%d", &n);
	for (int i = 0; i < n; i++) {
		int x;
		scanf("%d", &x);
		num.push_back(x);
	}

	scanf("%d %d %d %d", &oper[0], &oper[1], &oper[2], &oper[3]);


	dfs(0, num[0]);

	printf("%d\n%d\n", max_value, min_value);

	return 0;
}
```

