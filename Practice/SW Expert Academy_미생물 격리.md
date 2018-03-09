```c++
//미생물 격리, 시뮬레이션
#include<iostream>
#include <cstdio>
#include <vector>
#include <cstring>
using namespace std;
typedef struct cell {
	int x;
	int y;
	int cnt;
	int dir;
}cell;
int n, m, k;
int dx[] = { 0,-1,1,0,0 }; //x,상,하,좌,우
int dy[] = { 0,0,0,-1,1 };
int map[101][101];
int isDie[1001];
vector<cell> c;
int change_dir(int cdir) {
	if (cdir == 1) {
		return 2;
	}
	else if (cdir == 2) {
		return 1;
	}
	else if (cdir == 3) {
		return 4;
	}
	else {
		return 3;
	}
}
void init() {
	memset(isDie, -1, sizeof(isDie));
	for (int i = 0; i < n; i++) {
		memset(map[i], 0, sizeof(map[i]));
	}
	c.clear();
	c.resize(k + 1);
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);

	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		scanf("%d %d %d", &n, &m, &k);
		init();
		for (int i = 1; i <= k; i++) {
			scanf("%d %d %d %d", &c[i].x, &c[i].y, &c[i].cnt, &c[i].dir);
			map[c[i].x][c[i].y] = i;
			isDie[i] = i;
		}
		//for (int i = 0; i < n; i++) {
		//	for (int j = 0; j < n; j++) {
		//		printf("%d ", map[i][j]);
		//	}
		//	printf("\n");
		//}
		//printf("\n");
		while (m > 0) {
			int next_map[101][101];
			int sum[101][101];
			for (int i = 0; i < n; i++) {
				memset(next_map[i], 0, sizeof(next_map[i]));
				memset(sum[i], 0, sizeof(sum[i]));
			}
			for (int i = 1; i <= k; i++) {
				if (isDie[i] == -1)continue;

				int cx = c[i].x; int cy = c[i].y;
				int nx = cx + dx[c[i].dir];
				int ny = cy + dy[c[i].dir];
				int pre_idx = next_map[nx][ny];
				int idx = i;

				next_map[nx][ny] = idx;
				if (nx == 0 || nx == n - 1 || ny == 0 || ny == n - 1) { //약에 닿았을 경우
					c[idx].cnt /= 2;
					c[idx].dir = change_dir(c[i].dir);
					if (c[idx].cnt == 0)
						isDie[idx] = -1;
				}
				if (pre_idx != 0) { //합쳐지는 경우
					if (c[pre_idx].cnt >= c[idx].cnt) {
						next_map[nx][ny] = pre_idx;
						isDie[idx] = -1;
					}
					else {
						isDie[pre_idx] = -1;
					}
					if (sum[nx][ny] == 0)
						sum[nx][ny] = c[pre_idx].cnt + c[idx].cnt;
					else
						sum[nx][ny] += c[idx].cnt;
				}
				map[cx][cy] = 0;
				c[i].x = nx; c[i].y = ny;
			}
			for (int i = 0; i < n; i++) {
				for (int j = 0; j < n; j++) {
					map[i][j] = next_map[i][j];
					if (sum[i][j] != 0) {
						c[map[i][j]].cnt = sum[i][j];
					}
				}
			}
			//for (int i = 0; i < n; i++) {
			//	for (int j = 0; j < n; j++) {
			//		printf("%d ", map[i][j]);
			//	}
			//	printf("\n");
			//}
			//printf("\n");
			m--;
		}
		int answer = 0;
		for (int i = 1; i <= k; i++) {
			if (isDie[i] != -1) {
				answer += c[i].cnt;
			}
		}
		printf("#%d %d\n", test_case, answer);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

