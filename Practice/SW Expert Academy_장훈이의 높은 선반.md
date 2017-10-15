```c++
#include <cstdio>
#include <vector>
#include <algorithm>
using namespace std;

int n, b;
vector<int> a;
int sum = 0;
vector<int> answer;
void dfs(int node,int sum) {

	sum += a[node];

	if (sum >= b) {
		answer.push_back(sum);
		return;
	}
	
	for (int i = node + 1; i < n; i++) {
		dfs(i,sum);
	}
}
int main() {
	int T;
	scanf("%d", &T);
	for (int test = 0; test < T; test++) {
		a.clear();
		answer.clear();
		scanf("%d %d", &n, &b);

		for (int i = 0; i < n; i++) {
			int x;
			scanf("%d", &x);
			a.push_back(x);
		}
		for (int i = 0; i < n; i++) {
			sum = 0;
			dfs(i,0);
		}

		sort(answer.begin(), answer.end());

		printf("#%d %d\n",test+1, answer[0] - b);
	}

	return 0;
}
```

