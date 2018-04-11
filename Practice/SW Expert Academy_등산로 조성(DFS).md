```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>
#include <utility>
#include <cstring>
using namespace std;

int dx[] = { 1,0,-1,0 };
int dy[] = { 0,1,0,-1 };
int n, k;
int map[8][8];
int visited[8][8];
int max_length;
vector<pair<int, int>> start;
void dfs(pair<int,int> loc, int isItem, int depth) {
	
	int cx = loc.first;
	int cy = loc.second;

	for (int i = 0; i < 4; i++) {
		int nx = cx + dx[i];
		int ny = cy + dy[i];
		
		if (nx < 0 || nx >= n || ny < 0 || ny >= n)
			continue;

		if (visited[nx][ny] == 1)
			continue;
		//DFS 백트래킹
		if (map[nx][ny] < map[cx][cy]) {
			visited[nx][ny] = 1;
			dfs(make_pair(nx, ny), isItem, depth + 1);
			visited[nx][ny] = 0;
		}
		else {
			//깎을 수 있는 최대 깊이가 K라는 것 --> K보다 적게 깍을 수 있음
			int tmp = k;
			for (int j = 1; j <= 5; j++) {
				if (map[nx][ny] - j < map[cx][cy]) {
					tmp = j;
					break;
				}
			}
			if (k >= tmp) {
				if (isItem == 0 && map[nx][ny] - tmp < map[cx][cy]) {
					visited[nx][ny] = 1;
					isItem = 1;
					map[nx][ny] -= tmp;
					dfs(make_pair(nx, ny), isItem, depth + 1);
					map[nx][ny] += tmp;
					isItem = 0;
					visited[nx][ny] = 0;
				}
			}
		}
	}

	max_length = max(max_length, depth);

}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		start.clear();
		max_length = 0;
		scanf("%d %d", &n, &k);
		int max_value = 0;
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
				if (map[i][j] > max_value) {
					max_value = map[i][j];
				}
			}
		}
		
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				if (max_value == map[i][j]) {
					start.push_back(make_pair(i, j));
				}
			}
		}

		for (int i = 0; i < start.size(); i++) {
			for (int j = 0; j < n; j++) {
				memset(visited[j], 0, sizeof(visited[j]));
			}
			visited[start[i].first][start[i].second] = 1;
			dfs(start[i],0,1);
		}

		printf("#%d %d\n", test_case, max_length);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

