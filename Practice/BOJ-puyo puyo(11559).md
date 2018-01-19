```c++
/*
dfs 탐색
1. 터트릴 수 있는 뿌요 찾는다(dfs).
2. 터트린다 or 종료
3. 맵 다시 그려주기
--1,2,3 반복--
*/
#include <iostream>
#include <cstring>
#include <vector>
#include <utility>

using namespace std;

char map[12][6];
int chk[12][6];
int dx[] = { 1, 0, -1, 0 };
int dy[] = { 0, 1, 0, -1 };
int total_combo;
vector<pair<int, int>> tmp_loc;
void dfs(int x, int y, int depth, char cur_char) {

	for (int i = 0; i < 4; i++) {
		int nx = x + dx[i];
		int ny = y + dy[i];
		if (nx >= 0 && nx < 12 && ny >= 0 && ny < 6 && !chk[nx][ny] && map[nx][ny] == cur_char) {
			chk[nx][ny] = 1;
			tmp_loc.push_back(make_pair(nx, ny));
			dfs(nx, ny, depth + 1, map[nx][ny]);
		}
	}
}
void refresh() {
	/*
	맵 다시 그리기
	3중 루프로 쉽게 할 수 있음
	*/
	for (int i = 0; i < 6; i++) {
		for (int j = 10; j >= 0; j--) {
			for (int k = 11; k > j; k--) {
				if (map[j][i] != '.' && map[k][i] == '.') {
					map[k][i] = map[j][i];
					map[j][i] = '.';
					break;
				}
			}
		}
	}
}
int main() {

	total_combo = 0;

	for (int i = 0; i < 12; i++) {
		for (int j = 0; j < 6; j++) {
			cin >> map[i][j];
		}
	}
	
	while (1) {
		int combo = 0;
		bool isCombo = false;
		for (int i = 0; i < 12; i++) {
			for (int j = 0; j < 6; j++) {
				tmp_loc.clear();
				if (!chk[i][j] && map[i][j] != '.') {
					chk[i][j] = 1;
					dfs(i, j, 1, map[i][j]);
					if (tmp_loc.size() >= 3){
						map[i][j] = '.';
						isCombo = true;
						for (int k = 0; k < tmp_loc.size(); k++) {
							map[tmp_loc[k].first][tmp_loc[k].second] = '.';
						}
					}
				}
			}
		}
      	//더이상 콤보가 없을 경우 종료.
		if (!isCombo) {
			printf("%d\n", total_combo);
			break;
		}
		else {
			combo += 1;
		}
		total_combo += combo;
		refresh();
		for (int i = 0; i < 12; i++) {
			memset(chk[i], 0, sizeof(chk[i]));
		}
	}

	return 0;
}
```

