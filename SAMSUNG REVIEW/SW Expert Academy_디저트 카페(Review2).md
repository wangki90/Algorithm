```c++
//디저트 카페 REVIEW3.
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <utility>
using namespace std;
int map[50][50];
bool chk[102];
int n;
int dx[] = {1, 1, -1, -1};
int dy[] = {1, -1, -1, 1};
pair<int, int> start;
int answer;
void solution(int x, int y, int cnt, int dir) {

	int cx = x;
	int cy = y;
	int cdir = dir;
	int dessert = map[cx][cy];

	if (cnt != 0 && cdir == 3 && (cx == start.first && cy == start.second)) { // 종료 조건

		answer = max(answer, cnt);
		return;
	}

	if (chk[map[cx][cy]] || cx < 0 || cx >= n || cy < 0 || cy >= n) // 먹었던 디저트
		return;

	chk[map[cx][cy]] = true;
	solution(cx + dx[cdir], cy + dy[cdir], cnt + 1, cdir);
	solution(cx + dx[(cdir + 1) % 4], cy + dy[(cdir + 1) % 4], cnt + 1, (cdir + 1) % 4);
	chk[map[cx][cy]] = false;


}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("C:/Users/Wang Kyu Bong/Desktop/sample_input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		
		answer = -1;
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				map[i][j] = -1;
			}
		}
		scanf("%d", &n);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
			}
		}

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				start = make_pair(i, j);
				solution(i, j, 0, 0);
			}
		}

		printf("#%d %d\n", test_case, answer);
	}
	return 0;
}
```

