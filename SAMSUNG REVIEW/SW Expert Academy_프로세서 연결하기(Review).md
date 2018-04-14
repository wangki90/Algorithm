```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <utility>
#include <vector>
#include <cstring>
using namespace std;

int map[12][12];
int n;
vector<pair<int, int>> core;
int dx[] = { -1,0,1,0 };//상,우,하,좌
int dy[] = { 0,1,0,-1 };
int total_core, total_length;
void dfs(int depth, int core_cnt, int line_length) {

	if (depth == core.size()) {

		if (total_core < core_cnt) { //코어수가 많을 때, 전선 길이 갱신
			total_core = core_cnt;
			total_length = line_length;
		}
		if (total_core == core_cnt && total_length > line_length) { //코어수 같고 길이가 짧을때,
			total_core = core_cnt;
			total_length = line_length;
		}
		return;
	}

	int cx = core[depth].first;
	int cy = core[depth].second;

	if (cx == 0 || cx == n - 1 || cy == 0 || cy == n - 1) {
		dfs(depth + 1, core_cnt + 1, line_length);
		return;
	}

	for (int i = 0; i < 4; i++) {

		int cmap[12][12];

		for (int j = 0; j < n; j++) {
			memcpy(cmap[j], map[j], sizeof(int)*n);
		}

		int nx = cx;
		int ny = cy;
		int tmp_line = 0;
		bool flag = true;
		while (1) {
			nx += dx[i];
			ny += dy[i];
			if (map[nx][ny] == 0) {
				tmp_line++;
				map[nx][ny] = 2;
			}
			else {
				flag = false;
				break;
			}
			if (nx == 0 || nx == n - 1 || ny == 0 || ny == n - 1) {  //가장자리
				break;
			}
		}

		if (flag) {
			dfs(depth + 1, core_cnt + 1, line_length + tmp_line);
			for (int j = 0; j < n; j++) {
				memcpy(map[j], cmap[j], sizeof(int)*n);
			}
		}
		else {
			for (int j = 0; j < n; j++) {
				memcpy(map[j], cmap[j], sizeof(int)*n);
			}
			continue;
		}
		

	}
	dfs(depth + 1, core_cnt, line_length);
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		core.clear();
		total_core = 0, total_length = 987654321;
		scanf("%d", &n);
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
				if (map[i][j] == 1) {
					core.push_back(make_pair(i, j));
				}
			}
		}

		dfs(0, 0, 0);

		printf("#%d %d\n", test_case, total_length);

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

