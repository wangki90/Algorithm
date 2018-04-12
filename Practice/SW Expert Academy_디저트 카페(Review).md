```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <utility>
using namespace std;

int n;

int dx[] = { 1,1,-1,-1 };
int dy[] = { 1,-1,-1,1 };
int map[21][21];
int visit[21][21];
int chk[101];
pair<int, int> start;
int answer;

void dfs(int x, int y, int depth, int dir, int turn_cnt) {
	
	if (turn_cnt > 3)
		return;

	if (x < start.first)
		return;
	
	int nx = x + dx[dir]; 
	int ny = y + dy[dir];

	
	if (nx == start.first && ny == start.second) {
		answer = max(depth, answer);
		return;
	}
	if (nx >= 0 && nx < n && ny >= 0 && ny < n) {
		if (visit[nx][ny] == 0 && chk[map[nx][ny]] == 0) {
			visit[nx][ny] = 1;
			chk[map[nx][ny]] = 1;
			dfs(nx, ny, depth + 1, dir, turn_cnt); //방향 그대로
			visit[nx][ny] = 0;
			chk[map[nx][ny]] = 0;
		}
	}

	nx = x + dx[(dir + 1) % 4];
	ny = y + dy[(dir + 1) % 4];

	if (nx == start.first && ny == start.second) {
		answer = max(depth, answer);
		return;
	}

	if (nx >= 0 && nx < n && ny >= 0 && ny < n) {
		if (visit[nx][ny] == 0 && chk[map[nx][ny]] == 0) {
			visit[nx][ny] = 1;
			chk[map[nx][ny]] = 1;
			dfs(nx, ny, depth + 1, (dir + 1) % 4, turn_cnt + 1); //방향 바꿔서
			visit[nx][ny] = 0;
			chk[map[nx][ny]] = 0;
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
		scanf("%d", &n);

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
				memset(chk, 0, sizeof(chk));
				chk[map[i][j]] = 1;
				visit[i][j] = 1;
				start.first = i;
				start.second = j;
				dfs(i, j, 1, 0, 0);
			}
		}
		if (answer == 0)
			answer = -1;

		printf("#%d %d\n", test_case, answer);


	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

