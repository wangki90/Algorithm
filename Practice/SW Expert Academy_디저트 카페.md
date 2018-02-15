```c++
//dfs
#include <cstdio>
#include <algorithm>
#include <utility>
#include <vector>
#include <cstring>

using namespace std;
int n;
int map[21][21];
bool chk[101];
bool visit[21][21];
int ret = 0;
int dx[] = { 1,1,-1,-1 }; //↘,↙,↖,↗
int dy[] = { 1,-1,-1,1 };
vector<int> answer;
void dfs(int x, int y,int depth, pair<int,int> start, int direction, int changeDirectionCnt) {

	if (x == start.first && y == start.second && depth != 0) {
		ret = max(ret, depth);
		return;
	}
	if (changeDirectionCnt > 3)return; //방향 전환 4번 이상이면 위로 돌아 왔다는 뜻이므로 종료
	
	chk[map[x][y]] = true;
	visit[x][y] = true;

	for (int i = 0; i < 4; i++) {
		int nx1 = x + dx[i], ny1 = y + dy[i], nx2 = x + dx[(i + 1) % 4], ny2 = y + dy[(i + 1) % 4];
		if (direction == i) {
			//방향 그대로 진행,
			if (nx1 >= 0 && nx1 < n && ny1 >= 0 && ny1 < n) {
				if (!chk[map[nx1][ny1]] && !visit[nx1][ny1] || (nx1 == start.first && ny1 == start.second))
					dfs(nx1, ny1, depth + 1, start, direction, changeDirectionCnt);
			}
			//방향 바꿔서 진행.
			if (nx2 >= 0 && ny2 >= 0 && nx2 < n && ny2 < n) {
				if (!chk[map[nx2][ny2]] && !visit[nx2][ny2] || (nx2 == start.first && ny2 == start.second))
					dfs(nx2, ny2, depth + 1, start, (direction + 1) % 4, changeDirectionCnt + 1);
			}
			break;
		}
	}

	chk[map[x][y]] = false;
	visit[x][y] = false;

	return;
}
int main() {
	int T;

	scanf("%d", &T);

	for (int test = 0; test < T; test++) {
		ret = 0;

		scanf("%d", &n);
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
			}
		}

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				dfs(i, j, 0, make_pair(i, j), 0, 0);
			}
		}
		if (ret == 0) {
			answer.push_back(-1);
		}
		else {
			answer.push_back(ret);
		}

	}
	for (int i = 0; i < answer.size(); i++) {
		printf("#%d %d\n", i + 1, answer[i]);
	}
	return 0;
}
```

