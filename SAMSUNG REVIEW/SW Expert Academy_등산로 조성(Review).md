```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <utility>
#include <vector>

using namespace std;
int top;
vector<pair<int, int>> tops;
int n, k;
int map[9][9];
int visit[9][9];
bool dig;
int dx[] = { 1,0,-1,0 };
int dy[] = { 0,1,0,-1 };
int answer;
void solution(int x, int y, bool is_dig, int cnt) {

	answer = max(answer, cnt);

	for (int i = 0; i < 4; i++) {
		int nx = x + dx[i];
		int ny = y + dy[i];

		if (nx < 0 || nx >= n || ny < 0 || ny >= n)
			continue;
		
		if (visit[nx][ny])
			continue;
		
		//안파는 경우
		if (map[x][y] > map[nx][ny]) {
			visit[nx][ny] = true;
			solution(nx, ny, is_dig, cnt + 1);
			visit[nx][ny] = false;
		}
		//파는 경우
		if (!is_dig) {
			for (int j = 1; j <= k; j++) {
				if (map[x][y] > map[nx][ny] - j) {
					map[nx][ny] -= j;
					visit[nx][ny] = true;
					is_dig = true;
					solution(nx, ny, is_dig, cnt + 1);
					visit[nx][ny] = false;
					map[nx][ny] += j;
					is_dig = false;
				}
			}
		}
	}

}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("C:/Users/Wang Kyu Bong/Desktop/sample_input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		
		top = -1;
		answer = -1;
		tops.clear();
		for (int i = 0; i < 9; i++) {
			for (int j = 0; j < 9; j++) {
				visit[i][j] = false;
			}
		}
		scanf("%d %d", &n, &k);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
				top = max(top, map[i][j]);
			}
		}

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				if (top == map[i][j]) {
					tops.push_back(make_pair(i, j));
				}
			}
		}
		for (int i = 0; i < tops.size(); i++) {
			dig = false;
			for (int i = 0; i < 9; i++) {
				for (int j = 0; j < 9; j++) {
					visit[i][j] = false;
				}
			}
			visit[tops[i].first][tops[i].second] = true;
			solution(tops[i].first, tops[i].second, dig, 1);
			visit[tops[i].first][tops[i].second] = false;
		}


		printf("#%d %d\n", test_case, answer);

	}
	return 0;
}
```

