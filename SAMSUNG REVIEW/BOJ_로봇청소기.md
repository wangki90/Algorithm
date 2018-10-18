```c++
#include <cstdio>
#include <algorithm>
#include <vector>
#include <utility>
using namespace std;

int map[51][51];
bool visit[51][51];
int n, m;
int dx[] = { -1,0,1,0 };
int dy[] = { 0,1,0,-1 };
int main() {

	for (int i = 0; i < 51; i++) {
		for (int j = 0; j < 51; j++) {
			map[51][51] = -1;
			visit[51][51] = false;
		}
	}

	scanf("%d %d", &n, &m);

	pair<int, int> start;
	int dir;
	scanf("%d %d %d", &start.first, &start.second, &dir);
	visit[start.first][start.second] = true;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			scanf("%d", &map[i][j]);
		}
	}
	int cdir = dir;
	int cx = start.first;
	int cy = start.second;
	int rot_cnt = 0;
	int answer = 1;

	int copy_map[51][51];
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			copy_map[i][j] = map[i][j];
		}
	}
	copy_map[start.first][start.second] = 3;
	while (1) {
		int ndir = (cdir + 3) % 4;
		int nx = cx + dx[ndir];
		int ny = cy + dy[ndir];
		

		if (map[nx][ny] == 0 && !visit[nx][ny]) {
			visit[nx][ny] = true;
			cx = nx;
			cy = ny;
			cdir = ndir;
			rot_cnt = 0;
			copy_map[nx][ny] = 3;
			answer++;
		}
		else {
			cdir = ndir;
			rot_cnt++;
		}

		if (rot_cnt == 4) {
			ndir = (cdir + 2) % 4;
			if (map[cx + dx[ndir]][cy + dy[ndir]] == 1) {
				break;
			}
			else {
				cx += dx[ndir];
				cy += dy[ndir];
				rot_cnt = 0;
			}
		}

	}

	printf("%d\n", answer);

	return 0;
}
```

