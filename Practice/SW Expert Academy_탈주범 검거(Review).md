```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <queue>
#include <utility>

using namespace std;
int n, m, t;
pair<int, int> start;
int map[51][51];
int visit[51][51];
int answer;
void bfs() {

	int time = 1;
	queue<pair<int, int>> que;

	que.push(start);
	visit[start.first][start.second] = 1;


	while (!que.empty()) {
		int queSize = que.size();
		for (int z = 0; z < queSize; z++) {

			if (time == t)return;

			int cx = que.front().first;
			int cy = que.front().second;
			int nx, ny;
			que.pop();

			if (map[cx][cy] == 0)
				continue;

			if (map[cx][cy] == 1) {

				int dx[] = { 1,0,-1,0 }; //D,R,U,L
				int dy[] = { 0,1,0,-1 };

				for (int i = 0; i < 4; i++) {
					nx = cx + dx[i];
					ny = cy + dy[i];

					if (nx < 0 || nx >= n || ny < 0 || ny >= m)
						continue;

					if (visit[nx][ny] == 1 || map[nx][ny] == 0)
						continue;

					if (i == 0) {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else if (i == 1) {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else if (i == 2) {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
				}

			}
			else if (map[cx][cy] == 2) {
				int dx[] = { 1,-1 };
				int dy[] = { 0,0 };
				for (int i = 0; i < 2; i++) {
					nx = cx + dx[i];
					ny = cy + dy[i];

					if (nx < 0 || nx >= n || ny < 0 || ny >= m)
						continue;

					if (visit[nx][ny] == 1 || map[nx][ny] == 0)
						continue;
					if (i == 0) {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
				}

			}
			else if (map[cx][cy] == 3) {
				int dx[] = { 0, 0 };
				int dy[] = { 1,-1 };
				for (int i = 0; i < 2; i++) {

					nx = cx + dx[i];
					ny = cy + dy[i];

					if (nx < 0 || nx >= n || ny < 0 || ny >= m)
						continue;

					if (visit[nx][ny] == 1 || map[nx][ny] == 0)
						continue;
					if (i == 0) {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
				}
			}
			else if (map[cx][cy] == 4) {

				int dx[] = { -1, 0 };
				int dy[] = { 0, 1 };
				for (int i = 0; i < 2; i++) {

					nx = cx + dx[i];
					ny = cy + dy[i];

					if (nx < 0 || nx >= n || ny < 0 || ny >= m)
						continue;

					if (visit[nx][ny] == 1 || map[nx][ny] == 0)
						continue;
					if (i == 0) {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
				}
			}
			else if (map[cx][cy] == 5) {

				int dx[] = { 0, 1 };
				int dy[] = { 1, 0 };
				for (int i = 0; i < 2; i++) {

					nx = cx + dx[i];
					ny = cy + dy[i];

					if (nx < 0 || nx >= n || ny < 0 || ny >= m)
						continue;

					if (visit[nx][ny] == 1 || map[nx][ny] == 0)
						continue;
					if (i == 0) {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 6 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
				}

			}
			else if (map[cx][cy] == 6) {

				int dx[] = { 0, 1 };
				int dy[] = { -1, 0 };
				for (int i = 0; i < 2; i++) {

					nx = cx + dx[i];
					ny = cy + dy[i];

					if (nx < 0 || nx >= n || ny < 0 || ny >= m)
						continue;

					if (visit[nx][ny] == 1 || map[nx][ny] == 0)
						continue;
					if (i == 0) {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 4 || map[nx][ny] == 7) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
				}
			}
			else if (map[cx][cy] == 7) {

				int dx[] = { -1, 0 };
				int dy[] = { 0, -1 };
				for (int i = 0; i < 2; i++) {

					nx = cx + dx[i];
					ny = cy + dy[i];

					if (nx < 0 || nx >= n || ny < 0 || ny >= m)
						continue;

					if (visit[nx][ny] == 1 || map[nx][ny] == 0)
						continue;
					if (i == 0) {
						if (map[nx][ny] == 1 || map[nx][ny] == 2 || map[nx][ny] == 5 || map[nx][ny] == 6) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
					else {
						if (map[nx][ny] == 1 || map[nx][ny] == 3 || map[nx][ny] == 4 || map[nx][ny] == 5) {
							visit[nx][ny] = 1;
							que.push(make_pair(nx, ny));
							answer++;
						}
					}
				}
			}
		}
		time++;
	}
}
void init() {
	
	answer = 1;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			visit[i][j] = 0;
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

		scanf("%d %d %d %d %d", &n, &m, &start.first, &start.second, &t);
		init();

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < m; j++) {
				scanf("%d", &map[i][j]);
			}
		}

		bfs();

		printf("#%d %d\n", test_case, answer);

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

