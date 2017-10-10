```c++
//bfs
#include <cstdio>
#include <algorithm>
#include <vector>
#include <queue>
#include <cstring>
#include <utility>
using namespace std;

int map[51][51];
bool chk[51][51];
int a[51][51];
int n, m, r, c, l;
int dx[] = { 1,0,-1,0 };  //아래, 오른쪽, 위, 왼쪽
int dy[] = { 0,1,0,-1 };
vector<int> answer;
void bfs() {

	int level = 0;
	queue<pair<int, int> > que;
	que.push(make_pair(r, c));
	chk[r][c] = true;
	a[r][c]++;
	level++;
	

	while (!que.empty()) {
		int cx = que.front().first; //현재 x좌표
		int cy = que.front().second; //현재 y좌표
		int cv = a[cx][cy]; //현재 깊이
		int cp = map[cx][cy]; //현재 파이프
		if (cv >= l)break; 
		que.pop();
		if (cp == 1) {
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
					if (!chk[nx][ny] && map[nx][ny] != 0) {
						if (i == 0 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 1 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 2 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 3 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}

					}
				}

			}
		}
		else if (cp == 2) {
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
					if (!chk[nx][ny] && map[nx][ny] != 0) {
						if (i == 0 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 2 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
					}
				}
			}
		}
		else if (cp == 3) {
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
					if (!chk[nx][ny] && map[nx][ny] != 0) {
						if (i == 1 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 3 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
					}
				}
			}			
		}
		else if (cp == 4) {
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
					if (!chk[nx][ny] && map[nx][ny] != 0) {
						if (i == 1 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 2 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
					}
				}

			}

		}
		else if (cp == 5) {
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
					if (!chk[nx][ny] && map[nx][ny] != 0) {
						if (i == 0 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 1 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
					}
				}
			}

		}
		else if (cp == 6) {
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
					if (!chk[nx][ny] && map[nx][ny] != 0) {
						if (i == 0 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 3 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}

					}
				}
			}
		}
		else if (cp == 7) {
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
					if (!chk[nx][ny] && map[nx][ny] != 0) {
						if (i == 2 && (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}
						if (i == 3 && (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5)) {
							a[nx][ny] = cv + 1;
							chk[nx][ny] = true;
							que.push(make_pair(nx, ny));
							level++;
						}

					}
				}
			}
		}
	}
	
	answer.push_back(level);
}
int main() {
	int T;
	scanf("%d", &T);

	for (int test = 0; test < T; test++) {
		memset(chk, false, sizeof(chk));
		memset(a, 0, sizeof(a));
		scanf("%d %d %d %d %d", &n, &m, &r, &c, &l);
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < m; j++) {
				scanf("%d", &map[i][j]);
			}
		}

		bfs();

	}
	for (int i = 0; i < answer.size(); i++) {
		printf("#%d %d\n", i + 1, answer[i]);
	}

	return 0;
}
```

