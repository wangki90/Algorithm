```c++
// MAP 배열의 인덱스를 초과하는 부분에 대해서 Ex) MAP[-1][n+1] or MAP[-1][0] 
// 이런지점의 값은 정확히 알 수 없음. + 실행시, 인덱스 오류도 나질 않음
// 주의할것.!!

#include <cstdio>
#include <iostream>
#include <algorithm>
#include <queue>
#include <utility>
#include <vector>
#include <cstring>

using namespace std;
typedef struct white {
	int x;
	int y;
}white;

int n;
int map[101][101];
vector<pair<int, int>> black;
vector<vector<white>> worm;
int score;
int answer;
int dx[] = { 0,-1,0,1 };
int dy[] = { 1,0,-1,0 };
void move(int x, int y, int dir) {

	pair<int, int> start = make_pair(x, y);
	int cdir = dir;
	int nx = x;
	int ny = y;
	int time = 0;

	while (1) {
		bool chk1 = false, chk2 = false;

		if (map[nx][ny] == -1 || (nx == start.first && ny == start.second && time != 0)) {
			answer = max(answer, score);
			return;
		}

		if ((map[nx][ny] >= 1 && map[nx][ny] <= 5) || nx == -1 || nx == n || ny == -1  || ny == n){
			score++;

			if (map[nx][ny] == 1) {
				if (cdir == 0) {
					cdir = 2;
				}
				else if (cdir == 1) {
					cdir = 3;
				}
				else if (cdir == 2) {
					cdir = 1;
				}
				else {
					cdir = 0;
				}
			}
			else if (map[nx][ny] == 2) {
				if (cdir == 0) {
					cdir = 2;
				}
				else if (cdir == 1) {
					cdir = 0;
				}
				else if (cdir == 2) {
					cdir = 3;
				}
				else {
					cdir = 1;
				}
			}
			else if (map[nx][ny] == 3) {
				if (cdir == 0) {
					cdir = 3;
				}
				else if (cdir == 1) {
					cdir = 2;
				}
				else if (cdir == 2) {
					cdir = 0;
				}
				else {
					cdir = 1;
				}
			}
			else if (map[nx][ny] == 4) {
				if (cdir == 0) {
					cdir = 1;
				}
				else if (cdir == 1) {
					cdir = 3;
				}
				else if (cdir == 2) {
					cdir = 0;
				}
				else {
					cdir = 2;
				}
			}
			else if (map[nx][ny] == 5) {
				if (cdir == 0) {
					cdir = 2;
				}
				else if (cdir == 1) {
					cdir = 3;
				}
				else if (cdir == 2) {
					cdir = 0;
				}
				else {
					cdir = 1;
				}
			}
			else if (nx == -1) {
				cdir = 3;
			}
			else if (nx == n) {
				cdir = 1;
			}
			else if (ny == -1) {
				cdir = 0;
			}
			else if (ny == n) {
				cdir = 2;
			}

		}
        //처음에 else if대신 if만 썻다가 위에 if문에도 들어오고 아래 if문에도 들어오는 테스트 케이스가 존재해서 무한루프에 빠졌음.
        //else if(map[nx][ny] >= 6 && map[nx][ny] <= 10) 고치거나 아래와 같이..
        
		if (map[nx][ny] >= 6 && map[nx][ny] <= 10 && !(nx == -1 || nx == n || ny == -1 || ny == n)) {
			if (worm[map[nx][ny] - 6][0].x == nx && worm[map[nx][ny] - 6][0].y == ny) {
				int a = worm[map[nx][ny] - 6][1].x;
				int b = worm[map[nx][ny] - 6][1].y;
				nx = a, ny = b;
			}
			else {
				int a = worm[map[nx][ny] - 6][0].x;
				int b = worm[map[nx][ny] - 6][0].y;
				nx = a, ny = b;
			}
		}

		nx += dx[cdir];
		ny += dy[cdir];
		time++;

	}
}
int main(int argc, char** argv) {

	int tc;

	cin >> tc;

	for (int test_case = 1; test_case <= tc; test_case++) {
		
		worm.resize(5);
		for (int i = 0; i < worm.size(); i++) {
			worm[i].clear();
		}
		for (int i = 0; i < 101; i++) {
			for (int j = 0; j < 101; j++) {
				map[i][j] = 0;
			}
		}

		answer = 0;
		black.clear();

		cin >> n;

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				int x;
				cin >> x;

				map[i][j] = x;
				if(map[i][j] == -1){
					black.push_back(make_pair(i, j));
				}
				else if (map[i][j] >= 6 && map[i][j] <= 10) {
					white tmp;
					tmp.x = i;
					tmp.y = j;
					worm[map[i][j] - 6].push_back(tmp);
				}
			}
		}
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				if (map[i][j] == 0) {
					for (int k = 0; k < 4; k++) {
						score = 0;
						move(i, j, k);
					}
				}
			}
		}

		printf("#%d %d\n", test_case, answer);


	}


	return 0;
}
```

