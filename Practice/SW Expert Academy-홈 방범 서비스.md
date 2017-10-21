```c++
//bfs, 주의!-->6. 도시에는 최소 1개 이상의 집이 존재한다. 답의 default = 1
#include <cstdio>
#include <algorithm>
#include <queue>
#include <vector>
#include <cstring>
#include <cmath>

using namespace std;
int map[21][21];
bool chk[21][21];
int n, m;
int dx[] = { 1,0,-1,0 };
int dy[] = { 0,1,0,-1 };
int answer;

void bfs(int x,int y) {

	for (int i = 0; i < n; i++) {
		memset(chk[i], false, sizeof(chk[i]));
	}

	int numOfhouse = 0;
	int level = 1;
	queue<pair<int, int> > que;
	que.push(make_pair(x, y));
	chk[x][y] = true;

	if (map[x][y] == 1)numOfhouse++;

	while (!que.empty()) {
		int qSize = que.size();
		for (int k = 0; k < qSize; k++) {
			int cx = que.front().first;
			int cy = que.front().second;
			que.pop();
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < n) {
					if (!chk[nx][ny]) {
						if (map[nx][ny] == 1)numOfhouse++;

						que.push(make_pair(nx, ny));
						chk[nx][ny] = true;
					}
				}
			}
		}
		level++;
		//보안회사의 이익 = 서비스 제공받는 집들을 통해 얻는 수익 - 운영 비용
		if ((numOfhouse * m) - (pow(level, 2) + pow(level - 1, 2)) >= 0) {
			answer = max(answer, numOfhouse);
		}
	}

}
int main() {
	
	int T;
	scanf("%d", &T);
	for (int test = 0; test < T; test++) {
		//최소 한집 존재
		answer = 1;

		scanf("%d %d", &n, &m);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
			}
		}

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				bfs(i, j);
			}
		}

		printf("#%d %d\n",test+1, answer);
	}

	return 0;
}
```

