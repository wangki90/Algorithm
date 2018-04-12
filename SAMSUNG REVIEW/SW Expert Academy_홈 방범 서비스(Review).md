```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <queue>
#include <cstring>

using namespace std;

int n, m;
int map[21][21];
int visit[21][21];
int dx[] = { 1,0,-1,0 };
int dy[] = { 0,1,0,-1 };
int answer;
void bfs(int x, int y) {

	queue<pair<int, int>> que;

	int house_cnt = 0;
	int K = 1;
	que.push(make_pair(x, y));
	visit[x][y] = 1;
	if (map[x][y] == 1) {
		house_cnt++;
		answer = max(answer, house_cnt);
	}

	while (!que.empty()) {
		int queSize = que.size();
		if (K > n)return;
		K++;
		for (int z = 0; z < queSize; z++) {

			int cx = que.front().first;
			int cy = que.front().second;

			que.pop();

			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];

				if (nx < 0 || nx >= n || ny < 0 || ny >= n)
					continue;

				if (visit[nx][ny] == 1)
					continue;

				visit[nx][ny] = 1;
				que.push(make_pair(nx, ny));
				if (map[nx][ny] == 1)
					house_cnt++;

			}

		}
		if ((house_cnt * m) - ((K*K) + (K - 1)*(K - 1)) >= 0) {
			answer = max(answer, house_cnt);
		}
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
		answer = 0;
		scanf("%d %d", &n, &m);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
			}
		}

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				for (int k = 0; k < n; k++) {
					memset(visit[k], 0, sizeof(visit[k]));
				}

				bfs(i, j);
			}
		}

		printf("#%d %d\n", test_case, answer);

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

