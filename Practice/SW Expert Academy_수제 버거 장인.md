```c++
/*
DFS + Back tracking
*/
#include <cstdio>
#include <iostream>
#include <cstring>

using namespace std;
int n, m;
int a[21];
int b[21][21];
int out[1000001];
int answer;
bool chk(int cur, int depth) {
	for (int i = 0; i < depth; i++) {
		if (b[out[i] - 1][cur] == 1 || b[cur][out[i] - 1] == 1)
			return false;
	}
	return true;
}
void solution(int cur, int depth, int end) {

	if (depth == end) {
		answer++;
		return;
	}

	for (int i = cur; i < n; i++) {
		if (depth > 0) {
			if (chk(i, depth)) {
				out[depth] = i + 1;
				solution(i + 1, depth + 1, end);
			}
		}
		else {
			out[depth] = i + 1;
			solution(i + 1, depth + 1, end);
		}
	}

}
void init() {
	answer = 0;
	memset(a, 0, sizeof(a));
	for (int i = 0; i < 21; i++) {
		memset(b[i], 0, sizeof(b[i]));
	}
}
int main() {
	int T;
	cin >> T;

	for (int tc = 1; tc <= T; tc++) {
		init();
		cin >> n >> m;

		for (int i = 0; i < m; i++) {
			int x, y;
			cin >> x >> y;
			b[x - 1][y - 1] = 1;
			b[y - 1][x - 1] = 1;
		}
		for (int i = 1; i <= n; i++) {
			solution(0, 0, i);
		}
		printf("#%d %d\n", tc, answer + 1);
	}
	return 0;
}
```

