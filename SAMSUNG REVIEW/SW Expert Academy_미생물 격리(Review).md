```c++
#include<iostream>
#include <vector>
#include <cstring>
#include <algorithm>

using namespace std;

typedef struct cell {
	int x;
	int y;
	int num;
	int dir;
}cell;

int n, m, k;
vector<cell> vc;
int map[101][101];
int dx[] = {0, -1, 1, 0, 0 };
int dy[] = {0, 0, 0, -1, 1 };


int solution() {

	while (m != 0) {

		int cmap[101][101];
		int dmap[101][101];
		int max_value[101][101];

		for (int i = 0; i < n; i++) {
			memset(cmap[i], 0, sizeof(cmap[i])); //미생물 수 저장
			memset(dmap[i], 0, sizeof(dmap[i])); //방향저장
			memset(max_value[i], 0, sizeof(max_value[i])); //최대로 많은 군집 수 저장
		}

		for (int i = 0; i < vc.size(); i++) {
			cell tmp = vc[i];
			vector<cell> tmp_vc;
			int nx = tmp.x + dx[tmp.dir]; int ny = tmp.y + dy[tmp.dir];
			
			if (nx == 0 || nx == n - 1 || ny == 0 || ny == n - 1) { //가장자리.
				if (tmp.dir == 1) {
					tmp.dir = 2;
				}
				else if (tmp.dir == 2) {
					tmp.dir = 1;
				}
				else if (tmp.dir == 3) {
					tmp.dir = 4;
				}
				else {
					tmp.dir = 3;
				}
				tmp.num /= 2;
			}
			if (cmap[nx][ny] == 0) { //합쳐지지 않는 경우,
				cmap[nx][ny] = tmp.num;
				dmap[nx][ny] = tmp.dir;
				max_value[nx][ny] = tmp.num;
			}
			else { //합쳐지는 경우
				if (max_value[nx][ny] > tmp.num) { //현재 군집의 수가, 이전 군집보다 적을 경우
					cmap[nx][ny] += tmp.num;
				}
				else { // 현재 군집의 수가, 이전 군집보다 많을 경우,
					dmap[nx][ny] = tmp.dir;
					cmap[nx][ny] += tmp.num;
					max_value[nx][ny] = max(max_value[nx][ny], tmp.num);
				}
			}
		}
		vc.clear();
		for (int i = 0; i < n; i++) { 
			for (int j = 0; j < n; j++) {
				if (cmap[i][j] != 0) {
					cell tmp;
					tmp.x = i; tmp.y = j; tmp.num = cmap[i][j]; tmp.dir = dmap[i][j];
					vc.push_back(tmp);
				}
			}
		}
		for (int i = 0; i < n; i++) {
			memcpy(map[i], cmap[i], sizeof(int)*n);
		}
		m--;
	}

	int total = 0;

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			if (map[i][j] != 0) {
				total += map[i][j];
			}
		}
	}

	return total;

}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		vc.clear();
		scanf("%d %d %d", &n, &m, &k);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				map[i][j] = 0;
			}
		}

		for (int i = 0; i < k; i++) {
			cell tmp;
			scanf("%d %d %d %d", &tmp.x, &tmp.y, &tmp.num, &tmp.dir);
			map[tmp.x][tmp.y] = tmp.num;
			vc.push_back(tmp);
		}

		int ret = solution();

		printf("#%d %d\n", test_case, ret);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

