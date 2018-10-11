```c++
//연쇄적으로 터지는 부분 Review
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <queue>
#include <utility>
#include <vector>
#include <cstring>
#define MAX 9999999
using namespace std;


typedef struct block {
	int x;
	int y;
	int p;
};
int answer;
int n, w, h;
int map[15][12];
int copy_map[15][12];
bool chk[4];
int out[4];
int dx[] = { 1,0,-1,0 };
int dy[] = { 0,1,0,-1 };

void arrange() {

	queue<int> que;


	for (int i = 0; i < w; i++) {
		for (int j = 0; j < h; j++) {
			if (map[j][i] != 0)
				que.push(map[j][i]);

			map[j][i] = 0;
		}
		int queSize = que.size();
		for (int j = h - queSize; j < h; j++) {
			map[j][i] = que.front();
			que.pop();
		}
	}
}
void fire(int idx) {


	int x = 0;
	int y = idx;

	while (map[x][y] == 0) {
		x++;
		if (x >= h)
			return;
	}
	queue<block> que;
	block b;
	b.x = x;
	b.y = y;
	b.p = map[x][y] - 1;
	que.push(b);

	map[x][y] = 0;

	while (!que.empty()) {
		int queSize = que.size();
		for (int z = 0; z < queSize; z++) {
			block tmp = que.front();
			que.pop();

			int cx = tmp.x;
			int cy = tmp.y;
			int cp = tmp.p;

			map[cx][cy] = 0;

			for (int i = 0; i < 4; i++) {

				int nx = cx;
				int ny = cy;
				int ncnt = cp;
				
				while (ncnt > 0) {

					nx += dx[i];
					ny += dy[i];

					if (nx < 0 || nx >= h || ny < 0 || ny >= w)
						break;

					if (map[nx][ny] == 0) {
						ncnt--;
						continue;
					}

					block t;
					t.x = nx;
					t.y = ny;
					t.p = map[nx][ny] - 1;
					que.push(t);
					map[nx][ny] = 0;
					ncnt--;

				}
			}
		}
	}

	arrange();



}
void init() {
	for (int i = 0; i < h; i++) {
		for (int j = 0; j < w; j++) {
			map[i][j] = copy_map[i][j];
		}
	}
}
void get_nums(int cur, int depth) {

	if (depth == n) {
		for (int i = 0; i < n; i++) {
			/*printf("%d ", out[i]);*/
			fire(out[i]);
		}
		/*printf("\n");*/

		int cnt = 0;
		for (int i = 0; i < h; i++) {
			for (int j = 0; j < w; j++) {
				if (map[i][j] != 0)
					cnt++;
			}
		}

		answer = min(answer, cnt);
		if (cnt == 0)
			return;
		init();

		return;
	}

	for (int i = 0; i < w; i++) {
		out[depth] = i;
		get_nums(i + 1, depth + 1);
	}
}
int main() {

	int tc;
	cin >> tc;

	for (int test_case = 1; test_case <= tc; test_case++) {

		answer = MAX;
		scanf("%d %d %d", &n, &w, &h);

		for (int i = 0; i < h; i++) {
			for (int j = 0; j < w; j++) {
				scanf("%d", &map[i][j]);
			}
		}
		for (int i = 0; i < h; i++) {
			for (int j = 0; j < w; j++) {
				copy_map[i][j] = map[i][j];
			}
		}

		get_nums(0, 0);

		printf("#%d %d\n", test_case, answer);
	}
	return 0;
}
```

