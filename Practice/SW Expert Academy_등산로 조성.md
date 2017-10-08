```c++
//bfs,완전탐색
#include <vector>
#include <cstdio>
#include <queue>
#include <utility>
#include <cstring>
#include <algorithm>

using namespace std;

int n, k;
vector<vector<int> > map;
vector<int> answer;
int ret;
vector<pair<int, int> > mLoc;
int dx[] = { 1, 0, -1, 0 };
int dy[] = { 0, 1, 0, -1 };

void bfs(vector<vector<int> > cmap) {

	queue<pair<int, int> > que;

	//큐에 최대값 푸시
	for (int k = 0; k < mLoc.size(); k++) {


		vector<vector<int> > dInfo(n, vector<int>(n, 1));

		que.push(mLoc[k]);
		while (!que.empty()) {
			int cx = que.front().first;
			int cy = que.front().second;
			que.pop();
			for (int i = 0; i < 4; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];
				if (nx >= 0 && ny >= 0 && nx < n && ny < n) {
					//값이 작을 경우만 이동
					if (cmap[cx][cy] > cmap[nx][ny]) {
						que.push(make_pair(nx, ny));
						dInfo[nx][ny] = dInfo[cx][cy] + 1;
						ret = max(ret, dInfo[nx][ny]);
					}
				}
			}
		}
	}
}
int main() {

	int T;
	scanf("%d", &T);

	for (int test = 0; test < T; test++) {
		ret = 0;

		scanf("%d %d", &n, &k);
		map.clear();
		map.resize(n);
		mLoc.clear();

		int tmp = 0;
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				int x;
				scanf("%d", &x);
				map[i].push_back(x);
				if (tmp < x)tmp = x;
			}
		}

		//최대값 위치 저장
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				if (map[i][j] == tmp) {
					mLoc.push_back(make_pair(i, j));
				}
			}
		}
		//공사 가능 높이만큼 빼주고 탐색
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				for (int q = 1; q <= k; q++) {
					vector<vector<int> > cmap = map;
					cmap[i][j] -= q;
					bfs(cmap);
				}
			}
		}
		answer.push_back(ret);
	}
	for (int i = 1; i <= T; i++)
		printf("#%d %d\n", i, answer[i - 1]);

	return 0;
}
```

